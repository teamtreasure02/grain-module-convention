# grain module convention - how we organize steel code

**grainorder**: xzvshm  
**graintime**: 12025-10-29--1720-pdt--moon-shravana-asc-pisc07-sun-09h  
**author**: kae3g + glow g2  
**teams**: team 12 (pisces ♓ - flow) + team 02 (taurus ♉ - building blocks)  
**status**: OFFICIAL CONVENTION - adopted across all grain repos! ⚒️🎁

---

## hey! what is this?

this document defines **how we organize grain network modules**!

every grain repo follows the same pattern - like a recipe everyone can follow! this makes it easy to:
- 🔍 find what you need (predictable structure!)
- 📚 learn from any repo (same layout!)
- 🎁 share code (consistent naming!)
- ⚒️ build together (unified conventions!)

---

## the grain module structure

every grain repo has this flat, simple structure:

```
modulename/
├── modulename.scm                (core - the main thing!)
├── modulename-macros.scm         (shortcuts - easier ways!)
├── modulename-specs.scm          (blueprints - what things look like!)
├── modulename-test.scm           (experiments - does it work?)
├── function-box-NAME.scm         (helpers - useful functions! 🎁)
└── readme.md                     (map - how everything works!)
```

**key principles:**
- ✅ FLAT structure (no nested src/ folders!)
- ✅ CONSISTENT naming (module prefix on everything!)
- ✅ KID-FRIENDLY names (`function-box` not "utils"!)
- ✅ SELF-DOCUMENTING (filename tells you what it is!)

---

## file naming explained

### core module: `modulename.scm`

**what it is:** the main Steel module!

