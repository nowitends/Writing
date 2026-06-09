# Praktyczna Mechanika Kwantowa

## Spis treści proponowanych notatek laboratoryjnych

## 0. Wprowadzenie: po co są te notatki?

0.1. Mechanika kwantowa jako teoria modeli, nie katalog wzorów
0.2. Co znaczy „praktyczna” mechanika kwantowa?
0.3. Rola Mathematiki: rachunek symboliczny, obliczenia numeryczne, wizualizacja
0.4. Jak czytać równanie Schrödingera?
0.5. Jak czytać wykres funkcji falowej?
0.6. Jednostki, skale i sanity checks: eV, nm, masa efektywna
0.7. Stały schemat pracy laboratoryjnej
0.8. Typowy raport z ćwiczenia: teoria, model, kod, wynik, interpretacja

W materiałach organizacyjnych wyraźnie pojawia się nacisk na pracę laboratoryjną w Mathematice, ładne i czytelne wykresy, poprawne jednostki, masę efektywną oraz konieczność rozróżniania eV, nm i jednostek SI. 

Przykładowe okno kodu, które może pojawiać się już we wstępie:

```wolfram
ClearAll[energyEV];

hbarSI = 1.054571817*10^-34;
meSI = 9.1093837015*10^-31;
eVSI = 1.602176634*10^-19;

energyEV[n_, aNM_, mRel_: 1] :=
  (hbarSI^2 Pi^2 n^2)/(2 (mRel meSI) (aNM 10^-9)^2)/eVSI;

Table[energyEV[n, 8], {n, 1, 5}]
```

---

# Część I. Narzędzia i język mechaniki kwantowej

## 1. Mathematica jako laboratorium mechaniki kwantowej

1.1. Notatnik Mathematica jako zeszyt laboratoryjny
1.2. Definiowanie funkcji, parametrów i jednostek
1.3. Rachunek symboliczny: `Simplify`, `FullSimplify`, `Assumptions`
1.4. Rachunek numeryczny: `N`, `SetPrecision`, `FindRoot`, `NSolve`, `NDSolve`
1.5. Wykresy: `Plot`, `ListPlot`, `DensityPlot`, `DensityPlot3D`, `Manipulate`
1.6. Praca z liczbami zespolonymi
1.7. Najczęstsze błędy: brak założeń, złe jednostki, złe zakresy, nieczytelne wykresy
1.8. Jak sprawdzać wynik kodu fizycznie?

```wolfram
ClearAll[x, a, n, psi];

psi[n_, x_, a_] := Sqrt[2/a] Sin[n Pi (x + a/2)/a];

FullSimplify[
  Integrate[psi[n, x, a]^2, {x, -a/2, a/2}],
  Assumptions -> a > 0 && Element[n, PositiveIntegers]
]
```

## 2. Funkcja falowa, prawdopodobieństwo i normalizacja

2.1. Funkcja falowa jako obiekt matematyczny i fizyczny
2.2. Interpretacja Borna: $|\psi(x)|^2$
2.3. Normalizacja funkcji falowej
2.4. Wartości oczekiwane
2.5. Niepewność pomiaru obserwabli
2.6. Warunki brzegowe i ich sens fizyczny
2.7. Stany związane i stany rozproszeniowe
2.8. Co oznacza „rozwiązanie równania Schrödingera”?

---

# Część II. Jednowymiarowe układy kwantowe

## 3. Cząstka w nieskończonej studni potencjału

3.1. Sytuacja fizyczna: cząstka uwięziona w pudełku
3.2. Dwie konwencje studni: $x\in[0,a]$ oraz $x\in[-a/2,a/2]$
3.3. Stacjonarne równanie Schrödingera
3.4. Warunki brzegowe i kwantowanie energii
3.5. Funkcje własne i ich normalizacja
3.6. Parzystość funkcji falowych
3.7. Poziomy energetyczne w eV
3.8. Wizualizacja $\psi_n(x)$ oraz $|\psi_n(x)|^2$
3.9. Zależność energii od szerokości studni
3.10. Masa efektywna i przykład GaAs

