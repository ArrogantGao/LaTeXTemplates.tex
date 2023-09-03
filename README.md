# LaTeXTemplates.tex
This is a self-made project for some LaTeX templates.

I use vscode + MacTex + github to organize my scripts (previously I was using the overleaf).
Here is a simple guide for using vscode for LaTeX.

**Step 1**

Install ```MacTeX```.

**Step 2**

Install ```vscode``` and ```latex workshop```.

**Step 3**

Create a scrpit ```LaTeXCompiler``` under you ```bin``` dir, copy the following code into it.
```
#! /bin/bash

pdflatex -synctex=1 -interaction=nonstopmode -file-line-error $1.tex
bibtex $1
pdflatex -synctex=1 -interaction=nonstopmode -file-line-error $1.tex
pdflatex -synctex=1 -interaction=nonstopmode -file-line-error $1.tex
rm -f *.thm *.aux *.bbl *.blg *.idx *.ind *.lof *.lot *.out *.toc *.acn *.acr *.alg *.glg *.glo *.gls *.ist *.fls *.log *.fdb_latexmk *.gz
```
Then use ```chmod 777 LaTeXCompiler``` to make it runable.

Try to run this command ```LaTeXCompiler main``` in your own project to test.

**Step 4**

If the test above works, add these code to ```settings.json``` of vscode:

```
    "latex-workshop.showContextMenu": true,
    "latex-workshop.intellisense.package.enabled": true,
    "latex-workshop.message.error.show": true,
    "latex-workshop.message.warning.show": true,
       
    "latex-workshop.latex.tools": [
        {
        "name": "xelatex",
        "command": "xelatex",
        "args": [
          "-synctex=1",
          "-interaction=nonstopmode",
          "-file-line-error",
          "%DOC%"
        ]
        }, 
        {
        "name": "pdflatex",
        "command": "pdflatex",
        "args": [
          "-synctex=1",
          "-interaction=nonstopmode",
          "-file-line-error",
          "%DOC%"
        ]
        }, 
        {
        "name": "bibtex",
        "command": "bibtex",
        "args": [
          "%DOCFILE%"
        ]
        },
        {
          "name": "LaTeXCompiler",
          "command": "LaTeXCompiler",
          "args": [
            "%DOCFILE%"
          ]
          }
      ],

        "latex-workshop.latex.recipes": [
          {
            "name": "LaTeXCompiler",
            "tools": [
                "LaTeXCompiler"
            ]
          },
         
          {
            "name": "xelatex",
            "tools": [
                "xelatex"
            ]
          },
  
          {
            "name": "bibtex",
            "tools": [
                "bibtex"
            ]
          },
  
          {
            "name": "pdflatex",
            "tools": [
                "pdflatex"
            ]
          },
      ],

        "latex-workshop.view.pdf.viewer": "tab",

        "latex-workshop.latex.clean.fileTypes": [
          "*.aux",
          "*.bbl",
          "*.blg",
          "*.idx",
          "*.ind",
          "*.lof",
          "*.lot",
          "*.out",
          "*.toc",
          "*.acn",
          "*.acr",
          "*.alg",
          "*.glg",
          "*.glo",
          "*.gls",
          "*.ist",
          "*.fls",
          "*.log",
          "*.fdb_latexmk"
      ],
      "latex.linter.enabled": false,
      "latex-workshop.latex.autoClean.run": "onFailed",
      "latex-workshop.latex.recipe.default": "lastUsed",
      "latex-workshop.view.pdf.internal.synctex.keybinding": "double-click",
```
and it will work.
