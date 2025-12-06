# IntelliJ IDEA - Keyboard Productivity Guide

A guide to IntelliJ IDEA for developers who want to maximize keyboard use and eliminate mouse usage.

## Mouse-Free Work Philosophy

**Why keyboard-first?**
- Speed - no interruption to flow from reaching for the mouse
- Precision - accurate operations without clicking
- Productivity - less fatigue, more code
- Flow state - maintaining concentration

**Goal:** 95%+ operations without mouse

## Basic Shortcuts (Must Know)

### Universal Navigation

| Shortcut | Action | Description |
|-------|-------|------|
| `Shift Shift` | **Search Everywhere** | Most important shortcut! Search anything |
| `Ctrl+Shift+A` | Find Action | Find any action/command |
| `Ctrl+N` | Go to Class | Open class by name |
| `Ctrl+Shift+N` | Go to File | Open file by name |
| `Ctrl+Alt+Shift+N` | Go to Symbol | Find method/field |
| `Ctrl+E` | Recent Files | Recently opened files |
| `Ctrl+Shift+E` | Recent Locations | Recently edited locations |

**Protip:** `Shift Shift` replaces 90% of mouse navigation!

### Code Navigation

| Shortcut | Action |
|-------|-------|
| `Ctrl+B` or `Ctrl+Click` | Go to Declaration |
| `Ctrl+Alt+B` | Go to Implementation |
| `Ctrl+U` | Go to Super Method/Class |
| `Ctrl+Shift+B` | Go to Type Declaration |
| `Ctrl+G` | Go to Line |
| `Alt+←/→` | Previous/Next location |
| `Ctrl+[/]` | Jump to beginning/end of block |
| `Ctrl+F12` | File Structure (methods in class) |
| `Alt+↑/↓` | Previous/Next method |

### Code Editing

| Shortcut | Action |
|-------|-------|
| `Ctrl+Space` | Basic code completion |
| `Ctrl+Shift+Space` | Smart code completion |
| `Ctrl+Shift+Enter` | Complete Statement |
| `Alt+Insert` | Generate (getters, constructors, etc.) |
| `Ctrl+O` | Override Methods |
| `Ctrl+I` | Implement Methods |
| `Ctrl+Alt+T` | Surround With (try-catch, if, etc.) |
| `Ctrl+/` | Comment/Uncomment line |
| `Ctrl+Shift+/` | Comment/Uncomment block |
| `Ctrl+D` | Duplicate line/selection |
| `Ctrl+Y` | Delete line |
| `Ctrl+Shift+U` | Toggle case |
| `Ctrl+W` | Expand selection |
| `Ctrl+Shift+W` | Shrink selection |

### Refactoring

| Shortcut | Action |
|-------|-------|
| `Shift+F6` | Rename |
| `Ctrl+Alt+M` | Extract Method |
| `Ctrl+Alt+V` | Extract Variable |
| `Ctrl+Alt+F` | Extract Field |
| `Ctrl+Alt+C` | Extract Constant |
| `Ctrl+Alt+P` | Extract Parameter |
| `Ctrl+F6` | Change Signature |
| `F6` | Move |
| `F5` | Copy |
| `Alt+Delete` | Safe Delete |
| `Ctrl+Shift+F6` | Refactor This (menu) |

### Running & Debugging

| Shortcut | Action |
|-------|-------|
| `Shift+F10` | Run |
| `Shift+F9` | Debug |
| `Ctrl+Shift+F10` | Run context configuration |
| `Ctrl+F2` | Stop |
| `F8` | Step Over |
| `F7` | Step Into |
| `Shift+F7` | Smart Step Into |
| `Shift+F8` | Step Out |
| `Alt+F9` | Run to Cursor |
| `F9` | Resume Program |
| `Ctrl+F8` | Toggle Breakpoint |
| `Ctrl+Shift+F8` | View Breakpoints |
| `Alt+F8` | Evaluate Expression |

## Advanced Shortcuts

### Multi-Cursor & Selection

