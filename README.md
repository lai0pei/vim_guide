# Vim Field Guide

A single-file, searchable reference to **633 Vim commands in 30 groups**, compiled from the official
Vim help files. Each row reads **command first, description second**, aligned in a left-hand column
so the page scans like a reference table; search matches both, so commands can also be found by what
they do.

The page carries its own favicon (an inline SVG — still one file, nothing to upload).

**Every command carries a worked example.** All 633 have a before/after card: a sample line before the
command, the same line after, with the affected text highlighted and the cursor position marked.

No build step, no dependencies, no network calls. One `index.html`.

## Use it

```sh
xdg-open index.html      # Linux
open index.html          # macOS
```

| Action | How |
| --- | --- |
| Search everything | press <kbd>/</kbd>, or click the search box |
| Clear the search | <kbd>Esc</kbd> |
| See a command work | hover a row for a floating card, or click the row to pin the demo under it |
| Open the documentation | click the **?** at the end of any row |
| Collapse a group | click its heading; **collapse all** reduces the page to an index |
| Regroup | **by function** / **by frequency** in the header (remembered) |
| Light / dark theme | the **◐** button (remembered between visits) |
| Print | prints in two columns on a light background, without the interface |

Search matches the keys *and* the description, so concept words work:
`macro`, `register`, `split`, `fold`, `quickfix`, `sudo`, `clipboard`, `replace`, `remote`.

### Demos

Hovering a row displays a floating before/after card. Clicking the row opens the example inline
beneath it, where it stays until clicked again; several may be open at once.

### Official documentation

Every row ends with a **?** linking to that exact command on [vimhelp.org](https://vimhelp.org) —
the official help text, at the right anchor, not a search. The targets were generated from Vim's own
`tags` file, so all 633 point at a real help tag (the same one `:help <tag>` opens locally). The tag
is shown in the hover card, and in the link's tooltip.

### Two groupings

| Grouping | What it gives you |
| --- | --- |
| **by function** (default) | the 30 topic groups — movement, editing, registers, quickfix… ordered most useful first |
| **by frequency** | **Essential** (105) → **Daily use** (271) → **Rare** (257); each row keeps a tag showing which function group it came from |

*By function* suits lookup; *by frequency* suits working through the material in order.

## Layout

The list fills as many ~470px columns as the window allows, with no upper cap — 1 on a phone,
2 on a laptop, 3 at 1920px, 5 at 1440p, 7 on a 4K monitor.

Each group is placed **whole** into whichever column is shortest at that moment, so a heading always
sits at the top of its block and a group is never cut in half across a column break. The columns are
re-balanced when the window is resized and when the demo mode changes, since inline demos multiply
the heights.

## Host it on GitHub Pages

```sh
git init
git add index.html README.md
git commit -m "Vim Field Guide"
git branch -M main
git remote add origin git@github.com:<you>/vim-field-guide.git
git push -u origin main
```

Then: **Settings → Pages → Source: Deploy from a branch → `main` / `/ (root)` → Save.**
It goes live at `https://<you>.github.io/vim-field-guide/` within a minute or two.

## Groups, in order

1. Modes & Survival — 2. Motions — 3. Text Objects — 4. Editing (operators) — 5. Registers & Clipboard —
6. Search & Replace — 7. Ranges, `:global` & `:normal` — 8. Insert Mode Power — 9. Visual Mode —
10. Files, Buffers & Arguments — 11. Windows & Tabs — 12. Marks & Jumps — 13. Macros —
14. Undo & Time Travel — 15. Code Navigation (tags, quickfix, grep) — 16. Folding — 17. Diff —
18. Terminal & Shell — 19. Indent & Format — 20. Options Worth Knowing — 21. Mappings —
22. Autocommands — 23. File Browsing, Archives & Remote — 24. Bundled Plugins & Packages —
25. Spelling — 26. Sessions & Views — 27. Vimscript Essentials — 28. Command-Line Tricks —
29. Sysadmin & Big-File Survival — 30. Lesser-Known Gems

## Suggested use

Select **by frequency**, take the **Essential** group first, and work through it with the examples
open. Groups 1–7 of the functional view account for the majority of routine editing; groups 15, 20
and 29 are the ones that most affect a Linux workflow.

## Accuracy

Every entry resolves to a real tag in Vim's own `tags` file — all 633 — so the **?** links land on the
correct help section rather than a search page. Sixty entries, chosen as the ones most easily got
wrong, were then checked line by line against the help text itself: 57 were exact and 4 corrections
were made (`gm`, `zug`/`zuw`, and the help targets for blockwise `d` and `//`).

The remaining descriptions are paraphrases of the official help and have not been individually
verified against it. The worked examples are written illustrations of each command's behaviour, not
captured Vim output. Anything that looks wrong can be checked in one keystroke with the **?** link
or locally with `:help <tag>`.

## Editing the content

Entries live in a `SECTIONS` array inside the `<script>` block of `index.html`:

```js
{id:'motion', title:'Motions — Moving Precisely', icon:'➜', note:'…', items:[
  ['w / W', 'Next word start / WORD start', 'daily'],
  //  keys    explanation                    daily | weekly | occasional | rare
]}
```

Demos live in a second object, `DEMOS`, keyed by `"sectionId::exact key text"`:

```js
"objects::ci\"": ["title = \"old ti‸tle\";", "title = \"«new»‸\";", "caption under the card"],
//                 before                     after                  ‸ = cursor, «…» = what changed
```

Add a row, reload the page — counts, groups and the search index update themselves.

## Credits

Content distilled from the Vim help files (`usr_*.txt`, `quickref.txt`, `index.txt`, `motion.txt`,
`change.txt`, `pattern.txt`, `options.txt`, `quickfix.txt` and friends). Vim is by Bram Moolenaar
and contributors — [vim.org](https://www.vim.org/), Vim licence (charityware).
