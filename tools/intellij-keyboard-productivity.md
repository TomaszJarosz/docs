# IntelliJ IDEA - Keyboard Productivity Guide

Przewodnik po IntelliJ IDEA dla programistów, którzy chcą maksymalnie wykorzystać klawiaturę i wyeliminować używanie myszy.

## Filozofia Pracy bez Myszy

**Dlaczego keyboard-first?**
- Szybkość - brak przerywania flow na sięganie po mysz
- Precyzja - dokładne operacje bez klikania
- Produktywność - mniej zmęczenia, więcej kodu
- Flow state - utrzymanie koncentracji

**Cel:** 95%+ operacji bez myszy

## Podstawowe Skróty (Musisz Znać)

### Nawigacja Uniwersalna

| Skrót | Akcja | Opis |
|-------|-------|------|
| `Shift Shift` | **Search Everywhere** | Najważniejszy skrót! Szukaj wszystkiego |
| `Ctrl+Shift+A` | Find Action | Znajdź dowolną akcję/komendę |
| `Ctrl+N` | Go to Class | Otwórz klasę po nazwie |
| `Ctrl+Shift+N` | Go to File | Otwórz plik po nazwie |
| `Ctrl+Alt+Shift+N` | Go to Symbol | Znajdź metodę/field |
| `Ctrl+E` | Recent Files | Ostatnio otwarte pliki |
| `Ctrl+Shift+E` | Recent Locations | Ostatnio edytowane miejsca |

**Protip:** `Shift Shift` zastępuje 90% nawigacji myszką!

### Nawigacja w Kodzie

| Skrót | Akcja |
|-------|-------|
| `Ctrl+B` lub `Ctrl+Click` | Go to Declaration |
| `Ctrl+Alt+B` | Go to Implementation |
| `Ctrl+U` | Go to Super Method/Class |
| `Ctrl+Shift+B` | Go to Type Declaration |
| `Ctrl+G` | Go to Line |
| `Alt+←/→` | Poprzednia/Następna lokalizacja |
| `Ctrl+[/]` | Skocz do początku/końca bloku |
| `Ctrl+F12` | File Structure (metody w klasie) |
| `Alt+↑/↓` | Poprzednia/Następna metoda |

### Edycja Kodu

| Skrót | Akcja |
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

| Skrót | Akcja |
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

| Skrót | Akcja |
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

## Zaawansowane Skróty

### Multi-Cursor & Selection

| Skrót | Akcja |
|-------|-------|
| `Alt+J` | Add Selection for Next Occurrence |
| `Alt+Shift+J` | Unselect Occurrence |
| `Ctrl+Alt+Shift+J` | Select All Occurrences |
| `Alt+Shift+Insert` | Column Selection Mode |
| `Alt+Shift+Click` | Add/Remove Caret |
| `Ctrl+Alt+Shift+Click` | Create Rectangular Selection |
| `Esc` | Remove All Carets |

**Przykład workflow:**
1. Zaznacz zmienną
2. `Alt+J` kilka razy (zaznacza kolejne wystąpienia)
3. Pisz - wszystkie wystąpienia się zmienią

### Live Templates

| Skrót | Template | Rozwinięcie |
|-------|----------|-------------|
| `psvm` + `Tab` | `public static void main` | Main method |
| `sout` + `Tab` | `System.out.println()` | Print |
| `fori` + `Tab` | `for (int i = 0; i < ; i++)` | For loop |
| `iter` + `Tab` | `for (Type item : collection)` | For-each |
| `ifn` + `Tab` | `if (x == null)` | Null check |
| `inn` + `Tab` | `if (x != null)` | Not null check |

**Twórz własne!** `Ctrl+Alt+S` → Live Templates

### Code Analysis & Fixing

| Skrót | Akcja |
|-------|-------|
| `Alt+Enter` | **Show Intention Actions** (najważniejsze!) |
| `Ctrl+F1` | Show Error Description |
| `F2` | Next Highlighted Error |
| `Shift+F2` | Previous Highlighted Error |
| `Ctrl+Alt+Shift+I` | Run Inspection by Name |
| `Ctrl+Alt+L` | Reformat Code |
| `Ctrl+Alt+O` | Optimize Imports |

**Protip:** `Alt+Enter` to magiczne rozwiązanie większości problemów!

### VCS / Git Integration

| Skrót | Akcja |
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

| Skrót | Akcja |
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

## Workflow bez Myszy

### 1. Otwieranie Plików

```
❌ Mysz: Klikanie w Project Explorer
✅ Klawiatura:
   1. Ctrl+N → wpisz nazwę klasy
   2. Ctrl+Shift+N → wpisz nazwę pliku
   3. Shift Shift → wpisz cokolwiek
   4. Ctrl+E → wybierz z ostatnich
```