| Shortcut | Action |
|-------|-------|
| `Alt+J` | Add Selection for Next Occurrence |
| `Alt+Shift+J` | Unselect Occurrence |
| `Ctrl+Alt+Shift+J` | Select All Occurrences |
| `Alt+Shift+Insert` | Column Selection Mode |
| `Alt+Shift+Click` | Add/Remove Caret |
| `Ctrl+Alt+Shift+Click` | Create Rectangular Selection |
| `Esc` | Remove All Carets |

**Example workflow:**
1. Select a variable
2. `Alt+J` several times (selects next occurrences)
3. Type - all occurrences will change

### Live Templates

| Shortcut | Template | Expansion |
|-------|----------|-------------|
| `psvm` + `Tab` | `public static void main` | Main method |
| `sout` + `Tab` | `System.out.println()` | Print |
| `fori` + `Tab` | `for (int i = 0; i < ; i++)` | For loop |
| `iter` + `Tab` | `for (Type item : collection)` | For-each |
| `ifn` + `Tab` | `if (x == null)` | Null check |
| `inn` + `Tab` | `if (x != null)` | Not null check |

**Create your own!** `Ctrl+Alt+S` → Live Templates

### Code Analysis & Fixing

| Shortcut | Action |
|-------|-------|
| `Alt+Enter` | **Show Intention Actions** (most important!) |
| `Ctrl+F1` | Show Error Description |
| `F2` | Next Highlighted Error |
| `Shift+F2` | Previous Highlighted Error |
| `Ctrl+Alt+Shift+I` | Run Inspection by Name |
| `Ctrl+Alt+L` | Reformat Code |
| `Ctrl+Alt+O` | Optimize Imports |

**Protip:** `Alt+Enter` is the magic solution to most problems!

### VCS / Git Integration

| Shortcut | Action |
|-------|-------|
| `Alt+~` | VCS Operations Menu |
| `Ctrl+K` | Commit |
| `Ctrl+Shift+K` | Push |
| `Ctrl+T` | Update Project (Pull) |
| `Alt+Shift+C` | View Recent Changes |
| `Ctrl+Alt+Z` | Revert Changes |
| `Alt+9` | Version Control Tool Window |
| `Ctrl+D` | Show Diff |

### Window Management

| Shortcut | Action |
|-------|-------|
| `Alt+1` | Project Tool Window |
| `Alt+2` | Favorites |
| `Alt+3` | Find Tool Window |
| `Alt+4` | Run Tool Window |
| `Alt+5` | Debug Tool Window |
| `Alt+6` | Problems |
| `Alt+7` | Structure |
| `Alt+9` | Git |
| `Shift+Esc` | Hide Active Tool Window |
| `Ctrl+Shift+F12` | Hide All Tool Windows |
| `Ctrl+Tab` | Switcher |
| `Alt+F12` | Terminal |

## Mouse-Free Workflow

### 1. Opening Files

```
❌ Mouse: Clicking in Project Explorer
✅ Keyboard:
   1. Ctrl+N → type class name
   2. Ctrl+Shift+N → type file name
   3. Shift Shift → type anything
   4. Ctrl+E → select from recent
```

### 2. Code Navigation

```
❌ Mouse: Scrolling and clicking
✅ Keyboard:
   1. Ctrl+F12 → file structure → select method
   2. Ctrl+Alt+Shift+N → type method name
   3. Ctrl+B → go to definition
   4. Alt+←/→ → previous/next location
```

### 3. Refactoring

```
❌ Mouse: Right click → Refactor → select
✅ Keyboard:
   1. Select code: Ctrl+W (expand selection)
   2. Shift+F6 → rename
   3. Ctrl+Alt+M → extract method
   4. Alt+Enter → quick fixes
```

### 4. Running Tests

```
❌ Mouse: Click on green arrow
✅ Keyboard:
   1. Ctrl+Shift+F10 → run context (test/main)
   2. Shift+F10 → re-run last
   3. Ctrl+Shift+F9 → re-compile and run
```

### 5. Debugging

```
❌ Mouse: Clicking in gutter, Debug menu
✅ Keyboard:
   1. Ctrl+F8 → toggle breakpoint
   2. Shift+F9 → start debug
   3. F8 → step over
   4. F7 → step into
   5. Alt+F8 → evaluate expression
```

### 6. Git Operations

