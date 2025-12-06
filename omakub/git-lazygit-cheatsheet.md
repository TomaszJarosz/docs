# Git & Lazygit - Cheatsheet

## Git - Command Line

### Podstawowa Konfiguracja

```bash
# Ustaw dane użytkownika
git config --global user.name "Twoje Imię"
git config --global user.email "email@example.com"

# Edytor
git config --global core.editor "nvim"

# Aliasy (przydatne!)
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.unstage 'reset HEAD --'
git config --global alias.last 'log -1 HEAD'
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"

# Zobacz konfigurację
git config --list
git config --global --edit
```

### Podstawowe Komendy

**Inicjalizacja i Klonowanie:**
```bash
git init                          # Nowe repo
git clone url                     # Klonuj repo
git clone url folder             # Klonuj do folderu
git clone --depth 1 url          # Shallow clone (szybszy)
```

**Status i Informacje:**
```bash
git status                        # Status repozytorium
git status -s                     # Skrócony status
git diff                          # Zmiany (unstaged)
git diff --staged                 # Zmiany (staged)
git diff HEAD                     # Wszystkie zmiany
git diff branch1 branch2          # Różnice między gałęziami
git log                           # Historia commitów
git log --oneline                 # Skrócona historia
git log --graph --all             # Graficzna historia
git show commit_hash              # Pokaż commit
```

**Staging i Commits:**
```bash
git add plik.txt                  # Dodaj plik
git add .                         # Dodaj wszystkie
git add -p                        # Interaktywne dodawanie (po kawałku)
git reset plik.txt                # Unstage plik
git reset                         # Unstage wszystko

git commit -m "message"           # Commit
git commit -am "message"          # Add + commit (tylko tracked files)
git commit --amend                # Popraw ostatni commit
git commit --amend --no-edit      # Popraw bez zmiany message
```

**Gałęzie (Branches):**
```bash
git branch                        # Lista gałęzi
git branch nazwa                  # Nowa gałąź
git branch -d nazwa               # Usuń gałąź (safe)
git branch -D nazwa               # Usuń gałąź (force)
git checkout nazwa                # Przełącz na gałąź
git checkout -b nazwa             # Utwórz i przełącz
git switch nazwa                  # Przełącz (nowsza komenda)
git switch -c nazwa               # Utwórz i przełącz (nowsza)
git merge nazwa                   # Merge gałęzi
git rebase main                   # Rebase na main
```

**Remote (Zdalne Repo):**
```bash
git remote                        # Lista remote
git remote -v                     # Lista z URL
git remote add origin url         # Dodaj remote
git remote remove origin          # Usuń remote
git remote rename old new         # Zmień nazwę

git fetch                         # Pobierz zmiany
git fetch origin                  # Pobierz z origin
git pull                          # Fetch + merge
git pull --rebase                 # Fetch + rebase
git push                          # Wyślij zmiany
git push origin branch            # Wyślij do gałęzi
git push -u origin branch         # Wyślij i ustaw upstream
git push --force                  # Force push (OSTROŻNIE!)
git push --force-with-lease       # Bezpieczniejszy force push
```

**Cofanie Zmian:**
```bash
# Unstage (cofnij git add)
git reset plik.txt
git reset HEAD plik.txt

# Odrzuć zmiany w pliku (working directory)
git checkout -- plik.txt
git restore plik.txt              # Nowsza komenda

# Cofnij commit (zachowaj zmiany)
git reset --soft HEAD~1

# Cofnij commit (odrzuć zmiany)
git reset --hard HEAD~1

# Cofnij commit (stwórz nowy commit cofający)
git revert commit_hash

# Wyczyść working directory
git clean -n                      # Dry run
git clean -f                      # Usuń untracked files
git clean -fd                     # Usuń untracked files i foldery
```

**Stash (Schowek):**
```bash
git stash                         # Schowaj zmiany
git stash save "opis"             # Schowaj z opisem
git stash list                    # Lista stash
git stash pop                     # Przywróć i usuń stash
git stash apply                   # Przywróć (zachowaj stash)
git stash drop                    # Usuń stash
git stash clear                   # Wyczyść wszystkie stash
git stash show -p                 # Pokaż zawartość stash
```

