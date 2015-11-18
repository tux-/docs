Atom
====

Setup
-----

Install packages
```
Sublime-Style-Column-Selection
```

Config.json:
```
"*":
  "exception-reporting":
    userId: "8ef021f7-4975-979e-6e19-4e748c229831"
  welcome:
    showOnStartup: false
  core: {}
  editor:
    invisibles: {}
    showInvisibles: true
    tabType: "hard"
    scrollPastEnd: true
    preferredLineLength: 132
    showIndentGuide: true
    softTabs: false
    tabLength: 4
  "bracket-matcher":
    autocompleteBrackets: false
    autocompleteSmartQuotes: false
    wrapSelectionsInBrackets: false
  tabs:
    usePreviewTabs: true
```

Add to styles.less
```
atom-text-editor::shadow {
	.editor-contents--private .invisible-character, .editor-contents--private .indent-guide {
		visibility: hidden;
	}

	.editor-contents--private.has-selection .invisible-character, .editor-contents--private.has-selection .indent-guide {
		visibility: visible;
	}
}
```

Add to keymap.json:
```
'atom-workspace atom-text-editor:not([mini])':
  'ctrl-shift-c': 'editor:toggle-line-comments'
```
