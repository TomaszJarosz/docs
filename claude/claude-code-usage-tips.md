# Claude Code - Praktyczne Tipy i Najlepsze Praktyki

Jak efektywnie pracować z Claude Code - sprawdzone techniki i workflow.

## Filozofia Pracy z Claude Code

### Co Claude Code Robi Najlepiej

✅ **Doskonale:**
- Pisanie i refaktoryzacja kodu
- Code review i znajdowanie bugów
- Pisanie testów
- Dokumentacja kodu
- Debugowanie i analiza błędów
- Tłumaczenie między językami programowania
- Wyjaśnianie kodu
- Automatyzacja powtarzalnych zadań

⚠️ **Z ograniczeniami:**
- Bardzo duże refaktoringi (lepiej małymi krokami)
- Operacje wymagające kontekstu całego projektu (limit tokenów)
- Real-time debugging (nie widzę runtime state)

❌ **Nie używaj do:**
- Zadań wymagających dostępu do internetu (bez MCP)
- Operacji na bazach produkcyjnych
- Destructive operations bez weryfikacji

## Podstawowe Zasady Efektywnej Komunikacji

### 1. Bądź Konkretny

❌ **Źle:**
```
Napraw to
```

✅ **Dobrze:**
```
W pliku src/auth.ts funkcja validateToken() nie obsługuje przypadku
gdy token jest expired. Dodaj sprawdzanie expiration time i zwracaj
odpowiedni błąd.
```

### 2. Podawaj Kontekst

❌ **Źle:**
```
Dodaj walidację
```

✅ **Dobrze:**
```
W formularzu rejestracji (src/components/RegisterForm.tsx) dodaj
walidację email i hasła:
- Email: format RFC 5322
- Hasło: min 8 znaków, 1 wielka litera, 1 cyfra, 1 znak specjalny
Użyj Zod do walidacji, błędy wyświetl pod inputem.
```

### 3. Dziel Duże Zadania

❌ **Źle:**
```
Zbuduj cały system autentykacji z JWT, refresh tokens, OAuth,
2FA, password reset, email verification i role-based access control.
```

✅ **Dobrze:**
```
Krok 1: Stwórz podstawową autentykację z JWT
Krok 2: Dodaj refresh tokens
Krok 3: Implementuj password reset
...
```

Lub:
```
Najpierw zrób podstawową autentykację JWT (login/logout/protected routes).
Potem powiemy sobie o pozostałych features.
```

### 4. Pytaj o Wyjaśnienia

✅ **Zawsze możesz:**
```
Zanim zaczniesz - wyjaśnij mi jak działa ten kod
```

```
Nie rozumiem dlaczego używasz tego pattern - wytłumacz
```

```
Jakie są alternatywne podejścia do tego problemu?
```

## Prompting Patterns (Sprawdzone Wzorce)

### Pattern 1: "Analizuj → Planuj → Wykonaj"

```
1. Przeanalizuj plik src/api/users.ts
2. Zaproponuj plan refaktoryzacji aby był bardziej testowalny
3. Jak zaaprobuje plan, wykonaj refaktoryzację
```

**Dlaczego działa:** Dajesz mi szansę zrozumieć kontekst przed działaniem.

### Pattern 2: "Pokaż Przykład"

```
Napisz testy dla funkcji calculateDiscount w src/utils/pricing.ts.

Przykład testu który mi się podoba:
[kod przykładu]

Zrób podobne dla pozostałych przypadków.
```

**Dlaczego działa:** Widzę Twój preferowany styl i konwencje.

### Pattern 3: "Iteracyjne Ulepszanie"

```
[Runda 1]
Napisz podstawową funkcję do parsowania CSV

[Runda 2]
Dodaj obsługę błędów i walidację

[Runda 3]
Dodaj support dla custom delimiterów

[Runda 4]
Zoptymalizuj dla dużych plików (streaming)
```

**Dlaczego działa:** Małe, kontrolowane kroki. Łatwiej testować i weryfikować.

### Pattern 4: "Zainspiruj się"

```
Zobacz jak jest zaimplementowane logowanie w src/services/logger.ts.

Zrób podobny serwis do cache'owania, zachowując ten sam pattern
i styl kodu.
```

**Dlaczego działa:** Zachowujesz konsystencję w projekcie.

### Pattern 5: "Debuguj ze Mną"