**Tagi:**
```bash
git tag                           # Lista tagów
git tag v1.0.0                    # Lightweight tag
git tag -a v1.0.0 -m "Release"   # Annotated tag
git tag -d v1.0.0                 # Usuń tag lokalnie
git push origin v1.0.0            # Wyślij tag
git push origin --tags            # Wyślij wszystkie tagi
git push origin :refs/tags/v1.0.0 # Usuń tag ze zdalnego
```

### Zaawansowane

**Interaktywne Rebase:**
```bash
git rebase -i HEAD~3              # Edytuj ostatnie 3 commity
# W edytorze:
# pick = zachowaj commit
# reword = zmień message
# edit = zatrzymaj i edytuj
# squash = połącz z poprzednim
# fixup = squash bez message
# drop = usuń commit
```

**Cherry-pick:**
```bash
git cherry-pick commit_hash       # Zastosuj commit z innej gałęzi
git cherry-pick A B C             # Wiele commitów
git cherry-pick --abort           # Anuluj
```

**Blame i Historia:**
```bash
git blame plik.txt                # Kto zmienił każdą linię
git log -p plik.txt               # Historia zmian pliku
git log --follow plik.txt         # Historia z zmianami nazwy
git log --grep="pattern"          # Szukaj w commitach
git log --author="name"           # Commity autora
git log --since="2 weeks ago"     # Ostatnie 2 tygodnie
```

**Bisect (Znajdź Bug):**
```bash
git bisect start                  # Rozpocznij
git bisect bad                    # Oznacz jako złe
git bisect good commit_hash       # Oznacz dobry commit
# Git automatycznie testuje commity
git bisect good/bad               # Oznaczaj kolejne
git bisect reset                  # Zakończ
```

**Submoduły:**
```bash
git submodule add url path        # Dodaj submodule
git submodule init                # Inicjalizuj
git submodule update              # Zaktualizuj
git clone --recursive url         # Klonuj z submodułami
```

**Worktree (Wiele Katalogów Roboczych):**
```bash
git worktree add ../feature feature-branch
git worktree list
git worktree remove ../feature
```

## Lazygit - Terminal UI dla Git

**Uruchomienie:**
```bash
lazygit
# lub alias w Omakub:
lg
```

### Główne Panele

Lazygit ma 5 głównych paneli:
1. **Status** - Stan repozytorium
2. **Files** - Pliki (changes)
3. **Branches** - Gałęzie
4. **Commits** - Historia commitów
5. **Stash** - Schowane zmiany

### Nawigacja w Lazygit

| Skrót | Akcja |
|-------|-------|
| `1-5` | Przełącz między panelami (Status, Files, Branches, Commits, Stash) |
| `h/l` lub `←/→` | Przełącz między panelami |
| `j/k` lub `↑/↓` | Poruszaj się w panelu |
| `[/]` | Poprzedni/następny panel |
| `</>` | Scroll w panelu głównym |
| `Ctrl+u/d` | Scroll w górę/dół (pół strony) |
| `q` | Quit / Wróć |
| `Esc` | Anuluj / Wróć |
| `?` | Pomoc (zobacz wszystkie skróty!) |

### Panel Files (Pliki)

| Skrót | Akcja |
|-------|-------|
| `Space` | Stage/unstage plik lub hunk |
| `a` | Stage/unstage wszystko |
| `d` | Discard changes (usuń zmiany) |
| `e` | Edytuj plik |
| `o` | Otwórz plik |
| `i` | Add to .gitignore |
| `r` | Odśwież pliki |
| `s` | Stash wszystkie zmiany |
| `S` | Stash options (menu) |
| `M` | Commit (otwórz edytor message) |
| `c` | Commit (inline message) |
| `A` | Amend last commit |
| `Enter` | Stage pojedynczych linii (stage hunks) |

**W widoku hunków (Enter na pliku):**
| Skrót | Akcja |
|-------|-------|
| `Space` | Stage/unstage hunk |
| `a` | Stage/unstage plik |
| `e` | Edit hunk |
| `Esc` | Wróć do listy plików |

### Panel Commits

| Skrót | Akcja |
|-------|-------|
| `Space` | Checkout commit |
| `c` | Checkout commit (detached) |
| `r` | Reword commit (zmień message) |
| `R` | Reword with editor |
| `g` | Reset to commit (mixed) |
| `s` | Squash down (połącz z poprzednim) |
| `f` | Fixup commit |
| `d` | Delete commit (drop) |
| `e` | Edit commit |
| `p` | Pick commit (cherry-pick) |
| `C` | Copy commit (sha) |
| `A` | Amend commit |
| `Enter` | Zobacz pliki w commit |
| `v` | Paste (commits) |
| `t` | Revert commit |
| `T` | Tag commit |