### 2. Nawigacja po Kodzie

```
❌ Mysz: Scrollowanie i klikanie
✅ Klawiatura:
   1. Ctrl+F12 → struktura pliku → wybierz metodę
   2. Ctrl+Alt+Shift+N → wpisz nazwę metody
   3. Ctrl+B → idź do definicji
   4. Alt+←/→ → poprzednia/następna lokalizacja
```

### 3. Refactoring

```
❌ Mysz: Prawy przycisk → Refactor → wybierz
✅ Klawiatura:
   1. Zaznacz kod: Ctrl+W (rozszerz selekcję)
   2. Shift+F6 → rename
   3. Ctrl+Alt+M → extract method
   4. Alt+Enter → quick fixes
```

### 4. Running Tests

```
❌ Mysz: Klik na zieloną strzałkę
✅ Klawiatura:
   1. Ctrl+Shift+F10 → run kontekst (test/main)
   2. Shift+F10 → re-run ostatni
   3. Ctrl+Shift+F9 → re-compile i run
```

### 5. Debugging

```
❌ Mysz: Klikanie w gutter, menu Debug
✅ Klawiatura:
   1. Ctrl+F8 → toggle breakpoint
   2. Shift+F9 → start debug
   3. F8 → step over
   4. F7 → step into
   5. Alt+F8 → evaluate expression
```

### 6. Git Operations

```
❌ Mysz: Klikanie w VCS menu
✅ Klawiatura:
   1. Alt+~ → VCS menu
   2. Ctrl+K → commit
   3. Ctrl+Shift+K → push
   4. Ctrl+T → update/pull
```

## Praktyczne Scenariusze

### Scenariusz 1: Implementacja Nowej Metody

```
1. Ctrl+N → Otwórz klasę
2. Ctrl+F12 → Znajdź miejsce na metodę
3. Ctrl+O → Override lub Alt+Insert → Generate
4. Ctrl+Space → Code completion
5. Ctrl+Alt+T → Surround with try-catch
6. Ctrl+Alt+L → Reformat
7. Ctrl+Shift+F10 → Run test
```

### Scenariusz 2: Refactor Legacy Code

```
1. Ctrl+Alt+Shift+N → Znajdź metodę po nazwie
2. Ctrl+W (kilka razy) → Zaznacz cały blok
3. Ctrl+Alt+M → Extract method
4. Shift+F6 → Rename method
5. Alt+Enter → Resolve warnings
6. F2 → Przejdź do następnego błędu
7. Alt+Enter → Fix it
8. Ctrl+K → Commit
```

### Scenariusz 3: Fix Bug

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

### Scenariusz 4: Code Review w IDE

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

`Shift Shift` potem:
- Nic nie wpisuj → ostatnie pliki
- `/` → tylko pliki
- `#` → tylko klasy
- `@` → tylko symbole (metody)
- `:` → linia (go to line)

**Przykład:**
- `Shift Shift` → `UserService` → otwórz klasę
- `Shift Shift` → `/application.yml` → otwórz config
- `Shift Shift` → `@findUser` → skocz do metody

### 2. Multi-Cursor Power

```java
// Masz:
String name;
String email;
String phone;

// Chcesz dodać "private" przed każdym
// 1. Zaznacz "String" w pierwszej linii
// 2. Alt+J, Alt+J (zaznacz wszystkie)
// 3. Home (początek linii)
// 4. Wpisz "private "
// Gotowe!

private String name;
private String email;
private String phone;
```

### 3. Clipboard History

`Ctrl+Shift+V` → Zobacz historię schowka (ostatnie 5 kopii)

### 4. Postfix Completion

Zamiast owijać kod, użyj postfix:

```java
// Wpisz:
user.null
// Tab → automatycznie:
if (user == null) {}

// Wpisz:
list.for
// Tab → automatycznie:
for (String item : list) {}

// Inne:
.var → assign to variable
.return → return statement
.sout → System.out.println()
.notnull → if != null
```

### 5. CamelHumps

W ustawieniach włącz "CamelHumps":
- `Ctrl+→` przeskakuje przez całe słowo
- Z CamelHumps: `getUserName` → `get|User|Name` (3 kroki)

### 6. Bookmarks

```
F11 → Toggle bookmark (z numerem: Ctrl+Shift+[0-9])
Shift+F11 → Show bookmarks
Ctrl+[0-9] → Skocz do bookmark

Użycie: Oznacz ważne miejsca w kodzie podczas debugowania
```

### 7. Scratches

`Ctrl+Alt+Shift+Insert` → New scratch file
- Tymczasowe notatki/testy
- Nie w projekcie
- Z syntax highlighting
- Idealne do testowania snippetów

### 8. Local History

