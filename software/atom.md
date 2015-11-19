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



Keyboard Shortcut Cheat Sheet
-----------------------------

Use these rapid keyboard shortcuts to control the GitHub Atom text editor on xUbuntu.

### Keys ###

* <kbd>⌫ Backspace</kbd> : Delete key
* <kbd>↹ Tab</kbd> : Tab key
* <kbd>← Left</kbd> : Left arrow key
* <kbd>→ Right</kbd> : Right arrow key
* <kbd>↑ Up</kbd> : Up arrow key
* <kbd>↓ Down</kbd> : Down arrow key
* <kbd>↩ Enter</kbd> : Return or Enter key
* <kbd>⇧ Shift</kbd> : Shift key
* <kbd>⌃ Ctrl</kbd> : Control key
* <kbd>⎇ Alt</kbd> : Alt key
* <kbd>⎇ AltGr</kbd> : Alt Gr key
* <kbd>◆ Super</kbd> : Super key
* <kbd>Space</kbd> : Space key


### Actions ###

| Task                     | Keystrokes                                            |
|--------------------------|-------------------------------------------------------|
| Open Command Palette     | <kbd>⌃ Ctrl</kbd> + <kbd>⇧ Shift</kbd> + <kbd>P</kbd> |
| Open Settings            | <kbd>⌃ Ctrl</kbd> + <kbd>,</kbd>                      |
| Toggle developer console | <kbd>⌃ Ctrl</kbd> + <kbd>⇧ Shift</kbd> + <kbd>I</kbd> |
| Auto complete            | <kbd>⌃ Ctrl</kbd> + <kbd>Space</kbd>                  |
| Jump to matching bracket | <kbd>⌃ Ctrl</kbd> + <kbd>M</kbd>  |
| Toggle comment lines     | <kbd>⌃ Ctrl</kbd> + <kbd>⇧ Shift</kbd> + <kbd>C</kbd> |