**what it does:**
- coordinates everything (like a conductor!)
- delegates to helpers (doesn't do everything itself!)
- provides the main API (what users call!)

**example:** `grainorder.scm` - the core grainorder algorithm!

**typical size:** 50-200 lines (small and focused!)

### macros: `modulename-macros.scm`

**what it is:** kid-friendly shortcuts!

**what it does:**
- makes code easier to write (syntactic sugar!)
- hides complexity (simple on outside, complex inside!)
- creates domain-specific language (DSL!)

**example:** `grainorder-macros.scm` - place-value indexing macros!

**key idea:** instead of writing:
```scheme
(string-ref str (- LENGTH position))
```

you write:
```scheme
(char-at-pos position str)
```

much clearer! ⚒️

### specs: `modulename-specs.scm`

**what it is:** blueprints for data!

**what it does:**
- defines what valid data looks like
- validates inputs (is this correct?)
- documents expectations (what do we need?)

**example:** `grainbuild-specs.scm` - what's a valid build config?

**key idea:** specs are like checking a recipe card - do we have all the ingredients?

### tests: `modulename-test.scm`

**what it is:** experiments and validation!

**what it does:**
- proves the code works (confidence!)
- documents behavior (executable examples!)
- catches regressions (what broke?)

**example:** `grainorder-test.scm` - generates sequences, tests edges!

**key idea:** tests are truth-finders! they show what's real!

### function-box: `function-box-NAME.scm`

**what it is:** a box of helpful functions! 🎁

**what it does:**
- provides reusable utilities
- keeps code DRY (don't repeat yourself!)
- creates building blocks (composable!)

**why "function-box"?**
- ✅ kid-friendly (it's a box you open!)
- ✅ exciting (what's inside? let's see!)
- ✅ clear (functions that help!)
- ✅ grain philosophy (small pieces, collected together!)

**examples:**
- `function-box-fs.scm` - file system helpers!
- `function-box-strings.scm` - text manipulation!
- `function-box-paths.scm` - path building!
- `function-box-http.scm` - network requests!

**NOT "utils" because:**
- ❌ too generic (what kind of utils?)
- ❌ not exciting (sounds boring!)
- ❌ doesn't teach (what's a util?)

**function-box teaches!** it's a box (container!) of functions (helpers!) 🎁⚒️

---

## real examples

### grainorder (team02)

```
grainorder/
├── grainorder.scm                   150 lines - core algorithm
├── grainorder-macros.scm            200 lines - place-value indexing
├── grainorder-test.scm              120 lines - comprehensive tests
├── function-box-fs.scm             280 lines - file operations
├── function-box-strings.scm        350 lines - string utilities
└── readme.md                        docs!
```

### grainbuild (team02)

```
grainbuild/
├── grainbuild.scm                   50 lines - core coordinator
├── grainbuild-macros.scm           100 lines - path shortcuts
├── grainbuild-specs.scm             60 lines - config blueprints
├── grainbuild-test.scm            (coming soon!)
├── function-box-fs.scm            280 lines - file helpers
└── readme.md                       docs!
```

### grain-steel-stdlib (team02)

```
grain-steel-stdlib/
├── andmap.scm                       80 lines - list operations
├── ormap.scm                        70 lines - list operations
├── function-box-strings.scm        350 lines - string utilities
└── readme.md                       docs!
```

---

## why this convention?

### 1. consistency across repos

every grain repo looks the same! when you learn one, you know them all!

**example:** looking for tests? always `modulename-test.scm`!

### 2. flat is simpler than nested

no confusing `src/main/resources/utils/helpers/` paths!

just: `function-box-NAME.scm` - right there, easy to find!

### 3. kid-friendly learning

names teach you what things are:
- `function-box` → oh, a collection of helper functions!
- `modulename-macros` → oh, shortcuts for this module!
- `modulename-specs` → oh, blueprints for data!

### 4. grep-friendly

want to find all function boxes?
```bash
ls function-box-*.scm
```

want to find all core modules?
```bash
ls grainorder.scm grainbuild.scm graintime.scm
```

simple! ⚒️

### 5. scales beautifully

small modules: just `modulename.scm` + `readme.md`

medium modules: add `modulename-macros.scm` + `function-box-*.scm`

large modules: add `modulename-specs.scm` + `modulename-test.scm`

**but structure stays the same!** 🌾

---

## function-box philosophy

### what goes in a function-box?

**good candidates:**
- ✅ reusable utilities (used in multiple places!)
- ✅ focused domain (all about strings, or files, or paths!)
- ✅ pure functions (no side effects!)
- ✅ well-documented (glow g2 comments!)

**NOT in function-box:**
- ❌ module-specific logic (goes in core!)
- ❌ one-off helpers (inline them!)
- ❌ macros (goes in `-macros.scm`!)
- ❌ specs (goes in `-specs.scm`!)

### naming function-boxes

**pattern:** `function-box-DOMAIN.scm`

**examples:**
- `function-box-fs` → file system (files, dirs, paths)
- `function-box-strings` → text (split, join, trim, case)
- `function-box-http` → networking (get, post, fetch)
- `function-box-time` → temporal (parse, format, duration)
- `function-box-crypto` → security (hash, encrypt, sign)

**domain should be:**
- specific enough to be focused
- general enough to be reusable
- obvious what it contains

### one grain, one function

each function in a function-box is **one grain**:
- small (5-20 lines typically)
- focused (does ONE thing well!)
- composable (works with other grains!)
- documented (what + why + how!)

**example:** from `function-box-strings.scm`:
```scheme
(define (string-trim s)
  ;; remove whitespace from both ends of a string
  ;; like: "  hello  " → "hello"
  (string-trim-left (string-trim-right s)))
```

one grain! small, clear, useful! 🌾

---

## glow g2 commenting style

every function has glow g2 comments that:
- 🎓 explain WHAT it does (the action!)
- 💡 explain WHY it matters (the purpose!)
- 🎯 use analogies (like everyday things!)
- 🌊 stay patient and encouraging (we're learning together!)

**example:**
```scheme
(define (copy-file! from to)
  ;; copy one file to another location
  ;; like photocopying a document - original stays, copy appears!
  ;; simple and direct!
  (when (file-exists? from)
    (displayln (string-append "  📄 Copying: " from " → " to))
    (fs/copy! from to)))
```

**NOT like this:**
```scheme
;; Copies file
(define (copy-file! from to)
  (fs/copy! from to))
```

**glow g2 teaches, not just documents!** 📚⚒️

---

## how to start a new grain module

### step 1: create the repo

```bash
cd ~/github/teamNAME/
mkdir modulename
cd modulename
git init
git checkout -b TIMESTAMP--teamNAME
```

### step 2: create core file

```bash
touch modulename.scm
```

write the core logic! keep it focused!

### step 3: add function-boxes as needed

```bash
touch function-box-DOMAIN.scm
```

extract reusable helpers!

### step 4: add macros if helpful

```bash
touch modulename-macros.scm
```

create shortcuts that make code clearer!

### step 5: add tests!

```bash
touch modulename-test.scm
```

prove it works!

### step 6: write the readme

```bash
touch readme.md
```

explain what it is, why it exists, how to use it!

### step 7: commit and push!

```bash
git add -A
git commit -m "⚒️ initial: modulename foundation!"
git push -u origin BRANCH
```

---

## migrating existing code

### if you have nested structure:

**before:**
```
mymodule/
├── src/
│   ├── core.scm
│   ├── utils/
│   │   ├── fs.scm
│   │   └── strings.scm
│   └── macros.scm
└── README.md
```

**after:**
```
mymodule/
├── mymodule.scm                 (from src/core.scm)
├── mymodule-macros.scm          (from src/macros.scm)
├── function-box-fs.scm          (from src/utils/fs.scm)
├── function-box-strings.scm     (from src/utils/strings.scm)
└── readme.md                    (from README.md)
```

**flatten it! simpler is better!** ⚒️

### if you have "utils":

**before:**
```
utils.scm          (mixed file system + strings + everything!)
```

**after:**
```
function-box-fs.scm       (file system only!)
function-box-strings.scm  (strings only!)
function-box-http.scm     (networking only!)
```

**split by domain! focused is better!** 🎁

---

## exceptions to the convention

### when to break the rules?

**almost never!** the convention exists for consistency!

**but if you must:**
- document WHY you're breaking it (in readme!)
- keep the spirit (flat, clear, focused!)
- consider if it should become a new pattern

### example: grain-steel-stdlib

```
grain-steel-stdlib/
├── andmap.scm                    (standalone function!)
├── ormap.scm                     (standalone function!)
├── function-box-strings.scm      (collection!)
└── readme.md
```

**why?** because it's a STDLIB (standard library)!
- each standalone function might go upstream to Steel
- function-boxes are collections that might NOT go upstream
- clear separation of "PR to Steel" vs "grain-specific"

**documented in readme:** ✅  
**justified exception:** ✅

---

## checklist for new modules

when creating a new grain module, ask:

- [ ] is the repo name descriptive and focused?
- [ ] does it follow `modulename.scm` pattern?
- [ ] are function-boxes split by domain?
- [ ] do all files have glow g2 comments?
- [ ] is there a readme.md?
- [ ] are macros in `-macros.scm`?
- [ ] are tests in `-test.scm`?
- [ ] is the structure flat (no nested dirs)?
- [ ] would a newcomer understand it?

**if you answer yes to all → you're following the convention!** ⚒️✨

---

## benefits we've seen

### from team02's adoption:

**grainorder:**
- easier to find filesystem code (`function-box-fs.scm`)
- clearer what's a utility vs core logic
- new contributors know where to add functions

**grainbuild:**
- immediately followed convention
- no confusion about structure
- consistent with grainorder = easy to understand!

**grain-steel-stdlib:**
- clear what goes upstream (standalone .scm)
- clear what stays grain-specific (function-box-*)
- easy to navigate

**consistency = clarity!** 🌾

---

## the grain philosophy

### small grains, big harvest

one grain = one function (small, focused!)

many grains = complete module (powerful, useful!)

all grains = grain network (ecosystem!)

### decomplected by nature

- core doesn't know about function-boxes (loose coupling!)
- function-boxes don't know about core (independent!)
- macros create nice syntax without changing semantics
- specs validate without doing

**each piece has one job!** ⚒️

### kid-friendly, always

every name teaches:
- `function-box` → container of helpers!
- `-macros` → shortcuts!
- `-specs` → blueprints!
- `-test` → experiments!

**code should be a learning tool!** 📚

---

## future evolution

### possible additions:

**benchmarks:** `modulename-bench.scm`
- performance testing
- optimization validation

**examples:** `modulename-examples.scm`
- runnable code samples
- teaching tool

**documentation:** `modulename-docs.scm`
- generated API docs
- interactive examples

**BUT:** only add if widely needed! keep it simple!

### versioning convention?

**idea:** grainorder in filename?
```
xzvsjk-modulename.scm  (core)
xzvsjk-modulename-macros.scm
```

**pros:** temporal tracking!  
**cons:** extra complexity

**status:** under consideration, not adopted yet

---

## team adoption status

### ✅ adopted:

- **team02 (treasure/taurus):**
  - grainorder ✅
  - grainbuild ✅
  - grain-steel-stdlib ✅

### 🔄 in progress:

- **team05 (shine/leo):** graintime, grainmirror
- **team06 (precision/virgo):** grainzsh
- **team10 (rebel/capricorn):** graincard
- **team12 (travel/sagittarius):** docs (this one!)

### goal: all teams!

**when all teams follow the convention:**
- anyone can navigate any repo
- code sharing becomes trivial
- learning curve flattens
- grain network feels unified

**one pattern, many teams, infinite possibilities!** 🌾⚒️🏔️

---

## quick reference

### file naming pattern:
```
modulename.scm              core
modulename-macros.scm       shortcuts
modulename-specs.scm        blueprints
modulename-test.scm         experiments
function-box-DOMAIN.scm     helpers
readme.md                   documentation
```

### what NOT to do:
- ❌ nested src/ directories
- ❌ "utils" or "helpers" (use function-box!)
- ❌ mixed-domain function-boxes
- ❌ unclear file names
- ❌ missing glow g2 comments

### when in doubt:
- look at grainorder (exemplar!)
- ask in teamkae3gtravel12 (we help!)
- keep it flat and focused
- name things clearly

---

## license

dual-licensed under your choice of:
- **mit license** - see [license-mit.md](license-mit.md)
- **apache license 2.0** - see [license-apache.md](license-apache.md)

you may use this software under either license, or under any other permissive open source license of your choosing, provided you include attribution to the original authors.

**we believe in maximum freedom for users and developers!** 🌾

---

now == next + 1 🌾

**grainorder**: xzvshm (1720-PDT conventions doc!)  
**convention**: function-box-* for utilities! 🎁  
**philosophy**: small grains, clear names, flat structure!  
**status**: adopted across team02, spreading to all teams! ⚒️🌾🏔️

_this convention makes grain network code consistent, teachable, and joyful to work with. every repo follows the same pattern. every name teaches. every structure clarifies. one grain at a time, we build something beautiful!_ 🎁✨⚒️