Ten rozdział odpowiada pierwszej liście, gdzie studenci mają ręcznie wyprowadzić funkcję falową i energię dla nieskończonej studni, a następnie wygenerować wykresy energii, funkcji falowych i modułów funkcji falowych. 

## 4. Skończona studnia potencjału

4.1. Różnica między studnią nieskończoną i skończoną
4.2. Rozwiązania oscylacyjne wewnątrz studni
4.3. Rozwiązania zanikające w barierze
4.4. Warunki zszywania funkcji falowej
4.5. Równania transcendentalne dla energii
4.6. Parzyste i nieparzyste stany związane
4.7. Numeryczne szukanie poziomów energetycznych
4.8. Liczba stanów związanych a głębokość studni
4.9. Wizualizacja funkcji falowych dla skończonej liczby stanów
4.10. Kontrola wyniku: granica głębokiej studni

## 5. Bariery potencjału i tunelowanie

5.1. Cząstka padająca na barierę
5.2. Fala padająca, odbita i transmitowana
5.3. Współczynniki odbicia $R$ i transmisji $T$
5.4. Tunelowanie dla $E<V_0$
5.5. Przypadek $E>V_0$
5.6. Zależność transmisji od szerokości bariery
5.7. Sens fizyczny wykładniczego tłumienia
5.8. Praca z funkcjami zespolonymi w Mathematice
5.9. Wykresy $T(E)$ dla kilku szerokości bariery
5.10. Interpretacja: czego nie wolno rozumieć klasycznie?

Ten zakres odpowiada liście 2, gdzie pojawia się pojedyncza bariera, transmisja $T(E)$, szerokości barier z zakresu kilku nm, a także osobna uwaga o problemach Mathematiki ze sprzężeniami zespolonymi i $|\psi|^2$. 

## 6. Metoda macierzy przejścia

6.1. Po co wprowadzać macierze przejścia?
6.2. Jedna granica potencjału jako macierz
6.3. Propagacja w obszarze stałego potencjału
6.4. Pojedyncza bariera w formalizmie macierzowym
6.5. Podwójna bariera potencjału
6.6. Rezonansowe tunelowanie
6.7. Funkcja falowa w warunku $T(E)=1$
6.8. Część rzeczywista, część urojona i $|\psi|^2$
6.9. Numeryczne wyszukiwanie energii rezonansowych
6.10. Modelowanie nanostruktur półprzewodnikowych

---

# Część III. Metody numeryczne i struktury periodyczne

## 7. Równania transcendentalne i metoda Newtona-Raphsona

7.1. Dlaczego równania kwantowe często nie mają prostych rozwiązań?
7.2. Równanie $\tan x=x$ jako laboratorium numeryczne
7.3. Iteracja Newtona-Raphsona
7.4. Precyzja obliczeń: `SetPrecision` i `WorkingPrecision`
7.5. Porównanie własnej implementacji z `FindRoot`
7.6. Dobór punktu startowego
7.7. Zbieżność, brak zbieżności i fałszywe rozwiązania
7.8. Jak dokumentować obliczenie numeryczne?

```wolfram
ClearAll[x, newtonList];

newtonList[expr_, {var_, x0_}, steps_Integer?NonNegative] :=
  NestList[
    # - (expr /. var -> #)/(D[expr, var] /. var -> #) &,
    x0,
    steps
  ];

N[newtonList[Tan[x] - x, {x, 4.5`50}, 8], 30]