```
❌ Mouse: Clicking in VCS menu
✅ Keyboard:
   1. Alt+~ → VCS menu
   2. Ctrl+K → commit
   3. Ctrl+Shift+K → push
   4. Ctrl+T → update/pull
```

## Practical Scenarios

### Scenario 1: Implementing a New Method

```
1. Ctrl+N → Open class
2. Ctrl+F12 → Find place for method
3. Ctrl+O → Override or Alt+Insert → Generate
4. Ctrl+Space → Code completion
5. Ctrl+Alt+T → Surround with try-catch
6. Ctrl+Alt+L → Reformat
7. Ctrl+Shift+F10 → Run test
```

### Scenario 2: Refactor Legacy Code

```
1. Ctrl+Alt+Shift+N → Find method by name
2. Ctrl+W (several times) → Select entire block
3. Ctrl+Alt+M → Extract method
4. Shift+F6 → Rename method
5. Alt+Enter → Resolve warnings
6. F2 → Go to next error
7. Alt+Enter → Fix it
8. Ctrl+K → Commit
```

### Scenario 3: Fix Bug

```
1. Ctrl+Shift+F → Find in files "problematic code"
2. Ctrl+B → Go to usage
3. Ctrl+Alt+F7 → Show usages
4. Ctrl+Alt+H → Call hierarchy
5. Ctrl+F8 → Toggle breakpoint
6. Shift+F9 → Debug
7. F8/F7 → Step through
8. Alt+F8 → Evaluate expression
9. Fix code
10. Shift+F10 → Run tests
```

### Scenario 4: Code Review in IDE

```
1. Alt+9 → Open Git tool window
2. Ctrl+D → Show diff
3. F7 → Next change
4. Shift+F7 → Previous change
5. Ctrl+Z → Revert unwanted changes
6. Ctrl+/ → Add review comment
7. Ctrl+K → Commit review comments
```

## Tips & Tricks

### 1. Search Everywhere Mastery

`Shift Shift` then:
- Don't type anything → recent files
- `/` → files only
- `#` → classes only
- `@` → symbols only (methods)
- `:` → line (go to line)

**Example:**
- `Shift Shift` → `UserService` → open class
- `Shift Shift` → `/application.yml` → open config
- `Shift Shift` → `@findUser` → jump to method

### 2. Multi-Cursor Power

```java
// You have:
String name;
String email;
String phone;

// You want to add "private" before each
// 1. Select "String" in first line
// 2. Alt+J, Alt+J (select all)
// 3. Home (beginning of line)
// 4. Type "private "
// Done!

private String name;
private String email;
private String phone;
```

### 3. Clipboard History

`Ctrl+Shift+V` → See clipboard history (last 5 copies)

### 4. Postfix Completion

Instead of wrapping code, use postfix:

```java
// Type:
user.null
// Tab → automatically:
if (user == null) {}

// Type:
list.for
// Tab → automatically:
for (String item : list) {}

// Others:
.var → assign to variable
.return → return statement
.sout → System.out.println()
.notnull → if != null
```

### 5. CamelHumps

Enable "CamelHumps" in settings:
- `Ctrl+→` jumps through entire word
- With CamelHumps: `getUserName` → `get|User|Name` (3 steps)

### 6. Bookmarks

```
F11 → Toggle bookmark (with number: Ctrl+Shift+[0-9])
Shift+F11 → Show bookmarks
Ctrl+[0-9] → Jump to bookmark

Usage: Mark important places in code during debugging
```

### 7. Scratches

`Ctrl+Alt+Shift+Insert` → New scratch file
- Temporary notes/tests
- Not in project
- With syntax highlighting
- Perfect for testing snippets

### 8. Local History

`Alt+Shift+C` → Local History
- IntelliJ saves local history of changes
- You can revert to earlier versions
- Works even without Git!

## Customization

### Change Keymap

`Ctrl+Alt+S` → Keymap

**Recommended settings:**
1. **Add Alt+↑/↓ for Move Line Up/Down**
2. **Ctrl+Shift+↑/↓ for Move Statement**
3. **F1 for Quick Documentation** (instead of Ctrl+Q)

### Disable Mouse (Hardcore Mode)

1. Install plugin: "Key Promoter X"
   - Shows shortcut after every mouse click
   - Motivates learning shortcuts