```
Mam błąd: [wklej błąd]

Kod który powoduje błąd: [ścieżka do pliku]

Co próbowałem: [lista rzeczy]

Pomóż mi zrozumieć co się dzieje i jak to naprawić.
```

**Dlaczego działa:** Pełny kontekst = szybsza diagnoza.

### Pattern 6: "Ekspert w Dziedzinie"

```
Jesteś ekspertem od performance w React. Przejrzyj komponent
src/components/DataTable.tsx i znajdź wszystkie miejsca gdzie
możemy poprawić wydajność. Wyjaśnij każdą optymalizację.
```

**Dlaczego działa:** Skupiam się na konkretnym aspekcie.

## Workflow Patterns (Sprawdzone Przepływy Pracy)

### Workflow 1: Feature Development

```bash
# 1. Planowanie
"Chcę dodać feature X. Jakie pliki będę musiał zmienić/stworzyć?
 Zaproponuj architekturę."

# 2. Implementacja (małymi krokami)
"Zacznijmy od modelu danych"
"Teraz dodaj API endpoint"
"Teraz frontend component"

# 3. Testy
"Napisz testy dla tego co stworzyliśmy"

# 4. Dokumentacja
"Dodaj dokumentację i aktualizuj README"

# 5. Review
"Przejrzyj cały feature - czy coś można ulepszyć?"
```

### Workflow 2: Bug Fixing

```bash
# 1. Reprodukcja
"Mam bug: [opis]. Pomóż znaleźć gdzie jest problem."

# 2. Analiza
"Przeanalizuj [plik] i wyjaśnij dlaczego to się dzieje"

# 3. Fix
"Napraw bug, zachowując istniejącą funkcjonalność"

# 4. Test
"Napisz test który weryfikuje że bug jest naprawiony"

# 5. Verify
"Sprawdź czy fix nie wprowadza regresji w innych miejscach"
```

### Workflow 3: Refactoring

```bash
# 1. Analiza
"Przeanalizuj [plik/moduł] i znajdź code smells"

# 2. Plan
"Zaproponuj plan refaktoryzacji (co i dlaczego)"

# 3. Testy (najpierw!)
"Przed refaktoryzacją - napisz testy dla obecnej funkcjonalności"

# 4. Refactor (małymi krokami)
"Refaktoryzuj funkcję X"
"Teraz funkcję Y"

# 5. Verify
"Uruchom testy - wszystko powinno przechodzić"
```

### Workflow 4: Code Review

```bash
# Jako reviewer
"Przejrzyj PR w plikach: [lista]. Szukaj:
 - Bugów
 - Security issues
 - Performance problems
 - Code style violations
 - Missing tests
 Sformatuj jako GitHub review comments."

# Jako author przed PR
"Zrób self-review moich zmian i powiedz co powinienem poprawić
 przed wysłaniem PR"
```

### Workflow 5: Learning Codebase

```bash
# Eksploracja nowego projektu
"Przeanalizuj strukturę projektu i wyjaśnij:
 - Jaka jest architektura
 - Jakie są główne moduły
 - Jak działa flow danych
 - Gdzie są punkty wejścia"

"Wyjaśnij mi jak działa feature X krok po kroku"

"Znajdź wszystkie miejsca gdzie jest używana funkcja Y"
```

## Praca z Kodem

### Dobre Praktyki

#### 1. Zawsze Podawaj Ścieżki

✅ **Dobrze:**
```
Zrefaktoryzuj funkcję getUserData w src/api/users.ts
```

❌ **Źle:**
```
Zrefaktoryzuj funkcję getUserData
```

#### 2. Wskaż Co Ma Zostać Zachowane

✅ **Dobrze:**
```
Zrefaktoryzuj, ale zachowaj:
- Obecny interface
- Error handling
- Backwards compatibility
```

#### 3. Określ Standard Jakości

✅ **Dobrze:**
```
Kod powinien:
- Mieć type safety (TypeScript strict mode)
- Być pokryty testami (min 80%)
- Mieć JSDoc dla publicznych funkcji
- Followować nasze style guide w docs/STYLE.md
```

#### 4. Poproś o Wyjaśnienia

✅ **Zawsze OK:**
```
Dodaj komentarze wyjaśniające dlaczego ten kod jest napisany w ten sposób
```

```
Po implementacji - wyjaśnij mi kluczowe decyzje które podjąłeś
```

### Praca z Błędami

