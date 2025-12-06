# Git Console - Cheatsheet dla Programisty

Praktyczny przewodnik po Git z konsoli dla efektywnej pracy bez GUI.

## Filozofia Pracy z Git w Konsoli

**Dlaczego konsola?**
- Szybkość - brak klikania
- Automatyzacja - skrypty i aliasy
- Pełna kontrola - dostęp do wszystkich opcji
- Universalność - działa wszędzie (SSH, CI/CD)

## Szybka Konfiguracja

### Podstawowa Konfiguracja

```bash
# Dane użytkownika
git config --global user.name "Twoje Imię"
git config --global user.email "email@example.com"

# Edytor
git config --global core.editor "nvim"

# Kolory
git config --global color.ui auto

# Domyślna gałąź
git config --global init.defaultBranch main

# Pull z rebase zamiast merge
git config --global pull.rebase true

# Push tylko bieżącej gałęzi
git config --global push.default current

# Automatyczne usuwanie martwych remote branches
git config --global fetch.prune true

# Lepsze pokazywanie konfliktów
git config --global merge.conflictstyle diff3

# Zapamiętywanie rozwiązań konfliktów
git config --global rerere.enabled true
```

### Użyteczne Aliasy

Dodaj do `~/.gitconfig`:

```ini
[alias]
    # Status
    s = status -sb
    st = status

    # Log
    l = log --oneline --graph --decorate
    lg = log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit
    ll = log --oneline --graph --all --decorate
    today = log --since='00:00:00' --all --no-merges --oneline --author=<your-email>

    # Diff
    d = diff
    ds = diff --staged
    dc = diff --cached

    # Commit
    c = commit
    cm = commit -m
    ca = commit --amend
    can = commit --amend --no-edit

    # Branch
    b = branch
    ba = branch -a
    bd = branch -d
    bD = branch -D

    # Checkout
    co = checkout
    cob = checkout -b

    # Switch (nowsze komendy)
    sw = switch
    swc = switch -c

    # Remote
    f = fetch
    fo = fetch origin
    p = push
    pl = pull

    # Stash
    ss = stash save
    sp = stash pop
    sl = stash list

    # Reset
    unstage = reset HEAD --
    undo = reset --soft HEAD^

    # Misc
    last = log -1 HEAD
    aliases = config --get-regexp alias
    contributors = shortlog -sn --all --no-merges
```

Użycie:
```bash
git s          # git status -sb
git lg         # piękny log
git cm "msg"   # commit z message
```

## Codzienny Workflow

### Rozpoczęcie Pracy

```bash
# Sprawdź status
git status

# Zaktualizuj z remote
git pull --rebase

# Lub bezpieczniej (fetch + merge/rebase)
git fetch
git rebase origin/main
```

### Praca nad Zmianami

```bash
# Zobacz co się zmieniło
git status
git diff                  # zmiany unstaged
git diff --staged         # zmiany staged

# Dodaj zmiany
git add plik.txt          # konkretny plik
git add .                 # wszystko w bieżącym katalogu
git add -A                # wszystko w repo
git add -p                # interaktywnie (po kawałku)

# Cofnij git add
git reset HEAD plik.txt   # unstage plik
git reset                 # unstage wszystko

# Odrzuć lokalne zmiany
git checkout -- plik.txt  # stara składnia
git restore plik.txt      # nowa składnia
```

### Commit

```bash
# Podstawowy commit
git commit -m "feat: add user authentication"

# Multi-line commit message
git commit -m "feat: add user authentication" -m "- Add login endpoint
- Add JWT token generation
- Add password hashing"

# Commit wszystkich tracked files
git commit -am "fix: resolve validation bug"

# Popraw ostatni commit (message)
git commit --amend -m "nowa wiadomość"

# Popraw ostatni commit (dodaj pliki)
git add forgotten-file.txt
git commit --amend --no-edit

# Commit z datą
git commit --date="2024-01-15 10:00:00" -m "msg"
```

### Konwencja Commit Messages

Format: `<type>: <subject>`

**Typy:**
- `feat` - nowa funkcjonalność
- `fix` - poprawka błędu
- `docs` - dokumentacja
- `style` - formatowanie (bez zmian w logice)
- `refactor` - refaktoryzacja
- `perf` - optymalizacja wydajności
- `test` - testy
- `chore` - maintenance, dependencies
- `ci` - CI/CD
- `build` - build system

**Przykłady:**
```bash
git commit -m "feat: add password reset functionality"
git commit -m "fix: resolve null pointer in user service"
git commit -m "docs: update API documentation"
git commit -m "refactor: simplify authentication logic"
```

