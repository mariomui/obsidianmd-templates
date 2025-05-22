## 20-Inlink

> [!info]- Get Macros that Consume v0.0.1 `=this.MUID` 
`= join( map( filter( this.file.inlinks, (link) => icontains(meta(link).path, "macro") ) , (link) => "• " + link ), "<br>")`