**Rebase interaktywne:**
| Skrót | Akcja |
|-------|-------|
| `i` | Start interactive rebase |
| `e` | Edit (w trybie rebase) |
| `m` | Move commit down |
| `M` | Move commit up |

### Panel Branches

| Skrót | Akcja |
|-------|-------|
| `Space` | Checkout branch |
| `n` | Nowa gałąź |
| `o` | Utwórz pull request |
| `c` | Checkout by name |
| `r` | Rebase branch |
| `M` | Merge do obecnej gałęzi |
| `i` | Show git-flow options |
| `d` | Delete branch |
| `D` | Force delete |
| `F` | Fast-forward |
| `g` | Reset (z menu opcji) |
| `R` | Rename branch |
| `Enter` | Zobacz commits |
| `w` | View merge/rebase options |

### Panel Stash

| Skrót | Akcja |
|-------|-------|
| `Space` | Apply stash |
| `g` | Pop stash |
| `d` | Drop stash |
| `n` | Nowy stash |
| `r` | Rename stash |

### Remote Operations (Push/Pull)

| Skrót | Akcja |
|-------|-------|
| `p` | Pull |
| `P` | Push |
| `Shift+P` | Push force |
| `f` | Fetch |
| `F` | Force fetch |

### Ogólne

| Skrót | Akcja |
|-------|-------|
| `x` | Otwórz menu opcji |
| `!` | Otwórz command log |
| `@` | Otwórz command log menu |
| `z` | Undo (cofnij) |
| `Ctrl+z` | Redo |
| `:` | Execute custom command |
| `+` | Next screen mode |
| `_` | Previous screen mode |
| `Ctrl+r` | Ostatnio używane repo (switch) |
| `Ctrl+e` | Open lazygit config |

### Wyszukiwanie i Filtrowanie

| Skrót | Akcja |
|-------|-------|
| `/` | Start search (filtruj) |
| `Ctrl+s` | View filter-by-path options |
| `Ctrl+/` | Regex toggle |

## Workflow Tips

### 1. Podstawowy Workflow z Lazygit

```bash
# Uruchom lazygit
lazygit

# W lazygit:
1. Panel Files (2)
2. Space - stage pliki
3. c - commit z message
4. P - push
```

### 2. Interaktywne Staging (Hunks)

W lazygit:
1. Panel Files
2. `Enter` na pliku - zobacz hunks
3. `Space` - stage wybrane hunki
4. `Esc` - wróć
5. `c` - commit

### 3. Amending Commits

**Dodaj zmiany do ostatniego commita:**
```bash
# W lazygit:
1. Zmień plik
2. Panel Files
3. Space - stage
4. A - amend last commit
```

**Zmień message ostatniego commita:**
```bash
# W lazygit:
1. Panel Commits
2. r na ostatnim commicie
```

### 4. Rebase Interactive

```bash
# W lazygit:
1. Panel Commits
2. i - start interactive rebase
3. Używaj s/f/d do squash/fixup/drop
4. m/M - przenoś commity
5. Ctrl+o - kontynuuj rebase
```

### 5. Branch Workflow

```bash
# Nowa feature branch:
1. Panel Branches
2. n - new branch
3. Wpisz nazwę

# Merge do main:
1. Checkout main (Space na main)
2. Panel Branches
3. M na feature branch - merge
```

### 6. Stash Workflow

```bash
# Schowaj zmiany:
1. Panel Files
2. s - stash all

# Przywróć:
1. Panel Stash
2. Space - apply (lub g - pop)
```

### 7. Cherry-pick

```bash
1. Panel Commits (inna gałąź)
2. p na commicie - cherry-pick
3. Przełącz na docelową gałąź
4. v - paste (apply cherry-pick)
```

### 8. Rozwiązywanie Konfliktów

```bash
# Po merge/rebase z konfliktami:
1. Panel Files - pliki z konfliktami oznaczone
2. e - edytuj plik (otwiera w nvim)
3. Rozwiąż konflikty
4. :wq - zapisz i wyjdź
5. Space - stage rozwiązany plik
6. c - commit (lub kontynuuj rebase)
```