## Gałęzie (Branches)

### Zarządzanie Gałęziami

```bash
# Lista gałęzi
git branch                # lokalne
git branch -a             # wszystkie (remote + local)
git branch -v             # z ostatnim commitem
git branch -vv            # z tracking info

# Nowa gałąź
git branch feature/login
git checkout -b feature/login         # utwórz i przełącz
git switch -c feature/login           # nowsza składnia

# Przełączanie
git checkout main
git switch main

# Zmiana nazwy
git branch -m stara-nazwa nowa-nazwa
git branch -m nowa-nazwa              # zmień bieżącą gałąź

# Usuwanie
git branch -d feature/done            # bezpieczne (sprawdza czy merged)
git branch -D feature/abandoned       # force

# Usuń remote branch
git push origin --delete feature/old
```

### Branch Workflow

```bash
# Feature branch workflow
git checkout main
git pull
git checkout -b feature/new-feature

# ... praca ...
git add .
git commit -m "feat: implement new feature"

# Zaktualizuj z main przed merge
git checkout main
git pull
git checkout feature/new-feature
git rebase main           # lub: git merge main

# Wyślij do remote
git push -u origin feature/new-feature

# Po merge w GitHub/GitLab
git checkout main
git pull
git branch -d feature/new-feature
```

## Remote Operations

### Podstawy

```bash
# Lista remote
git remote -v

# Dodaj remote
git remote add origin https://github.com/user/repo.git

# Zmień URL
git remote set-url origin git@github.com:user/repo.git

# Usuń remote
git remote remove origin

# Zmień nazwę remote
git remote rename origin upstream
```

### Fetch, Pull, Push

```bash
# Fetch - pobierz zmiany (nie merge)
git fetch origin
git fetch --all
git fetch --prune         # usuń martwe remote branches

# Pull - fetch + merge/rebase
git pull
git pull --rebase         # zalecanec
git pull origin main

# Push
git push
git push origin main
git push -u origin feature/new      # ustaw upstream
git push --force-with-lease         # bezpieczniejszy force push
git push --all                      # wszystkie gałęzie

# Push tags
git push --tags
```

### Praca z Fork

```bash
# Dodaj upstream (oryginalny projekt)
git remote add upstream https://github.com/original/repo.git

# Synchronizacja z upstream
git fetch upstream
git checkout main
git merge upstream/main
# lub:
git rebase upstream/main

# Wyślij do swojego fork
git push origin main
```

## Historia i Log

### Przeglądanie Historii

```bash
# Podstawowy log
git log
git log --oneline
git log --graph --all
git log -10                   # ostatnie 10 commitów
git log --since="2 weeks ago"
git log --after="2024-01-01"
git log --author="Jan Kowalski"
git log --grep="fix"          # szukaj w messages

# Log dla pliku
git log plik.txt
git log -p plik.txt           # z diff
git log --follow plik.txt     # śledź zmiany nazwy

# Statystyki
git log --stat
git log --shortstat
git shortlog -sn              # liczba commitów per autor

# Piękny format
git log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset'
```

### Show, Diff, Blame

```bash
# Pokaż commit
git show commit-hash
git show HEAD
git show HEAD~2               # 2 commity wstecz

# Diff
git diff                      # working vs staged
git diff --staged             # staged vs last commit
git diff HEAD                 # working vs last commit
git diff branch1 branch2
git diff commit1 commit2
git diff main...feature       # od wspólnego przodka

# Blame - kto zmienił linię
git blame plik.txt
git blame -L 10,20 plik.txt   # tylko linie 10-20
git blame -w plik.txt         # ignoruj whitespace
git blame -C plik.txt         # wykryj kopiowanie kodu
```

## Cofanie Zmian

### Reset vs Revert

```bash
# Reset - cofa commity (zmienia historię!)
git reset --soft HEAD~1       # cofnij commit, zachowaj zmiany (staged)
git reset --mixed HEAD~1      # cofnij commit, zmiany unstaged (domyślne)
git reset --hard HEAD~1       # cofnij commit, USUŃ zmiany

# Reset do konkretnego commita
git reset --hard abc123

# Revert - tworzy nowy commit cofający (bezpieczne!)
git revert HEAD
git revert commit-hash
git revert HEAD~3
```

### Praktyczne Cofanie

```bash
# Chcę cofnąć ostatni commit (nie pushed)
git reset --soft HEAD~1

# Chcę cofnąć ostatni commit i zmiany
git reset --hard HEAD~1

# Chcę cofnąć commit który już został pushed
git revert HEAD

# Chcę usunąć uncommitted zmiany
git restore plik.txt
git restore .

# Chcę usunąć wszystkie lokalne zmiany
git reset --hard HEAD
git clean -fd                 # usuń untracked files

# Zapisałem się w niewłaściwej gałęzi
git reset --soft HEAD~1
git stash
git checkout correct-branch
git stash pop
git commit
```

