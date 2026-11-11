# Abtal Math (أبطال الجمع والطرح)

Arabic RTL math practice app for grade 2 (Saudi curriculum). The whole app is one file, `index.html`, published by GitHub Pages from `main` at https://mafia3001.github.io/abtal-math/.

## Publishing rule
The owner wants every change live right away: commit and push straight to `main` (no feature branch, no pull request) unless they ask otherwise. Pages redeploys in about a minute.

## Adding a lesson
The owner usually sends photos of a textbook page. Match the book's method, wording and lesson number.

1. **Generator** — add a function to the `G` object that returns `{op:'+'|'-', nums:[...]}`. Keep every result between 0 and 99 so it fits the tens/ones table.
2. **Lesson card** — add an entry to `LEVELS` (before the `mix` entry): `id` (same key as in `G`), `g` (index into `GROUPS`, the chapter heading on the home screen), `kind` (`add`/`sub`), `name`, `sub` (the lesson idea in one line), `tag` (book lesson number in Arabic digits, e.g. `'٥-١٠'`, omit if unknown), `ex` (sample problem), `helpers` (true when the lesson teaches regrouping, so the small carry/borrow boxes show), optional `hint` (the strategy line under the problem).
3. **Mixed challenge** — automatic: `mix` draws from every lesson in `LEVELS`.
4. **Explanation** — a generator can tag its problem with `m:'<method>'`; `steps(p)` then uses `SPECIAL[m]` (number line, make ten, related facts, etc.). Otherwise `steps(p)` builds the step-by-step walkthrough shown after a wrong answer. Reuse it if the method is the same; extend it if the book teaches a different method (e.g. a tip like "ابحث عن عددين مجموعهما ١٠").
5. Update the lessons table in `README.md`.

If a new lesson needs something the table can't show (hundreds, word problems, comparing numbers), ask the owner before changing the layout.

## Source book
The owner's textbook is Saudi Grade 2 Math, semester 1 (1446). A text conversion of the PDF is mostly unreadable (the Arabic font exports as glyph codes), so lesson numbers are only known for chapter 5 (from photos). Lessons not yet in the app and waiting on the owner's go-ahead because they need a different screen: data (tally, pictographs, bar graphs), probability (certain/impossible, more/less likely), estimating sums and differences by rounding to the nearest ten, and word-problem strategy lessons.

## Question types
- Default (no `type`): an operation in the tens/ones table, built from `op` and `nums`.
- `type:'num'`: the child writes one number (`answer`) in a tens/ones answer row. `title` is the instruction and `show` is HTML above the table (blocks, number words, a sequence via `seqHTML`).
- `type:'choice'`: tap one of `choices` (HTML strings); `correct` is the right index. Used for comparing (`relHTML`) and estimating.
Comparison symbols are written logically (`a > b`) inside RTL text, so the browser mirrors them and the open side always faces the larger number. Keep them inside `dir="rtl"`.

## Conventions
- All text Arabic, formal-simple wording for children, first person like the book (أجمع، أطرح، أعيد التجميع).
- Show numbers with Arabic-Indic digits via `ar()`. Minus sign is `−` (U+2212).
- Colors: green = آحاد, orange = عشرات (matches the book). Use the CSS tokens; keep light and dark themes working.
- Points: 10 per correct answer, +2 for correct regrouping boxes, +5 every 3 in a row. Don't change scoring unless asked.

## Before pushing
Open the page in headless Chromium at ~400px width, play the new lesson once with a correct answer and once with a wrong one, and confirm there are no console errors.
