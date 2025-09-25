---
---

# Bootup

```dataviewjs


// # BOOTUP 

this.app.workspace.onLayoutReady(
  main.bind(this)
);

// ## MAIN << BOOTUP
function main() {
  if (!this.app?.mrender?.renderEl) {
    this.app.mrender = {}
  
    this.app.mrender.renderEl = renderEl
    function renderEl(_value = 0, max = 100) {
        const space = "&nbsp;"
        const progress_html = `<progress value="${_value}" max="${max}"></progress>${space.repeat(10)}<span>${((_value/max)*100).toFixed(2)}%</span>`
        const $p = this.container.createEl("p", {attr: {style: `margin: 0.2em 1em .2em 1em`}})
        $p.innerHTML = progress_html;
    }
  }
  
	const hasDataview = this.app.plugins.enabledPlugins.has("dataview");
	console.log({hasDataview})
	if (hasDataview) {
		const dataviewApi = this.app.plugins.plugins.dataview.api;

		// populate evalution context so that inline dql can use functions
		for (const key in DefaultFunctions) {
			dataviewApi.evaluationContext
				.functions[key] = DefaultFunctions[key];
			dataviewApi.func[key] = DefaultFunctions[key];

		}
	}
	
}
// # Hoisted utilities 
function hoistFunctionBuilderClass() {
	return class FunctionBuilder {
		name;
		variants;
		vectorized;
		constructor(name) {
			this.name = name;
			this.variants = [];
			this.vectorized = {};
		}
		/** Add a general function variant which accepts any number of arguments of any type. */
		vararg(impl) {
			this.variants.push({ args: [], varargs: true, impl });
			return this;
		}
		/** Add a function variant which takes in a single argument. */
		add1(argType, impl) {
			this.variants.push({
				args: [argType],
				varargs: false,
				impl: (c, ...rest) => impl(rest[0], c),
			});
			return this;
		}
		/** Add a function variant which takes in two typed arguments. */
		add2(arg1, arg2, impl) {
			this.variants.push({
				args: [arg1, arg2],
				varargs: false,
				impl: (c, ...rest) => impl(rest[0], rest[1], c),
			});
			return this;
		}
		/** Add a function variant which takes in three typed arguments. */
		add3(arg1, arg2, arg3, impl) {
			this.variants.push({
				args: [arg1, arg2, arg3],
				varargs: false,
				impl: (c, ...rest) => impl(rest[0], rest[1], rest[2], c),
			});
			return this;
		}
		/** Add vectorized variants which accept the given number of arguments and delegate. */
		vectorize(numArgs, positions) {
			this.vectorized[numArgs] = positions;
			return this;
		}
		/** Return a function which checks the number and type of arguments, passing them on to the first matching variant. */
		build() {
			let self = (context, ...args) => {
				let types = [];
				for (let arg of args) {
					let argType = Values.typeOf(arg);
					if (!argType)
						throw Error(`Unrecognized argument type for argument '${arg}'`);
					types.push(argType);
				}
				// Handle vectorization, possibly in multiple fields.
				if (this.vectorized[types.length]) {
					let vectorizedPositions = this.vectorized[types.length].filter(
						(k) => types[k] == 'array'
					);
					if (vectorizedPositions.length > 0) {
						let minLength = vectorizedPositions
							.map((p) => args[p].length)
							.reduce((p, c) => Math.min(p, c));
						// Call the subfunction for each element in the longest array.
						// If you call a vectorized function with different-length arrays,
						// the output is limited by the length of the shortest array.
						let result = [];
						for (let vpos = 0; vpos < minLength; vpos++) {
							let subargs = [];
							for (let index = 0; index < args.length; index++) {
								if (vectorizedPositions.includes(index)) {
									let arr = args[index];
									subargs.push(arr[vpos]);
								} else {
									subargs.push(args[index]);
								}
							}
							result.push(self(context, ...subargs));
						}
						return result;
					}
				}
				outer: for (let variant of this.variants) {
					if (variant.varargs) return variant.impl(context, ...args);
					if (variant.args.length != types.length) continue;
					for (let index = 0; index < variant.args.length; index++) {
						if (variant.args[index] != '*' && variant.args[index] != types[index])
							continue outer;
					}
					return variant.impl(context, ...args);
				}
				throw Error(
					`No implementation of '${this.name}' found for arguments: ${types.join(
						', '
					)}`
				);
			};
			return self;
		}
	}
}
```
