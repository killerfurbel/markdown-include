# How It Works !heading

markdown-include works by recursively going through files based on the tags that are found.  For instance, consider the following in a `_README.md` file:

```
#include "first-file.md" !ignore
```

Let's also consider that `first-file.md` contains the following:

```
#include "third-file.md" !ignore
```

Let's also consider that `markdown.json` contains the following:

```json
{
	"build" : "README.md",
	"files" : ["_README.md"]
}
```

markdown-include will first read the contents of `_README.md` and look for include tags.  It will find `#include "first-file.md"` first.  From there it will parse the tag, open `first-fild.md` and find include tags in that file.  This process continues until no more include tags are found.  

At that point it will start over in the original file and parse other include tags if they exist.  Along the way, markdown-include will parse each file and keep a record of the contents.  Once the process is finished, a file will be written in `README.md` with all of the compiled content.

As you can see, you only need to reference one file which would be `_README.md`.  We didn't need to add `first-file.md` or `third-file.md`... markdown-include does that compiling for us by making an internal chain.

**NOTE**:  You must provide markdown-include with the entire file path you're trying to find in your working directory.  For example, if `first-file.md` and `third-file.md` were in the `docs` directory together and `first-file.md` was trying to include `third-file.md` you would need to do the following in `first-file.md`:

```
#include "docs/third-file.md" !ignore
```

This is because markdown-include doesn't make any assumptions about where your files are.  Use the correct paths or you could run into errors!