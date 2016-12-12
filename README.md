# Whats' this?

:rotating_light: ***This package provide keymaps only. surround feature itself is provided by vim-mode-plus itself.***  

Provides default surround keymaps for [vim-mode-plus](https://atom.io/packages/vim-mode-plus).

Provides following keymaps.  

Unlike tpop's vim-surround. `d s`, `c s` **auto-detect** pair char to delete/change.  
But this is not perfect, if fail, try manual version `d S`, `c S`.  

| Mode     | Keystroke | Description                                                            |
|:---------|:----------|:-----------------------------------------------------------------------|
| `normal` | `y s`     | `surround` e.g. `y s i w (`                                            |
| `normal` | `d s`     | `delete-surround-any-pair`. auto-detect surrounding char. e.g. `d s`   |
| `normal` | `d S`     | `delete-surround` e.g. `d s (`                                         |
| `normal` | `c s`     | `change-surround-any-pair`. auto-detect surrounding char. e.g. `c s {` |
| `normal` | `c S`     | `change-surround`. auto-detect e.g. `c s ( {`                          |
| `visual` | `S`       | `surround` selected text. `S (`                                        |

# Don't want to move cursor after surround operator?

From setting-view of vim-mode-plus, Check `stayOnTransformString`.

# Explain behavior details in pseudo DSL

```coffeescript

# Normal-mode
# -------------------------
# Set base text. cursor is `|`.

text = """
  pen pin|eapple
  apple pen
  """

# y s
# -------------------------
setText(text)
normal 'y s i w {',
  text: """
  pen {pineapple}
  apple pen
  """

# `y s s` surround current line
setText(text)
normal 'y s s {',
  text: """
  {pen pineapple}
  apple pen
  """

# d s
# -------------------------
text = """
  pen pineapple
  (apple {pe|n})
  """

# `d s` delete surrounding char by auto-detect
setText(text)
normal 'd s',
  desc: "auto detect `{`"
  text: """
  pen pineapple
  (apple pen)
  """

normal 'd s',
  desc: "auto detect `(`"
  text: """
  pen pineapple
  apple pen
  """

setText(text)
normal 'd S (',
  desc: "manually specify surrounding char"
  text: """
  pen pineapple
  apple {pen}
  """

# c s
# -------------------------
text = """
  pen pineapple
  (apple {pe|n})
  """
setText(text)

normal 'c s "',
  text: """
  pen pineapple
  (apple "pen")
  """
normal 'c s [',
  text: """
  pen pineapple
  (apple [pen])
  """

normal 'c S [ <',
  text: """
  pen pineapple
  (apple <pen>)
  """

normal 'c S ( {',
  text: """
  pen pineapple
  {apple <pen>}
  """

# Visual-mode selected-area is | to |
# -------------------------
text = """
  pen pi|neap|ple
  apple pen
  """
setText(text)

visual 'S {',
  text: """
  pen pi{neap}ple
  apple pen
  """
```
