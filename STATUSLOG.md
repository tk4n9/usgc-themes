# STATUSLOG

Chronological log of changes to this repository, kept so that any agent or person can pick up the
work without re-deriving decisions. Newest entry first. Dates are absolute (YYYY-MM-DD).

---

## 2026-10-31 — Ghostty themes for all five schemes (`themes/ghostty`)

### User prompt (verbatim)

> Read this repository. I would like to make a theme family for ghostty terminal as well.

### Clarifying questions asked and the user's answers

| Question | Answer chosen |
|---|---|
| Software code in file names | **GT** → `USGC-<THEME NAME>-GT` |
| RETICLE terminal colors: strict palette (as in VS Code and the other four iTerm2 schemes) or a P3→sRGB copy of the hand-tuned RETICLE-IT | **Strict palette** |
| Set Ghostty-only colors beyond the 7 keys that Ghostty's bundled themes use | **Yes: search matches and split divider** (needs Ghostty ≥ 1.3.0) |
| Also install the themes on this machine | **Yes, copy to `~/.config/ghostty/themes/`**; the user's Ghostty config is not edited |

Not asked, following precedent: directory `themes/ghostty` (sibling of `themes/iterm` and `themes/vscode`)
and part numbers 5203-010 … 5203-050 (continuing 5200 ST, 5201 IT, 5202 VSC in Sublime order).

### Files changed

| File | Action | Reason |
|---|---|---|
| `themes/ghostty/USGC-{HIGHK,RETICLE,POLYIMIDE,EPITAXY,METALGATE}-GT` | added | the five themes. No file extension: Ghostty's `theme =` value is the file name, and its bundled themes have none |
| `README.md` | added `GT / Ghostty` row to the software-code table; added "USGC Ghostty Color Themes" section (install steps, light/dark pairing, preferences snippet, `minimum-contrast` tip, 5203 part-number table) | document the new themes, mirroring the other sections |
| `STATUSLOG.md` | this entry | |