`Alt+Shift+C` → Local History
- IntelliJ zapisuje lokalną historię zmian
- Możesz wrócić do wcześniejszych wersji
- Działa nawet bez Git!

## Customizacja

### Zmień Keymap

`Ctrl+Alt+S` → Keymap

**Polecane ustawienia:**
1. **Dodaj Alt+↑/↓ dla Move Line Up/Down**
2. **Ctrl+Shift+↑/↓ dla Move Statement**
3. **F1 dla Quick Documentation** (zamiast Ctrl+Q)

### Wyłącz Myszy (Hardcore Mode)

1. Install plugin: "Key Promoter X"
   - Pokazuje skrót po każdym kliknięciu myszą
   - Motywuje do nauki skrótów

2. Install plugin: "Presentation Assistant"
   - Pokazuje wszystkie używane skróty
   - Świetne do nauki

### Produktywne Pluginy

1. **IdeaVim** - Vim keybindings
2. **String Manipulation** - Zaawansowane operacje na stringach
3. **Rainbow Brackets** - Kolorowe nawiasy
4. **GitToolBox** - Rozszerzone info o Git
5. **SonarLint** - Code quality w czasie rzeczywistym

## Praktyczne Ćwiczenia

### Tydzień 1: Podstawy
```
Dzień 1-2: Nawigacja
- Shift Shift (100x dziennie)
- Ctrl+N, Ctrl+Shift+N
- Ctrl+E
- Nie używaj myszy do otwierania plików!

Dzień 3-4: Edycja
- Ctrl+W / Ctrl+Shift+W
- Ctrl+D, Ctrl+Y
- Alt+Insert
- Tylko klawiatura do edycji!

Dzień 5-7: Refactoring
- Shift+F6 (rename wszystko)
- Ctrl+Alt+M (extract method)
- Alt+Enter (fix warnings)
```

### Tydzień 2: Zaawansowane
```
Dzień 1-3: Multi-cursor
- Alt+J do wszystkiego
- Ćwicz na długich listach

Dzień 4-5: Git
- Alt+~ → wszystkie operacje
- Ctrl+K → Commit
- Tylko klawiatura dla Git!

Dzień 6-7: Debugging
- Ctrl+F8 → breakpoints
- F8, F7 → stepping
- Alt+F8 → evaluate
- Zero myszy podczas debug!
```

### Tydzień 3: Mastery
```
- Spróbuj nie używać myszy przez cały dzień
- Używaj "Key Promoter X"
- Cel: 95%+ operacji bez myszy
```

## Cheatsheet do Wydrukowania

### Nawigacja
```
Shift Shift         Search Everywhere
Ctrl+N              Go to Class
Ctrl+Shift+N        Go to File
Ctrl+E              Recent Files
Ctrl+B              Go to Declaration
Alt+←/→             Back/Forward
```

### Edycja
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

### Sprawdź się!

Wykonaj poniższe zadania **TYLKO** używając klawiatury:

1. ✅ Otwórz klasę `UserService`
2. ✅ Znajdź metodę `findById`
3. ✅ Zobacz wszystkie miejsca gdzie jest użyta
4. ✅ Przejdź do jednego z nich
5. ✅ Wróć do `UserService`
6. ✅ Dodaj nową metodę `deleteUser`
7. ✅ Extract fragment do nowej metody
8. ✅ Zmień nazwę zmiennej we wszystkich miejscach
9. ✅ Ustaw breakpoint
10. ✅ Uruchom debug
11. ✅ Evaluate expression w debuggerze
12. ✅ Zatrzymaj debugger
13. ✅ Commit zmiany
14. ✅ Push do remote

**Jeśli użyłeś myszy choć raz - powtórz!**

## Zasoby

- `Help → Keyboard Shortcuts PDF` - oficjalny cheatsheet
- `Help → Productivity Guide` - Twoje statystyki użycia skrótów
- https://www.jetbrains.com/help/idea/ - dokumentacja
- YouTube: "IntelliJ IDEA Tips and Tricks"

---

## Mindset Shift

**Zamiast:** "Gdzie w menu jest ta opcja?"
**Myśl:** "Jaki skrót otwiera to?"

**Zamiast:** Kliknąć myszą
**Myśl:** `Shift Shift` → wpisz co szukasz

**Zamiast:** Scrollować w Project Explorer
**Myśl:** `Ctrl+N` → otwórz bezpośrednio

**Cel:** Mysz tylko do scrollowania dokumentacji (i to rzadko!)

---

**Pamiętaj:** Pierwsze 2 tygodnie będą wolniejsze. Po miesiącu będziesz 2x szybszy. Po 3 miesiącach nie wyobrazisz sobie pracy z myszą!

🚀 **Happy Coding without Mouse!**