## Stash - Schowek

### Podstawy

```bash
# Schowaj zmiany
git stash
git stash save "work in progress"
git stash push -m "WIP: feature X"

# Lista stash
git stash list

# Przywróć
git stash pop                 # apply + drop
git stash apply               # apply (zachowaj w stash)
git stash apply stash@{2}     # konkretny stash

# Usuń
git stash drop stash@{0}
git stash clear               # usuń wszystkie

# Zobacz co jest w stash
git stash show
git stash show -p             # z diff
```

### Zaawansowany Stash

```bash
# Stash tylko unstaged
git stash --keep-index

# Stash z untracked files
git stash -u

# Stash konkretnych plików
git stash push plik1.txt plik2.txt

# Utwórz branch ze stash
git stash branch feature/new-branch
```

## Rebase - Przepisywanie Historii

### Podstawowy Rebase

```bash
# Rebase na inną gałąź
git checkout feature
git rebase main

# Lub krócej
git rebase main feature

# Kontynuuj po rozwiązaniu konfliktów
git add resolved-file.txt
git rebase --continue

# Pomiń commit
git rebase --skip

# Anuluj rebase
git rebase --abort
```

### Interactive Rebase

```bash
# Edytuj ostatnie N commitów
git rebase -i HEAD~3

# W edytorze:
pick abc123 First commit
pick def456 Second commit
pick ghi789 Third commit

# Możliwe akcje:
# pick   = użyj commit
# reword = użyj commit, ale zmień message
# edit   = zatrzymaj się do edycji
# squash = połącz z poprzednim (zachowaj message)
# fixup  = połącz z poprzednim (usuń message)
# drop   = usuń commit
```

### Praktyczne Przykłady

```bash
# Połącz ostatnie 3 commity w jeden
git rebase -i HEAD~3
# Zmień: pick, squash, squash

# Zmień message ostatniego commita
git commit --amend -m "new message"

# Zmień message starszego commita
git rebase -i HEAD~5
# Zmień pick na reword dla wybranego commita

# Usuń commit z historii
git rebase -i HEAD~10
# Zmień pick na drop (lub usuń linię)

# Zmień kolejność commitów
git rebase -i HEAD~5
# Po prostu zmień kolejność linii

# Podziel commit na kilka
git rebase -i HEAD~3
# Zmień pick na edit
# Po zatrzymaniu:
git reset HEAD^
git add plik1.txt
git commit -m "first part"
git add plik2.txt
git commit -m "second part"
git rebase --continue
```

## Cherry-pick

```bash
# Zastosuj konkretny commit z innej gałęzi
git cherry-pick commit-hash

# Wiele commitów
git cherry-pick abc123 def456 ghi789

# Cherry-pick bez commit (tylko dodaj zmiany)
git cherry-pick -n commit-hash

# Kontynuuj po rozwiązaniu konfliktów
git cherry-pick --continue

# Anuluj
git cherry-pick --abort
```

## Tagi

```bash
# Lista tagów
git tag
git tag -l "v1.*"

# Utwórz tag
git tag v1.0.0                              # lightweight
git tag -a v1.0.0 -m "Release version 1.0"  # annotated

# Tag dla starego commita
git tag -a v0.9.0 commit-hash -m "message"

# Pokaż tag
git show v1.0.0

# Push tagów
git push origin v1.0.0
git push origin --tags                      # wszystkie

# Usuń tag
git tag -d v1.0.0                          # lokalnie
git push origin --delete v1.0.0            # remote
```

## Zaawansowane Operacje

### Bisect - Znajdź Bug

```bash
# Rozpocznij bisect
git bisect start
git bisect bad                    # obecny commit jest zły
git bisect good v1.0.0            # ten commit był dobry

# Git automatycznie checkoutuje środkowy commit
# Testuj aplikację i oznacz:
git bisect good                   # działa
# lub
git bisect bad                    # nie działa

# Git checkoutuje kolejny commit do testu
# Powtarzaj aż znajdziesz zły commit

# Zakończ
git bisect reset
```

### Reflog - Historia HEAD

```bash
# Pokaż historię HEAD (wszystkie zmiany)
git reflog

# Przywróć usunięty commit
git reflog
# Znajdź hash usuniętego commita
git checkout commit-hash
git checkout -b recovery-branch

# Cofnij zły reset
git reflog
git reset --hard HEAD@{2}
```