#### Gdy Dostaniesz Error

```
Uruchomiłem kod i dostałem błąd:
[pełny stack trace]

Komenda którą uruchomiłem:
[komenda]

Kontekst:
[co próbowałem zrobić]
```

**Nie:**
```
Nie działa
```

#### Gdy Coś Działa Nieprawidłowo

```
Funkcja zwraca nieprawidłowy wynik.

Expected: [co powinno być]
Actual: [co jest]
Input: [jakie dane wejściowe]

Kod: src/utils/calculate.ts:42
```

### Praca z Dużymi Zmianami

#### Gdy Projekt Jest Duży

```
# Zamiast "przejrzyj cały projekt"
Przejrzyj moduł autentykacji (src/auth/**) i znajdź potencjalne
problemy z bezpieczeństwem.
```

```
# Zamiast "zrefaktoryzuj wszystko"
Zrefaktoryzuj najpierw src/api/users.ts, potem powiemy o kolejnych.
```

#### Strategia "Divide and Conquer"

```
# Krok 1: Przegląd
Przeanalizuj src/services/ i powiedz które pliki wymagają refaktoryzacji.

# Krok 2: Priorytetyzacja
Które są najważniejsze? Zaproponuj kolejność.

# Krok 3: Wykonanie
OK, zaczynamy od [plik1]
```

## Praca z Testami

### Pattern: Test-Driven Development

```bash
# 1. Napisz test (czerwony)
"Napisz test dla funkcji calculateShipping która:
 - Dla weight < 1kg zwraca 5.00
 - Dla 1-5kg zwraca 10.00
 - Dla >5kg zwraca 15.00 + 2.00 za każdy dodatkowy kg"

# 2. Implementuj (zielony)
"Teraz zaimplementuj funkcję aby testy przechodziły"

# 3. Refactor
"Zoptymalizuj implementację zachowując przejście testów"
```

### Pattern: Existing Code

```bash
"Napisz testy dla istniejącej funkcji validateEmail w src/utils/validation.ts.
 Pokryj wszystkie edge cases."
```

### Pattern: Test Coverage

```bash
"Przejrzyj plik src/api/orders.ts i napisz testy dla wszystkich
 funkcji które nie mają testów. Pokrycie powinno być >80%."
```

## Git Workflow z Claude

### Commit Messages

```bash
# Dobry prompt
"Zrobiłem zmiany w [pliki]. Wygeneruj commit message według
 Conventional Commits (feat/fix/docs/etc)."

# Claude generuje:
feat(auth): add email verification

- Implement email verification service
- Add verification email template
- Add verification endpoint
- Update user model with verified flag

Closes #123
```

### Code Review przed Commit

```bash
"Przed commitem - przejrzyj moje zmiany w src/ i powiedz czy
 widzisz jakieś problemy."
```

### Pre-commit Hook Ideas

```bash
"Zaproponuj pre-commit hook który:
 - Uruchamia testy
 - Sprawdza linting
 - Weryfikuje że commit message jest Conventional Commits
 - Blokuje commit jeśli coś nie przechodzi"
```

## Dokumentacja

### Pattern: Auto-Documentation

```bash
"Dodaj JSDoc/docstrings dla wszystkich publicznych funkcji w src/api/users.ts.
 Format:
 - Opis funkcji
 - @param z typami i opisem
 - @returns z opisem
 - @throws jeśli applicable
 - @example z konkretnym przykładem użycia"
```

### Pattern: README Generation

```bash
"Wygeneruj README.md dla tego projektu zawierający:
 - Opis projektu
 - Installation
 - Usage z przykładami
 - API documentation
 - Development guide
 - Contributing guidelines"
```

### Pattern: Architecture Documentation

```bash
"Wygeneruj docs/ARCHITECTURE.md opisujący:
 - Strukturę projektu
 - Główne moduły i ich odpowiedzialności
 - Flow danych
 - Najważniejsze decyzje architektoniczne i dlaczego"
```

## Debugowanie

### Efektywne Debugowanie z Claude

#### 1. Pełny Kontekst

```
Problem: [konkretny opis]
Błąd: [pełny error message + stack trace]
Kod: [ścieżka do pliku lub fragment]
Co próbowałem: [lista prób]
Environment: [Node 18, Ubuntu 22.04, etc]
```

#### 2. Systematyczne Podejście