FindRoot[Tan[x] == x, {x, 4.5}, WorkingPrecision -> 50]
```

## 8. Supersieci i model Kroniga-Penneya

8.1. Od pojedynczej bariery do potencjału periodycznego
8.2. Studnia + bariera jako komórka elementarna
8.3. Warunek Blocha
8.4. Relacja dyspersji $E(k)$
8.5. Pasma dozwolone i przerwy energetyczne
8.6. Numeryczne wyznaczanie energii dla zadanych wartości wektora falowego
8.7. Rola szerokości studni i bariery
8.8. Wykres pasmowy jako wynik fizyczny, nie dekoracja
8.9. Kontrola: symetria względem $k=0$
8.10. Od supersieci do fizyki ciała stałego

Lista 3 zawiera metodę Newtona-Raphsona, porównanie z `FindRoot` oraz numeryczne wyznaczanie energii w supersieci z powtarzających się studni i barier. 

---

# Część IV. Potencjały ciągłe i oscylator harmoniczny

## 9. Różne profile potencjałów

9.1. Dlaczego prostokątna bariera to tylko pierwszy model?
9.2. Potencjał prostokątno-trójkątny
9.3. Potencjał trapezowy
9.4. Potencjał paraboliczny
9.5. Potencjał kosinusowy
9.6. Kwantowy „pryzmat”
9.7. Zszywanie rozwiązań numerycznych
9.8. Wykres profilu potencjału razem z funkcją falową
9.9. Re[$\psi$], Im[$\psi$] i $|\psi|^2$
9.10. Interpretacja: gdzie fala zwalnia, gdzie zanika, gdzie interferuje?

## 10. Kwantowy oscylator harmoniczny

10.1. Dlaczego oscylator harmoniczny jest fundamentalny?
10.2. Hamiltonian oscylatora
10.3. Równanie Schrödingera dla oscylatora
10.4. Wartości własne energii
10.5. Funkcje własne i wielomiany Hermite’a
10.6. Parzystość stanów oscylatora
10.7. Wykresy funkcji falowych i gęstości prawdopodobieństwa
10.8. Klasyczne punkty zwrotne a ogony kwantowe
10.9. Odtworzenie historycznego wykresu Schrödingera
10.10. Porównanie: studnia potencjału vs oscylator harmoniczny

## 11. Wielomiany ortogonalne w mechanice kwantowej

11.1. Skąd biorą się wielomiany specjalne?
11.2. Wielomiany Hermite’a
11.3. Wielomiany Legendre’a
11.4. Wielomiany Laguerre’a
11.5. Wielomiany Czebyszewa
11.6. Ortogonalność jako struktura fizyczna
11.7. Wbudowane funkcje Mathematiki
11.8. Jednolinijkowe generowanie rodzin wielomianów
11.9. Wykresy porównawcze
11.10. Powiązanie z oscylatorem, atomem wodoru i momentem pędu

Lista 4 obejmuje różne profile potencjału, oscylator harmoniczny, wielomiany Hermite’a, Czebyszewa, Legendre’a i Laguerre’a oraz odtworzenie wykresów funkcji falowych oscylatora z pracy Schrödingera. 

---

# Część V. Atom wodoru i moment pędu

## 12. Moment pędu w mechanice kwantowej

12.1. Operatorowy charakter momentu pędu
12.2. Operatory $\hat{L}_x,\hat{L}_y,\hat{L}_z$
12.3. Operator $\hat{L}^2$
12.4. Komutatory momentu pędu
12.5. Wspólne funkcje własne $\hat{L}^2$ i $\hat{L}_z$
12.6. Liczby kwantowe $l$ i $m$
12.7. Harmoniki sferyczne $Y_l^m(\theta,\phi)$
12.8. Sprawdzenie równań własnych w Mathematice
12.9. Wizualizacja harmonik sferycznych
12.10. Interpretacja geometryczna momentu pędu

## 13. Atom wodoru

13.1. Hamiltonian atomu wodoru
13.2. Separacja zmiennych we współrzędnych sferycznych
13.3. Równanie radialne i równanie kątowe
13.4. Liczby kwantowe $n,l,m$
13.5. Energia atomu wodoru
13.6. Serie widmowe: Lyman, Balmer, Paschen
13.7. Część radialna i wielomiany Laguerre’a
13.8. Część kątowa i harmoniki sferyczne
13.9. Jawne funkcje falowe dla $n=1,2,3$
13.10. Orbitale atomowe: przekroje 2D
13.11. Orbitale atomowe: wizualizacje 3D
13.12. Co naprawdę przedstawia orbital?

W Twoich ćwiczeniach pojawia się generowanie funkcji falowych atomu wodoru dla $n=1,2,3$, korzystanie z `SphericalHarmonicY`, rysowanie przekrojów orbitali przez `DensityPlot` oraz wizualizacja 3D przez `DensityPlot3D`. 

---

# Część VI. Nieoznaczoność, komutatory i interferencja

## 14. Wartości oczekiwane i niepewności pomiarowe

14.1. Obserwabla jako operator
14.2. Wartość oczekiwana $\langle \hat{A}\rangle$
14.3. Niepewność $\Delta A$
14.4. Przykład: położenie w nieskończonej studni
14.5. Przykład: pęd w nieskończonej studni
14.6. Iloczyn $\Delta x\Delta p$
14.7. Granica klasyczna a niezerowa niepewność
14.8. Interpretacja statystyczna, nie błąd aparatury

## 15. Komutatory

15.1. Czym jest komutator?
15.2. Komutator jako miara niekompatybilności obserwabli
15.3. Relacja $[\hat{x},\hat{p}_x]=i\hbar$
15.4. Komutatory z $\hat{L}^2$ i $\hat{L}_z$
15.5. Komutatory w Mathematice: reprezentacja operatorów różniczkowych
15.6. Co oznacza wynik zerowy?
15.7. Co oznacza wynik niezerowy?
15.8. Od komutatorów do zasady nieoznaczoności

## 16. Interferencja i doświadczenie z dwiema szczelinami

16.1. Superpozycja amplitud, nie prawdopodobieństw
16.2. Dwie szczeliny jako model interferencji
16.3. Pojedyncza szczelina jako granica
16.4. Trzy szczeliny i więcej szczelin
16.5. Szczeliny punktowe w 2D
16.6. Prążki interferencyjne jako mapa $|\psi(x,y)|^2$
16.7. Co niszczy interferencję?
16.8. Interpretacja: fala prawdopodobieństwa a pojedyncze zdarzenia

Lista 6 obejmuje obliczanie niepewności położenia i pędu, sprawdzanie zasady Heisenberga, komutatory oraz symulację prążków interferencyjnych dla dwóch i trzech szczelin. 

---

# Część VII. Formalizm Diraca i informatyka kwantowa

## 17. Przestrzeń Hilberta i notacja Diraca

17.1. Od funkcji falowej do wektora stanu
17.2. Ket $|\psi\rangle$ i bra $\langle\psi|$
17.3. Iloczyn skalarny
17.4. Baza ortonormalna
17.5. Rozkład stanu w bazie
17.6. Operatory jako macierze
17.7. Projektory i pomiar
17.8. Związek z wcześniejszymi funkcjami falowymi
17.9. Mathematica jako algebra liniowa mechaniki kwantowej

## 18. Kubity i proste układy kwantowe

18.1. Kubit jako najprostszy układ kwantowy
18.2. Stany $|0\rangle$ i $|1\rangle$
18.3. Superpozycja
18.4. Macierze Pauliego
18.5. Bramki kwantowe
18.6. Iloczyn tensorowy
18.7. Stany dwukubitowe
18.8. Splątanie
18.9. Stan Bella
18.10. Pomiar częściowy
18.11. Interpretacja: czego splątanie nie oznacza?

```wolfram
ket0 = {1, 0};
ket1 = {0, 1};