2. Install plugin: "Presentation Assistant"
   - Shows all used shortcuts
   - Great for learning

### Productive Plugins

1. **IdeaVim** - Vim keybindings
2. **String Manipulation** - Advanced string operations
3. **Rainbow Brackets** - Colored brackets
4. **GitToolBox** - Extended Git info
5. **SonarLint** - Real-time code quality

## Practical Exercises

### Week 1: Basics
```
Day 1-2: Navigation
- Shift Shift (100x per day)
- Ctrl+N, Ctrl+Shift+N
- Ctrl+E
- Don't use mouse to open files!

Day 3-4: Editing
- Ctrl+W / Ctrl+Shift+W
- Ctrl+D, Ctrl+Y
- Alt+Insert
- Keyboard only for editing!

Day 5-7: Refactoring
- Shift+F6 (rename everything)
- Ctrl+Alt+M (extract method)
- Alt+Enter (fix warnings)
```

### Week 2: Advanced
```
Day 1-3: Multi-cursor
- Alt+J for everything
- Practice on long lists

Day 4-5: Git
- Alt+~ → all operations
- Ctrl+K → Commit
- Keyboard only for Git!

Day 6-7: Debugging
- Ctrl+F8 → breakpoints
- F8, F7 → stepping
- Alt+F8 → evaluate
- Zero mouse during debug!
```

### Week 3: Mastery
```
- Try not using mouse for entire day
- Use "Key Promoter X"
- Goal: 95%+ operations without mouse
```

## Printable Cheatsheet

### Navigation
```
Shift Shift         Search Everywhere
Ctrl+N              Go to Class
Ctrl+Shift+N        Go to File
Ctrl+E              Recent Files
Ctrl+B              Go to Declaration
Alt+←/→             Back/Forward
```

### Editing
```
Ctrl+Space          Code Completion
Ctrl+W              Expand Selection
Alt+Insert          Generate
Ctrl+D              Duplicate Line
Ctrl+Y              Delete Line
Ctrl+/              Comment
```

### Refactoring
```
Shift+F6            Rename
Ctrl+Alt+M          Extract Method
Ctrl+Alt+V          Extract Variable
Alt+Enter           Show Intentions
```

### Running
```
Shift+F10           Run
Shift+F9            Debug
Ctrl+F2             Stop
F8                  Step Over
F7                  Step Into
```

### Git
```
Alt+~               VCS Menu
Ctrl+K              Commit
Ctrl+Shift+K        Push
Ctrl+T              Update
```

### Tools
```
Alt+1               Project
Alt+4               Run
Alt+5               Debug
Alt+F12             Terminal
Shift+Esc           Hide Window
```

## Keyboard-Only Challenge

### Test yourself!

Complete the following tasks using **ONLY** the keyboard:

1. ✅ Open `UserService` class
2. ✅ Find `findById` method
3. ✅ See all places where it's used
4. ✅ Go to one of them
5. ✅ Return to `UserService`
6. ✅ Add new `deleteUser` method
7. ✅ Extract fragment to new method
8. ✅ Rename variable in all places
9. ✅ Set breakpoint
10. ✅ Run debug
11. ✅ Evaluate expression in debugger
12. ✅ Stop debugger
13. ✅ Commit changes
14. ✅ Push to remote

**If you used mouse even once - repeat!**

## Resources

- `Help → Keyboard Shortcuts PDF` - official cheatsheet
- `Help → Productivity Guide` - Your shortcut usage statistics
- https://www.jetbrains.com/help/idea/ - documentation
- YouTube: "IntelliJ IDEA Tips and Tricks"

---

## Mindset Shift

**Instead of:** "Where in the menu is this option?"
**Think:** "What shortcut opens this?"

**Instead of:** Clicking with mouse
**Think:** `Shift Shift` → type what you're looking for

**Instead of:** Scrolling in Project Explorer
**Think:** `Ctrl+N` → open directly

**Goal:** Mouse only for scrolling documentation (and rarely!)

---

**Remember:** First 2 weeks will be slower. After a month you'll be 2x faster. After 3 months you won't imagine working with mouse!

🚀 **Happy Coding without Mouse!**