```
"Pomóż mi debugować ten problem systematycznie:

1. Najpierw przeanalizuj kod i wyjaśnij co powinno się dziać
2. Potem sprawdź gdzie może być problem
3. Zaproponuj sposób diagnozowania (console.log, debugger, etc)
4. Gdy znajdziemy problem, zaproponuj fix"
```

#### 3. Interactive Debugging

```
[Po każdym kroku debugging podaję wyniki]

Ty: "Dodaj console.log przed linią 42 i powiedz co się wyświetla"
Ja: [wynik]
Ty: "OK, teraz sprawdź wartość X"
Ja: [wynik]
...iteracyjnie
```

## Performance Optimization

### Pattern: Profile → Analyze → Optimize

```bash
# 1. Identify
"Przeanalizuj src/components/DataGrid.tsx pod kątem performance.
 Znajdź potencjalne bottlenecki."

# 2. Measure
"Dodaj performance measurements aby zweryfikować problem"

# 3. Optimize
"Zoptymalizuj [konkretna funkcja/komponent]"

# 4. Verify
"Sprawdź czy optymalizacja nie zepsuje funkcjonalności (dodaj testy)"
```

### Pattern: Bundle Size

```bash
"Przeanalizuj bundle size:
 1. Jakie są największe dependencies?
 2. Co możemy tree-shake?
 3. Co można lazy-load?
 4. Zaproponuj konkretne optymalizacje"
```

## Bezpieczeństwo

### Security Review

```bash
"Przejrzyj kod pod kątem bezpieczeństwa:
 - SQL injection
 - XSS
 - CSRF
 - Authentication/Authorization issues
 - Sensitive data exposure
 - Dependency vulnerabilities

Dla każdego znaleziska:
 - Severity (Critical/High/Medium/Low)
 - Lokalizacja
 - Opis problemu
 - Jak naprawić"
```

### Secret Scanning

```bash
"Sprawdź czy w projekcie nie ma:
 - API keys
 - Passwords
 - Tokens
 - Private keys
 - Credentials

Jeśli znajdziesz - powiedz gdzie i zasugeruj jak powinno być."
```

## Anti-Patterns (Czego Unikać)

### ❌ Zbyt Ogólne Prośby

```
"Ulepsz kod"
"Zoptymalizuj to"
"Napraw błędy"
```

**Lepiej:**
```
"Zoptymalizuj pod kątem memory usage"
"Napraw błędy TypeScript"
"Ulepsz error handling"
```

### ❌ Bez Kontekstu

```
"Dlaczego to nie działa?"
```

**Lepiej:**
```
"Funkcja X w pliku Y zwraca undefined zamiast expected value Z.
 Input to A, B, C. Pomóż znaleźć problem."
```

### ❌ Wszystko Naraz

```
"Zrób całą aplikację e-commerce z backendem, frontendem, bazą danych,
 autentykacją, płatnościami, i deploy na AWS"
```

**Lepiej:**
```
"Zacznijmy od podstawowego API dla produktów. Najpierw model danych
 i podstawowe CRUD endpoints."
```

### ❌ Brak Weryfikacji

```
[Claude coś zrobił]
[Commituje bez sprawdzenia]
[Okazuje się że nie działa]
```

**Lepiej:**
```
[Claude coś zrobił]
[Testuję]
"Działa, ale mam pytanie o linię 42 - dlaczego..."
[Dyskusja/poprawki]
[Commit]
```

## Zaawansowane Techniki

### Chain of Thought Prompting

```
"Rozwiąż ten problem krok po kroku:

1. Najpierw wyjaśnij problem własnymi słowami
2. Wymień wszystkie możliwe rozwiązania
3. Oceń pros/cons każdego
4. Wybierz najlepsze i wyjaśnij dlaczego
5. Zaimplementuj"
```

### Few-Shot Learning

```
"Napisz funkcję do walidacji numeru telefonu.

Przykład podobnego kodu w naszym projekcie:
[przykład walidacji email]

Zrób analogicznie, zachowując ten sam styl i pattern."
```

### Constrained Output

```
"Wygeneruj kod który:
✓ MUSI używać TypeScript strict mode
✓ MUSI mieć error handling
✓ MUSI być <100 linii
✓ NIE MOŻE używać any
✓ NIE MOŻE mieć side effects
"
```

### Meta-Prompting