### Worktree - Wiele Katalogów

```bash
# Dodaj dodatkowy katalog roboczy
git worktree add ../feature-branch feature/new-feature

# Lista worktrees
git worktree list

# Usuń worktree
git worktree remove ../feature-branch

# Użycie:
cd ../feature-branch
# Pracujesz w osobnym katalogu, ale tym samym repo!
```

### Submoduły

```bash
# Dodaj submodule
git submodule add https://github.com/user/repo.git libs/repo

# Klonuj repo z submodułami
git clone --recursive https://github.com/user/main-repo.git

# Zaktualizuj submoduły
git submodule update --init --recursive
git submodule update --remote

# Usuń submodule
git submodule deinit libs/repo
git rm libs/repo
```

## Praktyczne Workflow

### Feature Branch Workflow

```bash
# 1. Zacznij nową feature
git checkout main
git pull
git checkout -b feature/user-auth

# 2. Pracuj
# ... kod ...
git add .
git commit -m "feat: implement user authentication"

# 3. Push do remote
git push -u origin feature/user-auth

# 4. Przed merge: zaktualizuj z main
git fetch origin
git rebase origin/main

# 5. Rozwiąż konflikty jeśli są
git add resolved-files
git rebase --continue

# 6. Force push (bezpiecznie)
git push --force-with-lease

# 7. Po merge przez PR/MR
git checkout main
git pull
git branch -d feature/user-auth
git remote prune origin
```

### Hotfix Workflow

```bash
# 1. Pilna poprawka
git checkout main
git pull
git checkout -b hotfix/critical-bug

# 2. Popraw
# ... fix ...
git add .
git commit -m "fix: resolve critical security issue"

# 3. Push i merge ASAP
git push -u origin hotfix/critical-bug

# 4. Po merge
git checkout main
git pull
git branch -d hotfix/critical-bug
```

### Release Workflow

```bash
# 1. Utwórz release branch
git checkout -b release/v1.2.0 develop

# 2. Przygotuj release
# ... testy, dokumentacja ...
git commit -am "chore: prepare v1.2.0 release"

# 3. Merge do main i tag
git checkout main
git merge --no-ff release/v1.2.0
git tag -a v1.2.0 -m "Version 1.2.0"

# 4. Merge z powrotem do develop
git checkout develop
git merge --no-ff release/v1.2.0

# 5. Usuń release branch
git branch -d release/v1.2.0

# 6. Push wszystko
git push origin main develop --tags
```

## Rozwiązywanie Konfliktów

### Proces

```bash
# 1. Konflikt podczas merge/rebase
git status                    # zobacz skonfliktowane pliki

# 2. Otwórz plik - zobaczysz markery:
<<<<<<< HEAD
Twoja wersja
=======
Ich wersja
>>>>>>> branch-name

# 3. Edytuj ręcznie lub użyj narzędzi
git mergetool

# 4. Po rozwiązaniu
git add resolved-file.txt

# 5. Kontynuuj operację
git rebase --continue         # dla rebase
git merge --continue          # dla merge
git commit                    # dla merge (jeśli trzeba)

# Lub anuluj
git rebase --abort
git merge --abort
```

### Strategie Merge

```bash
# Merge z konfliktami - wybierz strategię
git merge --strategy-option theirs feature
git merge --strategy-option ours feature

# Akceptuj wszystko z ich strony
git checkout --theirs plik.txt

# Akceptuj wszystko z naszej strony
git checkout --ours plik.txt
```

## Bash Aliasy dla Git

Dodaj do `~/.bashrc`:

```bash
# Git shortcuts
alias g='git'
alias gs='git status -sb'
alias ga='git add'
alias gaa='git add -A'
alias gc='git commit'
alias gcm='git commit -m'
alias gca='git commit --amend'
alias gcan='git commit --amend --no-edit'
alias gp='git push'
alias gpu='git push -u origin HEAD'
alias gpl='git pull --rebase'
alias gf='git fetch'
alias gd='git diff'
alias gds='git diff --staged'
alias gl='git log --oneline --graph --decorate'
alias gll='git log --oneline --graph --all --decorate'
alias gco='git checkout'
alias gcob='git checkout -b'
alias gb='git branch'
alias gba='git branch -a'
alias gbd='git branch -d'
alias gst='git stash'
alias gstp='git stash pop'
alias gr='git rebase'
alias gri='git rebase -i'
alias grc='git rebase --continue'
alias gra='git rebase --abort'

# Advanced functions
function gac() {
    git add -A
    git commit -m "$1"
}

function gacp() {
    git add -A
    git commit -m "$1"
    git push
}

function gnb() {
    git checkout -b "$1"
    git push -u origin "$1"
}

function gclean() {
    git branch --merged | grep -v "\*" | grep -v "main\|master\|develop" | xargs -n 1 git branch -d
}

# Użycie:
# gac "feat: add feature"
# gacp "fix: resolve bug"
# gnb "feature/new-branch"
# gclean  # usuń zmergowane branche
```

