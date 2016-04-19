---
layout: post
title: Jupyter Python Notebook Keyboard Shortcuts and Text Snippets for Beginners
---

Here are some of the keyboard shortcuts and text snippets I've shared with others during Pair Programming sessions that have been well received. They've saved me countless hours programming and my hope is you'll be able to start using some of these techniques to become a more efficient Python programmer.

## Keyboard shortcuts

Taking a few minutes to learn certain Jupyter Notebook keyboard shortcuts has helped me be a more efficient Python developer. Below are the keyboard shortcuts I've found most useful.

But first...something key to be aware of: Jupyter Notebooks have two different keyboard input modes:

1. **Command mode** - binds the keyboard to notebook level actions. Indicated by a grey cell border with a blue left margin.
2. **Edit mode** - when you're typing in a cell. Indicated by a green cell border

**NOTE** these keyboard shortcuts are for Jupyter version 4.1.0 and Mac OSX. For most shortcuts below, you can replace `cmd` for `ctrl` for Windows or Linux. Or, you can use the `H` keyboard shortcut in Windows or Linux to confirm the appropriate keyboard shortcuts for those operating systems.

#### Command Mode

- `shift` + `enter` run cell, select below
- `ctrl` + `enter` run cell
- `option` + `enter` run cell, insert below
- `A` insert cell above
- `B` insert cell below
- `C` copy cell
- `V` paste cell
- `D` , `D` delete selected cell
- `shift` + `M` merge selected cells, or current cell with cell below if only one cell selected
- `I` , `I` interrupt kernel
- `0` , `0` restart kernel (with dialog)
- `Y` change cell to `code` mode
- `M` change cell to `markdown` mode (good for documentation)

<!-- |--
| Command | Description
|-:|:-
cmd + shift + p | open the command palette
`A` | insert cell above
|=== -->

#### Edit Mode

- `cmd` + `click` for multi-cursor editing
- `option` + `scrolling click` for column editing
- `cmd` + `/` toggle comment lines
- `tab` code completion or indent
- `shift` + `tab` tooltip
- `ctrl` + `shift` + `-` split cell

#### Command Palette

`cmd` + `shift` + `p`

Want quick access to all the commands in Jupyter Notebooks? Open the command palette with `cmd` + `shift` + `p` and you'll quickly be able to search all the commands!

<amp-img width="700" height="169" layout="responsive" src="/assets/images/keyboard-shortcuts/command_palette.png"></amp-img>

#### View all keyboard shortcuts

`H` (in Command mode)

Forget what that keyboard shortcut is? Type `H` in Command mode for a list of all available keyboard shortcuts.

<amp-img width="700" height="256" layout="responsive" src="/assets/images/keyboard-shortcuts/keyboard_shortcuts.png"></amp-img>

## Text snippets

Text snippets allow me to save time typing and keep things consistent.

For my text snippets, I use [Textexpander](https://textexpander.com/) which is Mac OSX only. However, for Windows I've used [PhraseExpress](http://www.phraseexpress.com/textexpander-windows.htm) in the past which works well too.

#### Quick imports for all your favorite packages

Constantly importing the same packages and/or forget what that package you always use is named? I like to store my default imports in a snippet such as the following. I'd recommend you create a similar snippet and tune it to your preferences.

`;imp` becomes:

~~~python
import numpy as np

import pandas as pd

from pandas import Series, DataFrame

from numpy.random import randn

from scipy import stats

import matplotlib as mpl
import matplotlib.pyplot as plt
import seaborn as sns
sns.set_style('whitegrid')

from __future__ import division

%matplotlib inline

import math

from sklearn.linear_model import LogisticRegression
from sklearn.linear_model import LinearRegression
from sklearn.cross_validation import train_test_split

from sklearn import metrics

import statsmodels.api as sm

from pprint import pprint
~~~


#### Making writing functions and documentation less painful

I like to remind myself to write a function DocString every time I write a function by using the following snippet.

`;def` becomes:

~~~python
def ():
    '''

    '''
~~~



<!-- Other ideas:
- python/ipython tips and tricks (textexpander for imports, tab-shift inside function parameters, cmd+click for multi-edit, tab to autocomplete, cmd+/ to comment, cmd+alt for column select, vars() to print object variables) -->
