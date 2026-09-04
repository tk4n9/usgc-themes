# STATUSLOG

Chronological log of changes to this repository, kept so that any agent or person can pick up the
work without re-deriving decisions. Newest entry first. Dates are absolute (YYYY-MM-DD).

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