```
"Zanim odpowiesz, zastanów się:
- Czy dobrze rozumiem problem?
- Czy mam wszystkie potrzebne informacje?
- Jakie assumptions robię?

Jeśli czegoś brakuje - zapytaj mnie najpierw."
```

## Productywność Boostery

### 1. Używaj Slash Commands

```bash
# Zamiast opisywać za każdym razem
/review src/api/users.ts

# Custom command robi:
# - Code review
# - Znajdź bugs
# - Sprawdź best practices
# - Sugeruj improvements
```

### 2. Template Prompty

Stwórz `.claude/prompts/` z gotowymi:

**refactor.md:**
```
Zrefaktoryzuj {{file}} aby był:
- Bardziej czytelny
- Lepiej testowalny
- DRY (bez duplikacji)
- SOLID compliant

Wyjaśnij każdą znaczącą zmianę.
```

**security-check.md:**
```
Security review dla {{file}}:
- Input validation
- SQL injection
- XSS
- Authentication/Authorization
- Sensitive data handling
```

### 3. Iteracyjny Workflow

```bash
# Zamiast wszystkiego naraz:
"Napisz api + testy + docs dla feature X"

# Rób iteracyjnie:
[Runda 1] "Napisz API endpoint"
[Test] curl ...
[Runda 2] "Dodaj testy"
[Test] npm test
[Runda 3] "Dodaj dokumentację"
```

### 4. Wykorzystuj Context

```bash
# Przy dłuższej sesji:
"Pamiętasz funkcję X którą napisaliśmy wcześniej?
 Teraz zrób podobnie dla Y"

"Wykorzystując ten sam pattern co w poprzednim pliku..."
```

## Quick Tips

### Komunikacja

- 🎯 Bądź konkretny
- 📍 Podawaj lokalizacje (ścieżki do plików)
- 📝 Opisuj expected behavior
- ❓ Pytaj o wyjaśnienia
- 🔄 Iteruj (małe kroki)

### Kod

- ✅ Zawsze testuj
- 📚 Proś o dokumentację
- 🔍 Rób code review
- 🧪 TDD when possible
- 📦 Małe, atomowe zmiany

### Workflow

- 📋 Planuj przed działaniem
- 🔄 Iteruj, nie rób wszystkiego naraz
- ✓ Weryfikuj każdy krok
- 💾 Commituj często
- 📖 Dokumentuj decyzje

## Przykładowa Sesja (Best Practices)

```
Ty: "Chcę dodać feature: user notifications w aplikacji React+Node.js"

Claude: "OK, zaplanujmy to:
1. Backend: API endpoints + database model
2. Frontend: komponenty UI
3. Real-time: WebSocket integration
4. Testy
5. Dokumentacja

Od czego zaczynamy?"

Ty: "Zacznijmy od backend. Jakie endpointy będziemy potrzebować?"

Claude: [analiza + propozycja]

Ty: "OK, zróbmy database model najpierw"

Claude: [implementacja modelu]

Ty: "Świetnie. Teraz API endpoints dla CRUD notifications"

Claude: [implementacja]

Ty: "Dodaj testy dla tych endpoints"

Claude: [testy]

Ty: "Przejrzyj co zrobiliśmy i powiedz czy coś można ulepszyć"

Claude: [code review + sugestie]

Ty: "OK, implementuj sugestię #2"

Claude: [refactor]

Ty: "Wygeneruj commit message"

Claude: [conventional commits message]

Ty: "Teraz możemy przejść do frontendu"
...
```

## Zasoby

- **Dokumentacja:** https://code.claude.com/docs
- **GitHub Discussions:** https://github.com/anthropics/claude-code/discussions
- **Prompt Engineering Guide:** https://www.promptingguide.ai/

## Szybka Ściąga

```bash
✅ DO:
- Bądź konkretny i szczegółowy
- Podawaj pełen kontekst
- Dziel duże zadania na małe
- Testuj i weryfikuj
- Pytaj o wyjaśnienia
- Iteruj i ulepszaj

❌ DON'T:
- Ogólne prośby bez kontekstu
- Wszystko naraz
- Commitować bez testowania
- Zakładać że Claude wie wszystko o projekcie
- Pomijać edge cases
```

**Zapamiętaj:**
- Jestem narzędziem - Ty jesteś developerem
- Weryfikuj zawsze co robię
- Małe kroki = mniej błędów
- Komunikacja > magiczne myślenie
- Iteracja > perfekcja za pierwszym razem