## Skróty Klawiszowe w Shell

```bash
# fzf dla git (jeśli zainstalowane)
# Dodaj do ~/.bashrc:

# Interaktywny checkout branch
gcof() {
    local branches branch
    branches=$(git branch -a) &&
    branch=$(echo "$branches" | fzf +m) &&
    git checkout $(echo "$branch" | sed "s/.* //" | sed "s#remotes/[^/]*/##")
}

# Interaktywny git log
glf() {
    git log --oneline --graph --color=always --all |
    fzf --ansi --no-sort --reverse --tiebreak=index --preview \
    'grep -o "[a-f0-9]\{7,\}" <<< {} | head -1 | xargs git show --color=always' \
    --bind "enter:execute(grep -o '[a-f0-9]\{7,\}' <<< {} | head -1 | xargs git show | less -R)"
}
```

## Best Practices

### Commity

1. **Małe, atomowe commity** - jeden commit = jedna logiczna zmiana
2. **Dobry commit message** - jasno opisuj CO i DLACZEGO
3. **Commituj często** - łatwiej wrócić do poprzedniego stanu
4. **Testuj przed commitem** - nie commituj broken code

### Gałęzie

1. **Krótkie życie feature branches** - merguj często
2. **Nazywaj konsekwentnie** - `feature/`, `bugfix/`, `hotfix/`
3. **Usuwaj zmergowane gałęzie** - utrzymuj porządek
4. **Jeden branch = jedna funkcjonalność**

### Remote

1. **Pull przed push** - zawsze aktualizuj lokalnie
2. **Rebase zamiast merge** - czystsza historia
3. **Force push ostrożnie** - używaj `--force-with-lease`
4. **Nie rebase public branches** - tylko lokalne/feature branches

### Historia

1. **Czysta historia** - używaj rebase i squash
2. **Sensowne messages** - nie "WIP", "fix", "update"
3. **Interactive rebase przed PR** - uporządkuj commity
4. **Nie zmieniaj historii po push** - chyba że feature branch

## Troubleshooting

### Przypadkowo usunąłem commit

```bash
git reflog
git checkout commit-hash
git checkout -b recovery
```

### Mam konflikty przy rebase

```bash
# Rozwiąż konflikty w plikach
git add resolved-files
git rebase --continue

# Lub pomiń ten commit
git rebase --skip

# Lub anuluj cały rebase
git rebase --abort
```

### Chcę cofnąć git push

```bash
# Jeśli nikt jeszcze nie pulled
git reset --hard HEAD~1
git push --force-with-lease

# Jeśli inni już pulled - użyj revert
git revert HEAD
git push
```

### Zapisałem wrażliwe dane w commicie

```bash
# Usuń plik i przepisz historię
git rm --cached secrets.txt
echo "secrets.txt" >> .gitignore
git commit --amend --no-edit

# Lub dla starszych commitów
git filter-branch --tree-filter 'rm -f secrets.txt' HEAD

# Lub użyj git-filter-repo (zalecane)
git-filter-repo --path secrets.txt --invert-paths
```

## Zasoby

- `git help <command>` - dokumentacja komendy
- `man git` - pełna dokumentacja
- https://git-scm.com/docs - oficjalna dokumentacja
- https://learngitbranching.js.org/ - interaktywna nauka

---

## Quick Reference Card

```bash
# Podstawy
git init                    # nowe repo
git clone <url>             # klonuj repo
git status                  # status
git add <file>              # stage
git commit -m "msg"         # commit
git push                    # wyślij do remote
git pull                    # pobierz z remote

# Branches
git branch                  # lista
git checkout -b <name>      # nowa gałąź
git merge <branch>          # merge
git branch -d <name>        # usuń

# Historia
git log                     # historia
git log --oneline          # skrócona historia
git diff                    # zmiany
git show <commit>          # pokaż commit

# Cofanie
git reset --soft HEAD~1     # cofnij commit
git restore <file>          # cofnij zmiany
git revert <commit>         # revert commit

# Stash
git stash                   # schowaj
git stash pop              # przywróć

# Remote
git remote -v              # lista remote
git fetch                  # pobierz zmiany
git push -u origin main    # push z tracking
```
