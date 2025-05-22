<%*
const top_string = atob(`PCUqIC8qKg==`)

const lower_string = atob(`KiovXyU+`)

await tp.file.cursor_append(top_string)
await tp.file.cursor_append("\n\n")
await tp.file.cursor_append(lower_string)

/**
* v0.0.2 *2025-05-06*
	* normalize file name
	* add MUID to filename
* v.0.0.1 *2025-01-23*
	* Use Base64 encoding on the sensitive strings so that the text doesn't trigger templater parsing/warning issues. It must be the initial read that has the error.
**/
_%>