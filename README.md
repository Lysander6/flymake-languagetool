[![License: GPL v3](https://img.shields.io/badge/License-GPL%20v3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)
[![MELPA](https://melpa.org/packages/flymake-languagetool-badge.svg)](https://melpa.org/#/flymake-languagetool)
[![MELPA Stable](https://stable.melpa.org/packages/flymake-languagetool-badge.svg)](https://stable.melpa.org/#/flymake-languagetool)

<img align="right" src="./etc/logo.png" with="138" height="46">

# flymake-languagetool
> Flymake support for LanguageTool.

[![CI](https://github.com/emacs-languagetool/flymake-languagetool/actions/workflows/test.yml/badge.svg)](https://github.com/emacs-languagetool/flymake-languagetool/actions/workflows/test.yml)

## 💾 Installation

The instruction to use this plugin.

1. Download LanguageTool from https://languagetool.org/download/ and
   extract on to your local machine (skip this step if using a remote
   server).
2. Consider adding the following snippet to your configuration.

```el
(use-package flymake-languagetool
  :ensure t
  :hook ((text-mode       . flymake-languagetool-load)
         (latex-mode      . flymake-languagetool-load)
         (org-mode        . flymake-languagetool-load)
         (markdown-mode   . flymake-languagetool-load))
  :init
  ;; Remote server config with LanguageTool's free API
  ;; (setq flymake-languagetool-url "https://api.languagetool.org")
  ;; (setq flymake-languagetool-server-port nil)
  ;; (setq flymake-languagetool-server-jar nil)

  ;; Local server config
  (setq flymake-languagetool-server-jar "path/to/LanguageTool-X.X/languagetool-server.jar"))
```

3. :tada: Done! Now open a text file and hit `M-x flymake-mode`!

otherwise you can call `flymake-languagetool-maybe-load` like the snippet below.

```el
(add-hook 'find-file-hook 'flymake-languagetool-maybe-load)
```

## 🧪 Configuration

- `flymake-languagetool-server-jar`
- `flymake-languagetool-active-modes`
- `flymake-languagetool-check-spelling`
- `flymake-languagetool-language` (Default `"en-US"`)

### Spellchecking

LanguageTool’s spellchecking is disabled by default. If
`flymake-languagetool-check-spelling` is non-nil LanguageTool will check
for spelling mistakes.

### Disabling Rules & Categories

Specific rules can be disabled using
`flymake-languagetool-disabled-rules`. For example, LanguageTool's
whitespace rule can be a bit verbose in `org-mode` and it can be
disabled by adding its ID to this variable.

```el
(push "WHITESPACE_RULE" flymake-languagetool--disabled-rules)
```

The full list of rules and their IDs can be found [here](https://community.languagetool.org/rule/list?lang=en).

Similarly, you can disable categories using the
`flymake-languagetool-disabled-categories` variable. The full list of
categories can be found in `flymake-languagetool-map`

You can also disable rules and categories interactively with the `Ignore`
option. These rules will be ignored temporarily, for the current buffer
only.

### Corrections

Suggestions from LanguageTool can be applied with:

`flymake-languagetool-correct`: select error in current buffer with
    completing read

`flymake-languagetool-correct-at-point`: correct error at point

`flymake-languagetool-correct-dwim`: if point is on a
    `flymake-languagetool` error then correct; otherwise, select one
    from the current buffer.

### Categories

By default, `flymake-languagetool` will now provide LanguageTool
category information for each identified error. If you wish to disable
this behavior, you can set `flymake-languagetool-use-categories = nil`.

<img align="middle" src="./etc/diagnostics.png" with="500" height="700">

## 🛠️ Contribute

[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](http://makeapullrequest.com)
[![Elisp styleguide](https://img.shields.io/badge/elisp-style%20guide-purple)](https://github.com/bbatsov/emacs-lisp-style-guide)
[![Donate on paypal](https://img.shields.io/badge/paypal-donate-1?logo=paypal&color=blue)](https://www.paypal.me/jcs090218)
[![Become a patron](https://img.shields.io/badge/patreon-become%20a%20patron-orange.svg?logo=patreon)](https://www.patreon.com/jcs090218)

If you would like to contribute to this project, you may either
clone and make pull requests to this repository. Or you can
clone the project and establish your own branch of this tool.
Any methods are welcome!

### 🔬 Development

To run the test locally, you will need the following tools:

- [Eask](https://emacs-eask.github.io/)
- [Make](https://www.gnu.org/software/make/) (optional)

Install all dependencies and development dependencies:

```sh
$ eask install-deps --dev
```

To test the package's installation:

```sh
$ eask package
$ eask install
```

To test compilation:

```sh
$ eask compile
```

**🪧 The following steps are optional, but we recommend you follow these lint results!**

The built-in `checkdoc` linter:

```sh
$ eask lint checkdoc
```

The standard `package` linter:

```sh
$ eask lint package
```

*📝 P.S. For more information, find the Eask manual at https://emacs-eask.github.io/.*

## ⚜️ License

This program is free software; you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see <https://www.gnu.org/licenses/>.

See [`LICENSE`](./LICENSE.txt) for details.