## Git Best Practices

### Commit Messages

**Format:**
```
typ: krótki opis (max 50 znaków)

Dłuższy opis jeśli potrzebny (wrap at 72 chars)
- Punkt 1
- Punkt 2

Fixes #123
```

**Typy:**
- `feat:` - nowa funkcjonalność
- `fix:` - poprawka błędu
- `docs:` - dokumentacja
- `style:` - formatowanie (nie wpływa na kod)
- `refactor:` - refaktoryzacja
- `test:` - testy
- `chore:` - maintenance

### Branch Naming

```bash
feature/nazwa-funkcji
bugfix/nazwa-buga
hotfix/pilna-poprawka
release/v1.2.3
```

### Workflow Strategies

**1. Feature Branch Workflow:**
```bash
git checkout -b feature/new-feature
# Praca...
git add .
git commit -m "feat: add new feature"
git push -u origin feature/new-feature
# Pull request/merge do main
```

**2. Git Flow:**
```bash
# Main branches: main, develop
# Supporting: feature/*, release/*, hotfix/*

git checkout -b develop
git checkout -b feature/feature-name
# Praca...
git checkout develop
git merge feature/feature-name
```

**3. Rebase Before Merge:**
```bash
git checkout feature
git rebase main           # Zaktualizuj z main
git push --force-with-lease
# Potem merge do main
```

### Przydatne .gitconfig Snippets

```ini
[core]
    editor = nvim
    autocrlf = input
    pager = delta           # Lepszy diff (jeśli zainstalowane)

[alias]
    st = status -sb
    co = checkout
    br = branch
    ci = commit
    unstage = reset HEAD --
    undo = reset --soft HEAD^
    lg = log --graph --oneline --all --decorate
    last = log -1 HEAD
    amend = commit --amend --no-edit

[pull]
    rebase = true           # Domyślnie pull --rebase

[push]
    default = current       # Push do gałęzi o tej samej nazwie
    followTags = true       # Automatycznie push tagów

[fetch]
    prune = true            # Usuń stare remote branches

[diff]
    colorMoved = zebra      # Lepsze pokazywanie przeniesionych linii

[merge]
    conflictstyle = diff3   # Lepsze pokazywanie konfliktów

[rerere]
    enabled = true          # Zapamiętaj jak rozwiązałeś konflikty
```

## .gitignore Patterns

```gitignore
# OS
.DS_Store
Thumbs.db

# Editors
.vscode/
.idea/
*.swp
*.swo
*~

# Languages
## Node
node_modules/
npm-debug.log
yarn-error.log

## Python
__pycache__/
*.py[cod]
*.pyo
.env
venv/
.pytest_cache/

## Ruby
*.gem
.bundle/

## Rust
target/

# Build outputs
dist/
build/
*.log

# Secrets
.env
.env.local
credentials.json
*.key
*.pem
```

## Przydatne Git Aliasy (Bash)

Dodaj do `~/.bashrc`:
```bash
alias g='git'
alias gs='git status'
alias ga='git add'
alias gc='git commit'
alias gp='git push'
alias gl='git pull'
alias gd='git diff'
alias gco='git checkout'
alias gb='git branch'
alias glog='git log --oneline --graph --decorate'
alias lg='lazygit'

# Funkcje
gac() {
    git add .
    git commit -m "$1"
}

gacp() {
    git add .
    git commit -m "$1"
    git push
}

# Użycie:
# gac "fix: update readme"
# gacp "feat: add new feature"
```

## Zasoby

- **Git Docs:** https://git-scm.com/doc
- **Lazygit:** https://github.com/jesseduffield/lazygit
- **Interactive Tutorial:** https://learngitbranching.js.org/
- **Git Cheatsheet:** https://education.github.com/git-cheat-sheet-education.pdf
- `man git` - Dokumentacja
- `git help <command>` - Pomoc dla komendy

## Szybki Start

**Git:**
```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin url
git push -u origin main
```

**Lazygit:**
```bash
lazygit
# 2 - Files
# Space - Stage
# c - Commit
# P - Push
```

**Zapamiętaj:**
- Commituj często, małymi porcjami
- Używaj dobrych commit messages
- Rebase przed merge (czysta historia)
- Nigdy force push do współdzielonej gałęzi
- Lazygit = szybki workflow wizualny
