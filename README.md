# Controlling personalny – sieć placówek medycznych (MS Excel)

Model raportowania danych HR dla fikcyjnej sieci 4 placówek medycznych (Katowice, Kraków, Ustroń, Bielsko-Biała).
Jeden eksport z systemu kadrowo-płacowego zasila wszystkie raporty: kontrolę jakości danych, koszty pracy,
przegląd wynagrodzeń, budżet kosztów pracy na 2027 r. i dashboard dla zarządu.

> **Dane są w pełni fikcyjne** i spseudonimizowane (zamiast nazwisk jest tylko ID pracownika).
> Plik wymaga Excela 365 lub Excela w przeglądarce (funkcje dynamiczne: FILTER, SORT, XLOOKUP).

Plik można pobrać z repozytorium lub wyświetlić [poprzez podany link: (arkusz został wstawiony na platformę OneDrive)](https://1drv.ms/x/c/a75301766ab1be92/IQCPkNuFAIy1QKkbt49ZEaAAAT0mu95BxGFfrvnuKyhNclo?e=rU5SU4) 

Link do pobrania arkusza (Wtedy dopiero będzie można przetestować projekt w pełni, tryb online jest tylko do odczytu, nie zapewnia niestety interaktywności z arkuszem):
[link do pobrania](https://github.com/Skotee/Raportowanie-danych-HR-w-MS-Excel/raw/refs/heads/master/Controlling%20personalny.xlsx)

---

## Dashboard

<img width="1376" height="1071" alt="image" src="https://github.com/user-attachments/assets/5dbe3f9f-fe96-46af-b827-319c5f66405b" />


- 6 kafelków KPI: zatrudnienie i FTE, koszt pracodawcy, średnie wynagrodzenie i mediana, rotacja YTD, luka płacowa K/M, jakość danych
- 4 wykresy: koszt wg działów, ruch kadrowy miesiąc po miesiącu, stawki K vs M, struktura umów
- **Filtr placówki** z listy rozwijanej: kafelki i wykresy przeliczają się automatycznie
- Dla przykładu - widok dashboardu wybrany dla oddziału w Ustroniu

<img width="1337" height="1066" alt="image" src="https://github.com/user-attachments/assets/d9abef01-5a9e-4f06-a741-1ea0bdd05f78" />

---

## Problem biznesowy

Dział HR dostaje surowy eksport z systemu kadrowo-płacowego. Zanim powstanie raport, trzeba:
1. sprawdzić poprawność, kompletność i spójność danych,
2. policzyć pełny koszt pracodawcy,
3. ocenić wynagrodzenia względem siatki płac (w tym lukę płacową K/M),
4. przygotować budżet kosztów pracy i plan zatrudnienia na kolejny rok.

## Struktura skoroszytu

| Zakładka | Co zawiera |
|---|---|
| **O projekcie** | Opis, spis treści z linkami, legenda kolorów, uproszczenia |
| **Dashboard** | KPI i wykresy z filtrem placówki |
| **Parametry** | Wszystkie założenia: data raportu, płaca minimalna 2026, składki pracodawcy, siatka płac G1–G6, podwyżki 2027 |
| **Dane_Kadrowe** | Tabela 184 rekordów: dane źródłowe + kolumny wyliczane (stawka na pełny etat, koszt pracodawcy, staż, compa-ratio, uwagi QC) |
| **Kontrola_Jakości** | 10 reguł walidacji i automatyczna lista rekordów do poprawy |
| **Koszty_Pracy** | Koszt pracodawcy wg placówek i działów, struktura składek, sumy kontrolne |
| **Przegląd_Wynagrodzeń** | Widełki, compa-ratio, koszt wyrównania, luka płacowa K/M w grupach zaszeregowania |
| **Budżet_2027** | Podwyżki wg grup, nowe etaty, porównanie r/r, most kosztów 2026 → 2027 |

---

## Kontrola jakości danych

<img width="1793" height="706" alt="image" src="https://github.com/user-attachments/assets/012c6611-a98d-4c6d-af3f-bee2443d2c57" />

Reguły walidacji (m.in.):
- duplikaty ID, braki w polach obowiązkowych, nieprawidłowy wymiar etatu,
- wynagrodzenie poniżej płacy minimalnej (proporcjonalnie do etatu),
- niespójny status (zwolniony bez daty zwolnienia, aktywny z datą zwolnienia),
- zgodność z Kodeksem pracy: umowy terminowe > 33 mies. (art. 25¹ KP), okres próbny > 3 mies. (art. 25 KP).

**Wynik:** 13 rekordów do weryfikacji na 184, wskaźnik jakości danych 92,9%.
Błędy nie są poprawiane w Excelu, tylko flagowane, bo poprawka powinna trafić do systemu źródłowego.

---

## Koszty pracy

<img width="1480" height="697" alt="image" src="https://github.com/user-attachments/assets/ce7d6f7f-3b7c-4abf-aded-c6944b50cb39" />

- Koszt pracodawcy = brutto × (1 + narzut 21,98%: ZUS emerytalne, rentowe, wypadkowe, FP, FGŚP, PPK)
- Ujęcia: placówka, placówka × dział, struktura składników
- **Sumy kontrolne** między sekcjami (różnica = 0) potwierdzają, że raporty się uzgadniają

---

## Przegląd wynagrodzeń i luka płacowa

<img width="1805" height="657" alt="image" src="https://github.com/user-attachments/assets/5b5bafff-a1e8-4837-bcd1-26e418553ec2" />

- **Compa-ratio** = stawka na pełny etat / środek widełek grupy
- Lista osób poniżej widełek, posortowana od najniższego compa-ratio, oraz koszt wyrównania do minimum
- **Luka płacowa K/M** liczona w każdej grupie zaszeregowania z progiem 5%
  (dyrektywa UE 2023/970 o jawności wynagrodzeń). Przekroczenie progu oznacza „Wymaga oceny”.
- Rozróżnienie luki **nieskorygowanej** (całej firmy, zależnej od struktury zatrudnienia) i luki w grupach

---

## Budżet kosztów pracy 2027

<img width="1871" height="863" alt="image" src="https://github.com/user-attachments/assets/bb0fefaa-ef38-4444-8488-4daea265cd7d" />

- Baza: run-rate aktywnych pracowników × 12 miesięcy
- Podwyżki zróżnicowane wg grup zaszeregowania (parametry)
- Nowe etaty planowane jako FTE × liczba miesięcy w roku
- Most kosztów: 2026 → podwyżki → nowe etaty → 2027 (**+5,9% r/r**)

---

## Objaśnienie konkretnych Arkuszy

### Dashboard
Co przedstawia: podsumowanie dla zarządu na jednym ekranie.

Filtr placówki. Po wybraniu placówki zmieniają się kafelki i wykresy.

6 kafelków KPI:
Zatrudnienie: 161 osób, a pod spodem 153,8 FTE, czyli suma etatów.
Koszt pracodawcy miesięcznie: 1 989 517 zł (rocznie 23,87 mln).
Średnie wynagrodzenie na pełny etat: średnia i mediana. Mediana (8 535 zł) jest niższa od średniej, bo lekarze podnoszą średnią.
Rotacja od początku roku: 9,6% (15 odejść, 23 przyjęcia).
Luka płacowa K/M: nieskorygowana, plus liczba osób poniżej widełek.
Jakość danych: 92,9%, czyli 13 rekordów do poprawy.
4 wykresy: koszt wg działów, przyjęcia i odejścia miesiąc po miesiącu, średnia stawka K i M w działach, struktura umów (wykres kołowy).
Obliczenia pomocnicze (od wiersza 40): dane, z których rysują się wykresy. Są widoczne celowo, żeby dało się sprawdzić, skąd biorą się liczby.

### Parametry
Co przedstawia: wszystkie założenia modelu. To jedyne miejsce, w którym zmienia się liczby ręcznie.

Parametry ogólne: data raportu (30.09.2026), płaca minimalna 4806 zł (w notatce jest źródło), rok budżetu.
Składki pracodawcy: emerytalna, rentowa, wypadkowa, FP, FGŚP i PPK, razem 21,98%. To narzut doliczany do wynagrodzenia brutto.
Siatka płac G1–G6: od pracowników pomocniczych do lekarzy specjalistów. Każda grupa ma minimum, maksimum, środek widełek i planowaną podwyżkę na 2027.
Słowniki: listy placówek i działów, z których korzystają listy rozwijane i raporty.

### Dane_Kadrowe
Co przedstawia: surowy eksport z systemu kadrowego (np. enova365).

Kolumny A–M (dane źródłowe): ID, placówka, dział, stanowisko, grupa, płeć, data zatrudnienia, typ umowy, etat, wynagrodzenie zasadnicze, dodatek, status, data zwolnienia.
Kolumny N–V (wyliczane):
Brutto_mies: zasadnicze + dodatek.
Stawka_pełny_etat: brutto / etat, żeby dało się porównywać osoby na różnych etatach.
Aktywny_na_dzień: czy osoba pracuje w dniu raportu (1 albo 0). 184 rekordy minus zwolnieni daje 161 aktywnych.
Staż_lat, Koszt_pracodawcy_mies (brutto × 1,2198).
Środek_widełek, Compa_ratio, Pozycja_w_widełkach (Poniżej, W widełkach, Powyżej).
Uwagi_QC: opis błędów w danym wierszu. Wiersze z błędami mają różowe tło.

### Kontrola_Jakości
Co przedstawia: walidację danych przed raportowaniem.

10 reguł: przy każdej jest opis, podstawa prawna i liczba wykrytych przypadków, np. duplikat ID, poniżej płacy minimalnej, umowa terminowa ponad 33 miesiące (art. 25¹ KP), okres próbny ponad 3 miesiące.
Podsumowanie: 13 rekordów z błędami na 184, czyli wskaźnik jakości 92,9%.
Lista do weryfikacji: tworzy się automatycznie (ID, placówka, opis problemu). To gotowa lista „do wyjaśnienia z kadrami”.

### Koszty_Pracy
Co przedstawia: ile kosztuje zatrudnienie aktywnych pracowników.

Sekcja 1, wg placówki: osoby, FTE, fundusz brutto, narzuty, koszt miesięczny i roczny, średni koszt na etat, udział w całości. Najwięcej kosztują Katowice.
Sekcja 2, placówka × dział: tabela kosztów z kolumną „Nieprzypisane” dla rekordu bez działu, dzięki czemu sumy się zgadzają. Pod spodem jest suma kontrolna, która wynosi 0.
Sekcja 3, struktura kosztu: rozbicie na brutto i poszczególne składki, również z sumą kontrolną równą 0.

### Przegląd_Wynagrodzeń
Co przedstawia: materiał do corocznego przeglądu płac.

Sekcja 1, dla każdej grupy G1–G6: widełki, liczba osób, mediana, średnie compa-ratio, ile osób jest poniżej i powyżej widełek oraz koszt wyrównania (ile kosztowałoby podniesienie wszystkich do minimum). Do tego średnia stawka K i M, luka i ocena względem progu 5%. G5 (lekarze) ma 7,3%, więc oznaczenie „Wymaga oceny”.
Notka pod tabelą: wyjaśnia, że luka „Razem” (37,4%) jest nieskorygowana i wynika ze struktury zatrudnienia. Odwołuje się do art. 10 dyrektywy 2023/970.
Sekcja 2: lista 12 osób poniżej widełek, posortowana od najniższego compa-ratio. To kandydaci do podwyżek w pierwszej kolejności.

### Budżet_2027
Co przedstawia: plan kosztów pracy na przyszły rok.

Sekcja 1: miesięczny fundusz brutto wg działu i grupy, a pod spodem procent podwyżki dla każdej grupy (z Parametrów).
Sekcja 2: dla każdego działu zestawienie 2026 i 2027:
obecne FTE,
nowe etaty i liczba miesięcy, w których będą opłacane (żółte pola do zmiany, np. 2 etaty w Kardiologii od lipca, czyli 6 miesięcy),
koszt 2026, koszt 2027, różnica i dynamika.
Razem: 25,28 mln zł wobec 23,87 mln zł (+5,9%).
Sekcja 3, most kosztów: koszt 2026 (23,87 mln) + podwyżki (1,00 mln) + nowe etaty (0,41 mln) = koszt 2027 (25,28 mln). Obok jest wykres.

---

## Użyte techniki Excel

- **Formuły:** XLOOKUP, SUMIFS / COUNTIFS / AVERAGEIFS, SUMPRODUCT, FILTER, SORT, CHOOSECOLS, TEXTJOIN, YEARFRAC, EOMONTH, MEDIAN
- **Struktura:** tabele z odwołaniami strukturalnymi, nazwy zakresów, listy rozwijane (sprawdzanie poprawności danych), sumy kontrolne
- **Wizualizacja:** formatowanie warunkowe (flagi błędów, skale kolorów, paski danych), wykresy reagujące na filtr
- **Dobre praktyki modelowania:** wszystkie założenia w jednym arkuszu, brak wpisanych na sztywno liczb w formułach,
  kolorystyka komórek (niebieski = dane wejściowe, czarny = formuły, zielony = powiązania między arkuszami)

## Uproszczenia

- Pominięto limit 30-krotności dla składek emerytalno-rentowych oraz zwolnienia z FP/FGŚP (wiek 55/60+)
- Stopa składki wypadkowej przyjęta umownie
- Budżet nie obejmuje premii, nadgodzin, dyżurów ani nagród jubileuszowych

## Możliwe rozszerzenia

- Import eksportu z systemu HR przez Power Query
- Analiza absencji i nadgodzin
- Luka płacowa skorygowana o staż i stanowisko
- Wersja raportu w Power BI
