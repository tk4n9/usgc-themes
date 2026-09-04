# USGC Sublime Text Color Schemes
For text only, not designed for programming.

### Sublime Text
Download and obtain a license here: https://www.sublimetext.com/

### Installation
Settings > Browse Packages... > Paste theme files in this directory.

### Themes list

U.S. Graphics Company internal part numbers.
```text
┌─────────────┬─────────────┬────────────────┬──────────────────────────────────┐
│ PART NUMBER │ THEME NAME  │ DESCRIPTION    │ COMMENT                          │
├─────────────┼─────────────┼────────────────┼──────────────────────────────────┤
│ 5200-010    │ HIGHK       │ White scheme   │ High dielectric constant         │
│ 5200-020    │ RETICLE     │ Dark scheme    │ Photomask for lithography        │
│ 5200-030    │ POLYIMIDE   │ Amber scheme   │ Heat-resistant polymer           │
│ 5200-040    │ EPITAXY     │ Magenta scheme │ Crystal layer growth             │
│ 5200-050    │ METALGATE   │ Cyan scheme    │ Metal gate transistor            │
└─────────────┴─────────────┴────────────────┴──────────────────────────────────┘
```

Theme file names are formatted as `USGC-<THEME NAME>-<SOFTWARE CODE>`.

```text
┌───────────────┬────────────────┐
│ SOFTWARE CODE │ SOFTWARE NAME  │
├───────────────┼────────────────┤
│ ST            │ Sublime Text   │
│ IT            │ iTerm2         │
│ VSC           │ VS Code        │
└───────────────┴────────────────┘
```

### Standard colors
```text
┌───────────┬──────────────────────┐
│ HEX COLOR │ NAME                 │
├───────────┼──────────────────────┤
│ 000000    │ BLACK                │
│ FFFFFF    │ WHITE                │
│ FF0000    │ FL RED               │
│ 00FF00    │ FL GREEN             │
│ 0000FF    │ FL BLUE              │
│ 00FFFF    │ FL CYAN              │
│ FF00FF    │ FL MAGENTA           │
│ FFFF00    │ FL YELLOW            │
│ FF6600    │ FL ORANGE            │
│ 660000    │ MAROON               │
│ 00A645    │ GREEN                │
│ 000066    │ BLUE                 │
│ 006666    │ CYAN                 │
│ 660066    │ MAGENTA              │
│ FFBF00    │ YELLOW               │
│ 666600    │ OLIVE                │
│ 999999    │ GRAY                 │
└───────────┴──────────────────────┘
```

### Sublime Text Preferences

These themes work best with the following settings in your `Preferences.sublime-settings` file:

<img width="600" alt="usgc-theme-colors" src="https://github.com/user-attachments/assets/f0210f2a-9468-48d9-9ecf-30547e601526" />

WARNING: `vim` mode is active in this settings file.
```json
{
	"theme": "Adaptive.sublime-theme",
	"color_scheme": "USGC-RETICLE-ST.sublime-color-scheme",
	"theme_font_options": ["no_italic"],
	"auto_complete": true,
	"caret_blink_interval": 0.5,
	"caret_extra_bottom": -5,
	"caret_extra_top": -5,
	"caret_extra_width": 0,	
	"caret_style": "wide",
	"font_face": "Berkeley Mono Condensed",
	"font_size": 13,
	"font_options": ["no_italic"],
	"line_padding_top": -1,
	"line_padding_bottom": -1,
	"highlight_line": false,
	"rulers": [96],
	"default_line_endings": "unix",
	"show_line_endings": false,
	"tab_size": 4,
	"tab_completion": false,
	"detect_indentation": false,
	"draw_white_space": "none",
	"draw_indent_guides": false,
	"index_files": true,
	"ignored_packages": [
	]
}

```

### Screenshots

Here is the updated flowing table with a merged header column:

Here is the updated Markdown table with all text in code format and without bold formatting:

| U.S. Graphics Company Themes |                                                                                                                                                                              |
|------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| `HIGHK`<br>`USGC-HIGHK-ST`<br>`PN#: 5200-010`<br><img width="460" alt="HIGHK" src="https://github.com/user-attachments/assets/fe0ebfa7-2725-4eb0-bd67-5d316daa8a63" /> | `RETICLE`<br>`USGC-RETICLE-ST`<br>`PN#: 5200-020`<br><img width="460" alt="RETICLE" src="https://github.com/user-attachments/assets/d5c16dec-2374-4dc3-8e61-d756eb345b65" /> |
| `POLYIMIDE`<br>`USGC-POLYIMIDE-ST`<br>`PN#: 5200-030`<br><img width="460" alt="POLYIMIDE" src="https://github.com/user-attachments/assets/05e4576a-6006-4f01-9a08-a5b54e05d21d" /> | `EPITAXY`<br>`USGC-EPITAXY-ST`<br>`PN#: 5200-040`<br><img width="460" alt="EPITAXY" src="https://github.com/user-attachments/assets/729ea77b-f101-4e22-988d-7f4d404dc37e" /> |
| `METALGATE`<br>`USGC-METALGATE-ST`<br>`PN#: 5200-050`<br><img width="460" alt="METALGATE" src="https://github.com/user-attachments/assets/aa7d4900-6621-4c0d-a989-3c555ebdf1ee" /> |                                                                                                                                                                              |