Outside the repo: created `~/.config/ghostty/themes/` (did not exist) and copied the five files into it.
The agent did not modify `~/.config/ghostty/config`; at the time it set `theme = "Xcode Light"` and
`cursor-color = "#ebb03c"`, which overrides the cursor color of any theme, USGC included (see
"Follow-up prompts" for the user's later change).

Not changed: Sublime, iTerm2 and VS Code themes, `VERSION`, `pkg`, `.gitignore`. Committed and pushed
later in the session (see "Follow-up prompts" at the end of this entry).

### Theme file format

- A Ghostty theme is an ordinary Ghostty config file (`key = value`; `#` comments only on their own
  line). `theme = <name>` searches `$XDG_CONFIG_HOME/ghostty/themes` (or `~/.config/ghostty/themes`),
  then the bundled themes; `theme = /absolute/path` also works. Colors set in the user's own config
  (`background`, `cursor-color`, `palette`, …) override the theme. Source: `ghostty +show-config --default --docs`
  of the installed Ghostty 1.4.0 (stable channel).
- Hex is uppercase `#RRGGBB`, like the rest of this repo (bundled themes use lowercase; both parse).
- Layout: `palette` 0–15, blank line, the 6 core keys (same keys and order as all 819 bundled
  themes), blank line, the 5 Ghostty-only keys. No comments, like the other theme files.

### Mapping rules (Sublime `globals` → Ghostty keys)

| Ghostty key | Source | Note |
|---|---|---|
| `palette = 0..15` | strict USGC ANSI table (see the iTerm2 entry below) | identical in all five files |
| `background` | `background` | |
| `foreground` | `foreground` | |
| `cursor-color` | `caret` | |
| `cursor-text` | BLACK or WHITE, whichever has the higher WCAG contrast against `caret` | same rule as iTerm2 and VS Code |
| `selection-background` | `selection` | |
| `selection-foreground` | `selection_foreground` | |
| `search-selected-background` / `search-selected-foreground` | FL YELLOW / BLACK | current match; = VS Code `findMatchBackground`, iTerm2 `Match Background Color` |
| `search-background` / `search-foreground` | YELLOW / BLACK | other matches; = VS Code `findMatchHighlightBackground` minus its alpha (Ghostty colors have no alpha) |
| `split-divider-color` | GRAY | = VS Code BORDER minus its alpha |

Deliberately not set:
- `bold-color`: setting it to a color also switches all other bold text to the bright palette (per
  Ghostty docs). Unset, bold text keeps its own color, which matches iTerm2's `Bold Color` = foreground.
- `unfocused-split-fill`: defaults to the background color, already a palette color.
- `window-titlebar-background` / `-foreground`: GTK only, only with `window-theme = ghostty`, which
  then uses background/foreground anyway.
- `palette-generate`: off (default), so indices 16–255 stay the xterm standard instead of being
  derived from the strict palette.
- `minimum-contrast`, `cursor-style`, fonts: user preferences, not colors; README suggests them.
- `window-colorspace`: default sRGB; all values are sRGB hex.

### Per-theme values (hex)

| Key | HIGHK | RETICLE | POLYIMIDE | EPITAXY | METALGATE |
|---|---|---|---|---|---|
| `background` | FFFFFF | 000000 | 000000 | 000000 | 000000 |
| `foreground` | 000000 | 00A645 | FFBF00 | FF00FF | 00FFFF |
| `cursor-color` | 0000FF | FFFFFF | 00A645 | FFFFFF | 0000FF |
| `cursor-text` | FFFFFF | 000000 | 000000 | 000000 | FFFFFF |
| `selection-background` | 00FF00 | FFFFFF | 000066 | 000066 | 666600 |
| `selection-foreground` | 000000 | 0000FF | 00FFFF | FFFF00 | FFFF00 |

Same in all five: `search-background` FFBF00, `search-selected-background` FFFF00, both foregrounds
000000, `split-divider-color` 999999.

### Minimum Ghostty version

Checked by grepping `src/config/Config.zig` at release tags, fetched 2026-10-31 from
`raw.githubusercontent.com/ghostty-org/ghostty/<tag>/`:

| Keys | First tag containing them |
|---|---|
| `palette`, `background`, `foreground`, `cursor-color`, `cursor-text`, `selection-background`, `selection-foreground` | v1.0.0 |
| `split-divider-color` | v1.1.0 |
| `search-foreground`, `search-background`, `search-selected-foreground`, `search-selected-background` | v1.3.0 (absent in v1.2.0) |

Hence "Ghostty 1.3.0 or later" in the README. Ghostty 1.3.0 was released 2026-03-09 (official release
notes); those notes do not list the new search color keys, so the tag check is the evidence. On older
versions the search keys are unknown fields; Ghostty 1.4.0 reports unknown keys in a theme as
`unknown field` errors. Behavior on 1.1/1.2 was not tested.

### Validation performed (2026-10-31, Ghostty 1.4.0 stable, macOS)

1. `ghostty +validate-config --config-file=<theme>` on each file: exit 0, no output. The same command
   reports `unknown field` and `invalid value` for a deliberately broken theme, also when it is loaded
   through `theme = /abs/path`, so the check is not vacuous.
2. In a temporary `XDG_CONFIG_HOME` (real config untouched), `theme = USGC-<NAME>-GT` resolved by name,
   and `ghostty +show-config` matched all 27 keys of each file. `+show-config` omits values equal to the
   defaults (e.g. `search-foreground = #000000`), so its output was merged over `+show-config --default`.
3. The 22 shared keys (background, foreground, cursor, cursor text, selection pair, 16 ANSI) equal the
   `terminal.*` colors of the matching VS Code theme (all five) and the matching iTerm2 scheme (HIGHK,
   POLYIMIDE, EPITAXY, METALGATE; RETICLE-IT is hand-tuned and differs by design).
4. `ghostty +list-themes --plain --color=light` lists only HIGHK; `--color=dark` lists the other four.
   `theme = light:USGC-HIGHK-GT,dark:USGC-RETICLE-GT` validates.
5. Installed copies are byte-identical to the repo files (`cmp`); unsandboxed `ghostty +list-themes`
   lists all five as `(user)`; the user's real config still validates.
6. README snippet: `shell-integration-features = no-cursor` resolves to
   `no-cursor,no-sudo,title,no-ssh-env,no-ssh-terminfo,path`, so only the cursor feature changes.
7. README `minimum-contrast` wording checked against `contrasted_color()` in
   `src/renderer/shaders/shaders.metal` (v1.3.0): text below the ratio is drawn white or black,
   whichever contrasts more with the cell background.

Not done: no visual check in a Ghostty window. The README's `font-family = "Berkeley Mono Condensed"`
copies the Sublime and VS Code snippets; this machine has only `Berkeley Mono` installed
(`ghostty +list-fonts`), so that family name is unverified in Ghostty.

### Contrast notes (WCAG ratios, computed)

| Theme | fg / bg | selection fg / selection bg | current match bg / bg | other match bg / bg | divider / bg |
|---|---|---|---|---|---|
| HIGHK | 21.00 | 15.30 | 1.07 | 1.65 | 2.85 |
| RETICLE | 6.54 | 8.59 | 19.56 | 12.70 | 7.37 |
| POLYIMIDE | 12.70 | 14.05 | 19.56 | 12.70 | 7.37 |
| EPITAXY | 6.70 | 16.41 | 19.56 | 12.70 | 7.37 |
| METALGATE | 16.75 | 5.64 | 19.56 | 12.70 | 7.37 |

Match text is BLACK: 19.56 on FL YELLOW, 12.70 on YELLOW.
- HIGHK: the FL YELLOW current-match block differs from the white background mostly in hue
  (1.07:1 luminance), the same as VS Code and iTerm2 HIGHK.
- POLYIMIDE: the other-match color YELLOW equals its foreground, so those matches look like inverse video.
- ANSI trade-offs are those listed in the iTerm2 entry. On RETICLE, the USGC prompt's `setaf 2`
  directory is GREEN, the same as the foreground, and its `setaf 1` dot is MAROON (1.6:1 on black);
  accepted with the strict-palette choice.

### Observation (not changed)

The README's VS Code section says the integrated terminal uses "the same 16 ANSI colors as the iTerm2
schemes". That holds for HIGHK, POLYIMIDE, EPITAXY and METALGATE; RETICLE-VSC uses the strict palette
while RETICLE-IT is hand-tuned. Left as is; the Ghostty section states the exception.

### How to verify / regenerate

- Check: `ghostty +validate-config --config-file=themes/ghostty/USGC-HIGHK-GT` (no output = valid).
  After copying to `~/.config/ghostty/themes/`, `ghostty +list-themes` shows a live preview.
- Regeneration is fully specified by the tables above; the throwaway generator and verifier used this
  session were not committed.

### Follow-up prompts (same session)

> How can I apply this theme?

Answered in chat; no files changed. Steps given: in `~/.config/ghostty/config` replace
`theme = "Xcode Light"` with `theme = USGC-<THEME NAME>-GT`, delete `cursor-color = "#ebb03c"`, save,
reload with ⌘⇧,. By the next prompt the user had set `theme = USGC-HIGHK-GT` themselves.

> Commit and push the changes

- Committed on a new branch `ghostty-themes`, not on `master`: Claude Code's git rule is to branch
  before committing on the default branch, and the prompt named no branch. Local `master` was not
  touched.
- `git fetch` showed `origin/master` one commit ahead: `ffa714b` "Fix VS Code install instructions"
  (README install block plus a STATUSLOG correction entry, from the VS Code session), not yet in this
  clone. The branch was rebased onto it. Only conflict: both add a STATUSLOG entry at the top;
  resolved newest first (this entry, then the 2026-09-04 correction).
- Three commits, mirroring the VS Code ones: theme files, README, this log. Branch pushed to `origin`
  (`git@github.com:tk4n9/usgc-themes.git`) with upstream tracking.
- Not on `master` yet. To land it: fast-forward `master` to `ghostty-themes` and push, or merge a pull
  request into `master`.

---

## 2026-09-04 — Correction: VS Code install instructions

### User prompt (verbatim)

> I linked the extension folder into vscode's extensions directory. Also, I restarted the VSCode.
> However, I cannot see the themes from my color theme selector dropdown.

### Cause

The README told users to copy or symlink `themes/vscode` into `~/.vscode/extensions`. That has not
worked since VS Code 1.74 (December 2022): the extensions folder is no longer scanned; only
extensions listed in its `extensions.json` registry are loaded. A VS Code team member reproduced
the exact symlink scenario in microsoft/vscode#175069 ("Can't copy/symlink extensions into
code-oss"), which was closed as out-of-scope in December 2023. In the duplicate #179442 the
extensions maintainer gave the workaround `Developer: Install Extension from Location...`.
The earlier STATUSLOG entry said "recent VS Code versions still pick up manually placed folders";
that was wrong.

### Files changed

| File | Action | Reason |
|---|---|---|
| `README.md` | Installation block rewritten: primary route is `Developer: Install Extension from Location...`; the copy/symlink route is called out as non-working with the issue reference; `.vsix` route notes Node.js ≥ 20 (`@vscode/vsce` 3.9.2 `engines.node`); added `code --extensionDevelopmentPath` for trying without installing | previous instructions did not work |
| `STATUSLOG.md` | this entry | correction record |

Theme files were not changed; they were never the cause.

---

## 2026-09-04 — VS Code themes for all five schemes (`themes/vscode`)

### User prompt (verbatim)

> Could you also make a vscode theme from the pallette? You may make a new directory `theme/vscode`.
> If you want more detailed instruction, ask me some questions.

### Clarifying questions asked and the user's answers

| Question | Answer chosen |
|---|---|
| How much of VS Code to color | **Full workbench** (editor, sidebar, tabs, bars, panels, integrated terminal) |
| How to color code tokens | **Minimal palette syntax**: comments GRAY, strings and keywords one accent each, everything else foreground |
| Software code in file names | **VSC** → `USGC-<THEME NAME>-VSC.json` |
| Location and numbering | **`themes/vscode`** (plural, matching the sibling directories; the prompt said `theme/vscode`), part numbers **5202-010 … 5202-050** mirroring Sublime order |

### Files changed

| File | Action | Reason |
|---|---|---|
| `themes/vscode/package.json` | added | VS Code only loads themes from an extension; this is the manifest (`contributes.themes` lists the five files) |
| `themes/vscode/USGC-{HIGHK,RETICLE,POLYIMIDE,EPITAXY,METALGATE}-VSC.json` | added | the five themes, one per Sublime scheme |
| `README.md` | added `VSC / VS Code` row to the software-code table; added "USGC VS Code Color Themes" section (install steps, settings snippet, 5202 part-number table) | document the new themes, mirroring the Sublime and iTerm sections |
| `.gitignore` | added `*.vsix` | the README install alternative builds a .vsix inside the repo |
| `STATUSLOG.md` | this entry | |

Not changed: Sublime themes, iTerm files, `VERSION`, `pkg`. Nothing was committed.

### Extension manifest facts

- `name` `usgc-themes`, `displayName` `USGC Themes`, `publisher` `usgraphics` (assumed from the GitHub
  org in `pkg`; change if the real Marketplace publisher id differs), `license` `BSD-3-Clause` (from
  `LICENSE`), `engines.vscode` `^1.85.0`.
- `version` is copied from `VERSION` at generation time (1.0.11). `pkg publish` bumps `VERSION` but
  not this file, so it will drift unless updated by hand or `pkg` is extended.
- HIGHK uses `uiTheme: vs` (light base); the other four use `vs-dark`.

### Design rules (Sublime `globals` → VS Code roles)

| Role | Source | Used for |
|---|---|---|
| BG | `background` | every surface: editor, sidebar, tabs, bars, panels, widgets, terminal, menus |
| FG | `foreground` | primary text everywhere, icons, all `symbolIcon.*`, all six bracket-pair colors (so bracket colorization is a visual no-op) |
| ACCENT | `caret` | focus borders, active tab top border, activity-bar indicator, buttons, badges, progress bar, bracket-match border, peek border |
| SEL / SELFG | `selection` / `selection_foreground` | editor and terminal selection, list/quick-pick/menu active rows, banner, prominent status items |
| LINENO / LINENO_ACT | `gutter_foreground` / `gutter_foreground_highlight` | `editorLineNumber.foreground` / `.activeForeground` |
| LINEHL | `line_highlight` | `editor.lineHighlightBackground` and `.lineHighlightBorder`. With `editor.renderLineHighlight: "gutter"` only the line number cell is tinted, matching Sublime; with the default `"all"` the whole line is tinted |
| DIM | GRAY `#999999` | secondary text, inactive tabs, placeholders, comments, whitespace/indent guides, widget borders |
| BORDER | GRAY at alpha 80 | separators between workbench parts |
| INACTIVE_SEL | GRAY at alpha 80 | inactive editor/list/terminal selection (Sublime uses solid GRAY with FL BLUE text, but VS Code cannot recolor inactive-selection text, so a translucent gray keeps FG legible) |
| FIND / FIND_OTHER | FL YELLOW / YELLOW at alpha 99 | current find match (black text) / other matches |
| ERR / WARN / INFO | FL RED / (dark YELLOW, light OLIVE) / per-theme (see below) | diagnostics, icons, status items |
| MOD / ADD / CONFLICT | FL ORANGE / GREEN / (dark FL MAGENTA, light MAGENTA) | git decorations, gutter and overview-ruler diff marks |
| Terminal ANSI | strict palette, identical to the iTerm themes | `terminal.ansi*` |
| Cursor text | BLACK or WHITE by contrast with `caret` | `editorCursor.background`, `terminalCursor.background` |

Alpha is used only on overlay and interaction layers (hover, word/selection highlights, diff tints,
scrollbar sliders, borders). All surfaces and text colors are solid palette values.

### Per-theme accents (hex)

| Theme | FG | STRING | KEYWORD | LINK | INFO | Rationale |
|---|---|---|---|---|---|---|
| HIGHK | 000000 | 660000 MAROON | 000066 BLUE | 0000FF | 0000FF | dark palette variants of HIGHK's own FL RED gutter / FL BLUE caret; FL colors are too weak on white |
| RETICLE | 00A645 | FFBF00 YELLOW | FFFFFF | 00FFFF | 00FFFF | white = caret; amber is the accent RETICLE-IT already uses |
| POLYIMIDE | FFBF00 | 00FFFF | FFFFFF | 00FFFF | 00FFFF | string = its selection_foreground |
| EPITAXY | FF00FF | FFFF00 | FFFFFF | FFFF00 | 00FFFF | string = its selection_foreground; keyword = caret |
| METALGATE | 00FFFF | FFFF00 | FFFFFF | FFFF00 | FF00FF | string = its selection_foreground; caret FL BLUE is illegible on black so keywords are white; INFO avoids the cyan foreground |

Token rules (identical structure in all five, `fontStyle` cleared, no italics):
1. default: FG on BG
2. `comment`, `punctuation.definition.comment` → GRAY
3. `string` → STRING
4. `keyword`, `storage.type`, `storage.modifier` → KEYWORD
5. `keyword.operator` → FG (operators are not treated as keywords)

`semanticHighlighting` is `false` in every theme so language servers cannot add colors.

### Caveats and unverified items

- Not tested inside VS Code: this machine has no `code` binary. Validation done: JSON parses, every
  color key (≈660 per theme) exists in the official theme-color reference fetched 2026-09-04
  (`code.visualstudio.com/api/references/theme-color`), every value is `#RRGGBB` or `#RRGGBBAA`,
  manifest fields are complete.
- `editor.selectionForeground` is documented as "for high contrast"; whether VS Code honors it in
  normal themes is uncertain. If not, selected text keeps its token color (still legible on every
  theme's selection color except RETICLE's white selection with white keywords).
- Markdown headings, bold, links etc. are intentionally unstyled (minimal syntax as chosen).
- Bright ANSI colors on HIGHK's white terminal background have the same weak contrast as in the
  iTerm HIGHK scheme (FL YELLOW 1.07:1, FL CYAN 1.25:1, FL GREEN 1.4:1).

### How to verify / regenerate

- Install per README, then Command Palette → `Developer: Generate Color Theme From Current Settings`
  shows the resolved colors; `Developer: Inspect Editor Tokens and Scopes` shows token rule hits.
- The mapping is fully specified by the tables above; the throwaway generator used this session was
  not committed.

---

## 2026-09-04 — iTerm2 color schemes for HIGHK, POLYIMIDE, EPITAXY, METALGATE

### User prompt (verbatim)

> Please read this repository carefully. Then generate a iterm2 color scheme that matches all the
> sublime text themes (HIGHK, RETICLE, POLYIMIDE, EPITAXY, METALGATE). I can see that RETICLE
> theme is already implemented. If you need any further detailed instructions, please ask me
> question(s).

### Clarifying questions asked and the user's answers

| Question | Answer chosen |
|---|---|
| How to fill the 16 ANSI slots (the Sublime themes only define bg/fg/caret/selection; RETICLE-IT's ANSI slots are hand-picked and not derivable from the palette) | **Strict USGC palette for all four** (see ANSI table below) |
| Part numbers for the new iTerm themes | **Mirror the Sublime numbering**: HIGHK 5201-010, RETICLE 5201-020, POLYIMIDE 5201-030, EPITAXY 5201-040, METALGATE 5201-050 |

### Files changed

| File | Action | Reason |
|---|---|---|
| `themes/iterm/USGC-HIGHK-IT.itermcolors` | added | requested |
| `themes/iterm/USGC-POLYIMIDE-IT.itermcolors` | added | requested |
| `themes/iterm/USGC-EPITAXY-IT.itermcolors` | added | requested |
| `themes/iterm/USGC-METALGATE-IT.itermcolors` | added | requested |
| `README.md` | iTerm "Part Numbers" table now lists all five themes; RETICLE renumbered 5201-010 → 5201-020 per user's choice; descriptions use the same wording as the Sublime table | user chose Sublime-mirrored numbering |
| `README.md` | software-code table: added `IT / iTerm2` row | the iTerm files use the `IT` code but it was undocumented |
| `README.md` | Sublime table typo `Cyan  cheme` → `Cyan scheme` | obvious typo in a table being mirrored |
| `STATUSLOG.md` | created | required by the user's global CLAUDE.md |

Not changed: `themes/iterm/USGC-RETICLE-IT.itermcolors` (user said it is already implemented),
`VERSION` (bumped by `pkg publish`), `pkg`, all Sublime themes, `USGC-PROMPT-TE.txt`. Nothing was
committed.

### Mapping rules used (Sublime `globals` → iTerm2 keys)

All values are the exact hex from the README "Standard colors" table, written in the `sRGB`
color space (see "Color space" below).

| iTerm2 key | Source | Note |
|---|---|---|
| `Background Color` | Sublime `background` | |
| `Foreground Color` | Sublime `foreground` | |
| `Bold Color` | Sublime `foreground` | Sublime themes have no bold concept; only takes effect if the profile's "Use custom bold color" is on |
| `Cursor Color` | Sublime `caret` | |
| `Cursor Text Color` | BLACK or WHITE, whichever has the higher WCAG contrast against `caret` | text under a block cursor must stay readable |
| `Selection Color` | Sublime `selection` | |
| `Selected Text Color` | Sublime `selection_foreground` | |
| `Cursor Guide Color` | Sublime `line_highlight`, alpha 0.0 | alpha 0 = off, same as RETICLE-IT and the README's `highlight_line: false` |
| `Badge Color` | Sublime `gutter_foreground`, alpha 0.5 | closest analogue to a marginal accent; alpha 0.5 is iTerm2's default badge alpha |
| `Link Color` | Sublime `selection_foreground`; HIGHK uses its `caret` (FL BLUE) because its selection_foreground is BLACK, indistinguishable from text | Sublime has no link concept |
| `Match Background Color` | FL YELLOW | find-match highlight; same as RETICLE-IT |
| `Ansi 0..15 Color` | fixed table below, identical in all four files | user's choice "strict USGC palette" |

Keys present are exactly the 27 keys of the existing RETICLE-IT file (verified by script).

### ANSI slot table (identical in HIGHK, POLYIMIDE, EPITAXY, METALGATE)

| Slot | Name | USGC color | Hex | | Slot | Name | USGC color | Hex |
|---|---|---|---|---|---|---|---|---|
| 0 | black | BLACK | 000000 | | 8 | bright black | GRAY | 999999 |
| 1 | red | MAROON | 660000 | | 9 | bright red | FL RED | FF0000 |
| 2 | green | GREEN | 00A645 | | 10 | bright green | FL GREEN | 00FF00 |
| 3 | yellow | OLIVE | 666600 | | 11 | bright yellow | FL YELLOW | FFFF00 |
| 4 | blue | BLUE | 000066 | | 12 | bright blue | FL BLUE | 0000FF |
| 5 | magenta | MAGENTA | 660066 | | 13 | bright magenta | FL MAGENTA | FF00FF |
| 6 | cyan | CYAN | 006666 | | 14 | bright cyan | FL CYAN | 00FFFF |
| 7 | white | GRAY | 999999 | | 15 | bright white | WHITE | FFFFFF |

FL ORANGE and YELLOW (amber) are not in any ANSI slot; they appear only through theme specials.

Known legibility trade-offs of this choice (numbers are WCAG contrast ratios, computed):
- On black backgrounds the dark variants are dim: BLUE 1.2:1, MAROON 1.6:1, MAGENTA 1.8:1,
  CYAN 3.1:1, OLIVE 3.5:1 (GREEN 6.5:1 and GRAY 7.4:1 are fine). The USGC prompt's `setaf 1` dot renders MAROON; `setaf 2` directory
  renders GREEN; `setaf 7` hostname renders GRAY.
- On HIGHK's white background the bright (8-15) slots are poor: FL YELLOW 1.07:1, FL CYAN 1.25:1,
  FL GREEN 1.4:1 (GRAY 2.9:1, FL RED 4.0:1). Slot 15 WHITE is invisible on white, as in most light schemes.

### Per-theme special colors (hex)

| Key | HIGHK | POLYIMIDE | EPITAXY | METALGATE |
|---|---|---|---|---|
| Background | FFFFFF | 000000 | 000000 | 000000 |
| Foreground / Bold | 000000 | FFBF00 | FF00FF | 00FFFF |
| Cursor | 0000FF | 00A645 | FFFFFF | 0000FF |
| Cursor Text | FFFFFF | 000000 | 000000 | FFFFFF |
| Selection | 00FF00 | 000066 | 000066 | 666600 |
| Selected Text | 000000 | 00FFFF | FFFF00 | FFFF00 |
| Cursor Guide (α 0) | 00FF00 | 0000FF | FFFF00 | 0000FF |
| Badge (α 0.5) | FF0000 | FF6600 | 0000FF | FFFF00 |
| Link | 0000FF | 00FFFF | FFFF00 | FFFF00 |
| Match Background | FFFF00 | FFFF00 | FFFF00 | FFFF00 |

### Color space

RETICLE-IT stores colors as Display P3 floats (written by the macOS color picker). The four new
files use `Color Space = sRGB` with components = hex/255, so every value equals the Sublime hex
exactly and can be audited by eye. iTerm2 renders both spaces correctly; sRGB has been accepted
since well before P3 support was added.

### Observations about the existing RETICLE-IT (not modified)

Decoded from P3 to sRGB for reference. It is hand-tuned, not a strict palette mapping:
- Foreground ≈ 009D5F (palette GREEN is 00A645); Selection ≈ 000581 (BLUE is 000066);
  Selected Text ≈ FFC200 (YELLOW is FFBF00); Cursor 858E97 gray; Bold 75767C gray.
- ANSI: 0 = 262626, 1/9 = E00000, 2/3/11 = FFC200, 10 = F4BA00, 4 = 723DF9, 12 = FF7321,
  5/13 = FF208F, 6/14 = 0079FF, 7 = FFFFFF, 8 = 494747, 15 = FEFEFF.
- The README screenshot of RETICLE-IT shows ANSI slot 4 (blue) as orange, but the committed file
  has violet-blue 723DF9 in slot 4 and orange only in slot 12. The screenshot was therefore taken
  from a profile that differs from the committed file.

### How to verify / regenerate

- Import: iTerm2 → Settings → Profiles → Colors → Color Presets… → Import… → pick the file.
- Structural check (Linux/macOS): `python3 -c "import plistlib,sys;print(sorted(plistlib.load(open(sys.argv[1],'rb'))))" themes/iterm/USGC-HIGHK-IT.itermcolors`
- Regeneration is fully specified by the tables above; the throwaway generator used this session
  was not committed.