bell = (KroneckerProduct[ket0, ket0] +
    KroneckerProduct[ket1, ket1])/Sqrt[2];

FullSimplify[bell.bell]
```

Lista 7 w materiałach przechodzi do formalizmu Diraca, przestrzeni Hilberta i podstaw informatyki kwantowej, w tym kubitów i stanów splątanych. 

---

# Część VIII. Dynamika kwantowa

## 19. Zależne od czasu równanie Schrödingera

19.1. Od stanów stacjonarnych do ewolucji w czasie
19.2. Równanie Schrödingera zależne od czasu
19.3. Ewolucja swobodnej paczki falowej
19.4. Paczka Gaussa
19.5. Rozmywanie paczki falowej
19.6. Zderzenie paczki z barierą
19.7. Odbicie, transmisja i tunelowanie w czasie
19.8. Animacje $|\psi(x,t)|^2$
19.9. Zachowanie normy jako test poprawności
19.10. Fizyka wyniku, nie tylko filmik

## 20. Numeryczne rozwiązywanie TDSE

20.1. Dyskretyzacja przestrzeni i czasu
20.2. Warunki początkowe
20.3. Warunki brzegowe
20.4. Stabilność obliczeń
20.5. `NDSolve` w problemach kwantowych
20.6. Animacje przez `Animate` i `Manipulate`
20.7. Porównanie rozwiązań numerycznych z analitycznymi
20.8. Kontrola normy, energii i zakresu obliczeń

Lista 8 dotyczy dynamiki paczek falowych, zależnego od czasu równania Schrödingera oraz tworzenia symulacji pokazujących ewolucję $|\psi(x,t)|^2$. 

---

# Część IX. Pola zewnętrzne i metody przybliżone

## 21. Cząstka w polu magnetycznym

21.1. Sprzężenie minimalne
21.2. Potencjał wektorowy
21.3. Cechowanie
21.4. Pęd kanoniczny i pęd kinematyczny
21.5. Jednorodne pole magnetyczne
21.6. Problem Landaua
21.7. Redukcja do oscylatora harmonicznego
21.8. Poziomy Landaua
21.9. Degeneracja poziomów
21.10. Interpretacja fizyczna ruchu cyklotronowego

## 22. Rachunek zaburzeń

22.1. Po co stosujemy rachunek zaburzeń?
22.2. Hamiltonian niezaburzony i zaburzenie
22.3. Poprawki do energii pierwszego rzędu
22.4. Poprawki do energii drugiego rzędu
22.5. Poprawki do stanów własnych
22.6. Przypadek niezdegenerowany
22.7. Przypadek zdegenerowany — uwaga koncepcyjna
22.8. Efekt Starka w studni kwantowej
22.9. Porównanie rachunku zaburzeń z rozwiązaniem numerycznym
22.10. Zakres stosowalności metody

Lista 9 obejmuje potencjał wektorowy, cechowanie, pęd kanoniczny i kinematyczny, poziomy Landaua oraz rachunek zaburzeń wraz z efektem Starka. 

---

# Część X. Elementy fizyki ciała stałego

## 23. Sieci krystaliczne i przestrzeń odwrotna

23.1. Kryształ jako potencjał periodyczny
23.2. Sieć bezpośrednia
23.3. Komórka elementarna
23.4. Sieć odwrotna
23.5. Komórka Wignera-Seitza
23.6. Strefa Brillouina
23.7. Warunek Blocha
23.8. Od supersieci 1D do kryształów 2D i 3D
23.9. Wizualizacja sieci i stref Brillouina w Mathematice

## 24. Grafen jako praktyczny model kwantowy

24.1. Sieć plastra miodu
24.2. Dwie podsieci grafenu
24.3. Wektory sieciowe
24.4. Model ciasnego wiązania
24.5. Relacja dyspersji
24.6. Punkty Diraca
24.7. Liniowa dyspersja w pobliżu punktów Diraca
24.8. Elektrony jako efektywne bezmasowe fermiony Diraca
24.9. Wizualizacja struktury pasmowej grafenu
24.10. Granice modelu

Lista 10 obejmuje sieć krystaliczną, sieć odwrotną, komórkę Wignera-Seitza, strefy Brillouina, grafen, strukturę pasmową grafenu i efektywne fermiony Diraca. 

---

# Część XI. Struktury kwantowe w 3D

## 25. Równanie Schrödingera w trzech wymiarach

25.1. Od problemu 1D do problemu 3D
25.2. Współrzędne kartezjańskie i sferyczne
25.3. Laplasjan we współrzędnych sferycznych
25.4. Separacja zmiennych
25.5. Część radialna i część kątowa
25.6. Warunki regularności w początku układu
25.7. Warunki brzegowe na skończonym promieniu
25.8. Interpretacja radialnej gęstości prawdopodobieństwa

## 26. Kropki kwantowe i sferyczna studnia potencjału

26.1. Kropka kwantowa jako sztuczny atom
26.2. Sferyczna studnia potencjału
26.3. Funkcje Bessela sferyczne
26.4. Kwantowanie energii w 3D
26.5. Numeryczne szukanie zer funkcji specjalnych
26.6. Degeneracje poziomów
26.7. Wizualizacja stanów w 3D
26.8. Porównanie: atom wodoru, oscylator 3D, kropka kwantowa
26.9. Interpretacja fizyczna wyników

Lista 11 zawiera równanie Schrödingera w 3D, kropkę kwantową, sferyczną studnię potencjału, rozwiązania radialne związane z kulistymi funkcjami Bessela oraz numeryczne wyznaczanie energii. 

---

# Część XII. Projekty końcowe i standard raportu

## 27. Jak przygotować dobry projekt w Mathematice?

27.1. Wybór problemu fizycznego
27.2. Definicja modelu i założeń
27.3. Wersja analityczna, jeśli istnieje
27.4. Wersja numeryczna
27.5. Wykresy i animacje
27.6. Testy poprawności
27.7. Interpretacja wyniku
27.8. Granice stosowalności modelu
27.9. Estetyka i czytelność notatnika
27.10. Reprodukowalność obliczeń

## 28. Proponowane tematy projektów

28.1. Rezonansowe tunelowanie przez układ wielu barier
28.2. Animacja paczki falowej padającej na barierę
28.3. Porównanie skończonej i nieskończonej studni potencjału
28.4. Numeryczna analiza efektu Starka
28.5. Wizualizacja orbitali atomu wodoru
28.6. Struktura pasmowa grafenu
28.7. Poziomy Landaua
28.8. Kropka kwantowa w 3D
28.9. Interferencja dla wielu szczelin
28.10. Supersieć i powstawanie pasm energetycznych

---

# Dodatki

## Dodatek A. Szybki przewodnik po Mathematice

A.1. Definiowanie funkcji
A.2. Zmienne lokalne i globalne
A.3. Listy, tabele i mapowanie
A.4. Funkcje czyste
A.5. `Plot`, `ListPlot`, `DensityPlot`, `DensityPlot3D`
A.6. `Simplify`, `FullSimplify`, `Assumptions`
A.7. `Solve`, `NSolve`, `FindRoot`
A.8. `NDSolve`
A.9. `Manipulate` i `Animate`
A.10. Eksport wykresów

## Dodatek B. Stałe fizyczne i jednostki

B.1. Stała Plancka i zredukowana stała Plancka
B.2. Masa elektronu
B.3. Elektronowolt
B.4. Nanometr
B.5. Masa efektywna
B.6. Konwersje między SI, eV i nm
B.7. Jak nie zgubić czynników $10^{-9}$ i $10^{-19}$

## Dodatek C. Najczęstsze błędy studentów

C.1. Wykres w dżulach zamiast w eV
C.2. Szerokość w metrach zamiast w nm
C.3. Brak normalizacji funkcji falowej
C.4. Mylenie $\psi$ i $|\psi|^2$
C.5. Brak warunków brzegowych
C.6. Złe założenia w `Simplify`
C.7. Nieodróżnianie przypadku $E<V_0$ od $E>V_0$
C.8. Zbyt brzydkie i nieczytelne wykresy
C.9. Wynik numeryczny bez interpretacji
C.10. Kod, którego autor sam nie rozumie

## Dodatek D. Minimalny szablon raportu laboratoryjnego

D.1. Temat
D.2. Sytuacja fizyczna
D.3. Model i założenia
D.4. Równania
D.5. Implementacja w Mathematice
D.6. Wykresy
D.7. Kontrola wyniku
D.8. Interpretacja
D.9. Wnioski
D.10. Kod źródłowy

---

## Proponowany kręgosłup kursu

Najważniejszy ciąg pojęciowy powinien być taki:

$$
\text{funkcja falowa}
\rightarrow
\text{równanie Schrödingera}
\rightarrow
\text{warunki brzegowe}
\rightarrow
\text{kwantowanie energii}
\rightarrow
\text{wizualizacja}
\rightarrow
\text{tunelowanie}
\rightarrow
\text{metody numeryczne}
\rightarrow
\text{struktury kwantowe}.
$$

A najważniejszy ciąg kompetencji laboratoryjnych:

$$
\text{zdefiniuj model}
\rightarrow
\text{napisz równanie}
\rightarrow
\text{rozwiąż symbolicznie lub numerycznie}
\rightarrow
\text{narysuj}
\rightarrow
\text{sprawdź jednostki}
\rightarrow
\text{zinterpretuj}.
$$