# USGC iTerm Color Schemes

For macOS iTerm only.

### Instructions

- Settings (⌘ + ,) 
- Profiles Tab
- Select a profile in the left column
- Colors Tab
- Color Presets... > Import...
- Select the `.itermcolors` file
- Color Presets... > Select the imported scheme `USGC-<THEME NAME>-IT`

### USGC Bash Prompt
```
# USGC BASH PROMPT
if [[ $- == *i* ]]; then
  export CLICOLOR=1
  export LSCOLORS=GxFxCxDxBxegedabagaced
  export PS1="\[$(tput setaf 7)\]❬\h❭ \[$(tput setaf 2)\]\W\[$(tput setaf 1)\] ●\[$(tput sgr0)\] "
fi
```


### Part Numbers
```
┌─────────────┬─────────────┬────────────────┐
│ PART NUMBER │ THEME NAME  │ DESCRIPTION    │
├─────────────┼─────────────┼────────────────┤
│ 5201-010    │ HIGHK       │ White scheme   │
│ 5201-020    │ RETICLE     │ Dark scheme    │
│ 5201-030    │ POLYIMIDE   │ Amber scheme   │
│ 5201-040    │ EPITAXY     │ Magenta scheme │
│ 5201-050    │ METALGATE   │ Cyan scheme    │
└─────────────┴─────────────┴────────────────┘
```
### Screenshot
<img width="600" alt="USGC-RETICLE-IT" src="https://github.com/user-attachments/assets/b3fcf389-ae20-438f-903a-1e0220ab7369" />


# USGC VS Code Color Themes

Full-workbench themes: editor, sidebar, tabs, activity/status/title bars, panels and the integrated
terminal all use the theme background and foreground, `GRAY` for secondary text and borders, and the
theme's caret and selection colors as accents. Syntax coloring is minimal: comments are `GRAY`, strings
and keywords each get one accent color from the palette, everything else is the theme foreground.
The integrated terminal uses the same 16 ANSI colors as the iTerm2 schemes.

### Installation

The `themes/vscode` directory is a complete VS Code extension. Copying or symlinking it into
`~/.vscode/extensions` does not work: since VS Code 1.74 only extensions registered in that
folder's `extensions.json` are loaded (see microsoft/vscode#175069).

- Command Palette (⇧⌘P) > `Developer: Install Extension from Location...`
- Select the `themes/vscode` directory
- Command Palette > `Preferences: Color Theme` > select `USGC-<THEME NAME>-VSC`

Alternatively, build and install a package (requires Node.js 20 or newer):
```
cd themes/vscode
npx @vscode/vsce package
code --install-extension usgc-themes-<version>.vsix
```

To try the themes without installing, open an Extension Development Host window:
```
code --extensionDevelopmentPath="$PWD/themes/vscode"
```

### VS Code Preferences

These themes work best with the following settings in your `settings.json` file. The
`editor.renderLineHighlight` value reproduces the Sublime look: the current line number gets the
theme's `line_highlight` color while the text line itself stays unhighlighted.

```json
{
	"workbench.colorTheme": "USGC-RETICLE-VSC",
	"editor.fontFamily": "Berkeley Mono Condensed",
	"editor.fontSize": 13,
	"editor.renderLineHighlight": "gutter",
	"editor.rulers": [96],
	"editor.tabSize": 4,
	"editor.detectIndentation": false,
	"editor.renderWhitespace": "none",
	"editor.guides.indentation": false,
	"files.eol": "\n"
}
```

### Part Numbers
```
┌─────────────┬─────────────┬────────────────┐
│ PART NUMBER │ THEME NAME  │ DESCRIPTION    │
├─────────────┼─────────────┼────────────────┤
│ 5202-010    │ HIGHK       │ White scheme   │
│ 5202-020    │ RETICLE     │ Dark scheme    │
│ 5202-030    │ POLYIMIDE   │ Amber scheme   │
│ 5202-040    │ EPITAXY     │ Magenta scheme │
│ 5202-050    │ METALGATE   │ Cyan scheme    │
└─────────────┴─────────────┴────────────────┘
```
