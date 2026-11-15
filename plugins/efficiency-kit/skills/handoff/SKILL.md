---
name: handoff
description: Use when the user says 'zrób handoff', 'handoff', or ends a session that produced results: writes HANDOFF.md and saves it to krzyszur/websites.
---

# Handoff

Cel: zamknąć sesję krótkim podsumowaniem, żeby kolejny czat startował od kilkuset słów zamiast całej rozmowy.

## 1. Napisz HANDOFF.md (po polsku, max ~400 słów)

```
# HANDOFF – <projekt> – <RRRR-MM-DD>
## Cel
## Stan (co jest zrobione, gdzie leżą pliki)
## Decyzje (z uzasadnieniem w 1 linii)
## Otwarte kwestie / ryzyka
## Następne kroki (kolejność)
## Prompt startowy do nowego czatu
```

Tylko fakty z sesji, bez powtarzania całej rozmowy. Jeśli projekt ma PROJECT.md, dodaj listę zmian do niego jako diff.

## 2. Zapisz w repo

- Repo: github.com/krzyszur/websites (lokalny klon tego repo).
- Ścieżka: `<projekt>/docs/HANDOFF.md` (nazwa projektu w kebab-case; nadpisz poprzedni handoff, historia zostaje w git).
- Jeśli folder projektu nie istnieje, utwórz `<projekt>/` z `docs/` i krótkim README.
- Commit: `handoff(<projekt>): <RRRR-MM-DD> <1 linia stanu>`, potem push.
- Bez sekretów i plików > 50 MB.

## 3. Gdy repo jest niedostępne

Powiedz to w jednej linii, wyślij HANDOFF.md jako plik do pobrania i podaj ścieżkę docelową w repo.

## 4. Zakończ

Pokaż prompt startowy do nowego czatu i zaproponuj „czas na nowy czat”.
