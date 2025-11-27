# SPRAWOZDANIE AISD - grupa laboratoryjna nr 7:

## Data: 27.11.2025
- ## Autorzy wykonanych poniżej algorytmów:
    - Bartłomiej Podstawek nr indeksu - 184285.
    - Maria Panek nr indeksu - 184275.

## Tematy otrzymanych zadań:

    - Zadanie 3.2 – analiza programu (zadanie 3.2), dodanie licznika operacji, analiza położenia
    dominanty względem min/max oraz procentowego udziału.
    
    - Zadanie 3.3 – analiza programu (wersja 3.3), dodanie licznika operacji, sprawdzenie
    położenia dominanty oraz wyznaczenie anty-dominanty.
    
## Kod do zadania (3.2);

```C++
#include <iostream>
#include <cstdlib>
#include <ctime>
#include <iomanip>
#include <cmath>

using namespace std;

int main()
{
    const int N = 200;
    int D[N], i, j, L, W, maxL, maxW;

    // Zmienne do zadania:
    long long lo = 0; // licznik operacji
    int minVal = 100, maxVal = -1;

    // Generujemy dane D[ ]
    srand(time(NULL));
    for (i = 0; i < N; i++)
        D[i] = rand() % 100;
    
        if (D[i] < minVal) minVal = D[i];
        if (D[i] > maxVal) maxVal = D[i];

    // Wyszukujemy najczęstszą wartość
    maxL = 0;
    maxW = D[0] - 1;

    for (i = 0; i < N - maxL; i++)
    {
        lo++;

        W = D[i];

        lo++;

        if (maxW != W)
        {
            L = 1;
            for (j = i + 1; j < N; j++)
                lo++;
                if (D[j] == W) { L++; }
            
            lo++;
            if (L > maxL)
            {
                maxL = L;
                maxW = W;
            }
        }
    }

    // Wypisanie tablicy
    for (i = 0; i < N; i++)
        if (D[i] == maxW)
            cout << " >" << setw(2) << D[i];
        else
            cout << setw(4) << D[i];

    cout << endl << endl;

    // Podstawowy wynik
    cout << "Dominanta (najczesciej wystepujaca wartosc): " << maxW << endl;
    cout << "Liczba wystapien: " << maxL << endl;

    // Liczba operacji
    cout << "Liczba operacji (lo): " << lo << endl;

    // Czy wartosc jest blizej min czy max
    cout << "Min w tablicy: " << minVal << endl << "Max w tablicy: " << maxVal << endl;
    int distMin = abs(maxW - minVal);
    int distMax = abs(maxW - maxVal);

    cout << "Odleglosc od min: " << distMin << endl;
    cout << "Odleglosc od max: " << distMax << endl;

    if (distMin < distMax)
        cout << "Wniosek: Dominanta jest blizej wartosci ! MINIMALNEJ !" << endl << endl;
    else if (distMin > distMax)
        cout << "Wniosek: Dominanta jest blizej wartosci ! MAKSYMALNEJ !" << endl << endl;
    else
        cout << "Wniosek: Dominanta jest posrodku (w rownej odleglosci)." << endl << endl;
    
    // Procent danych
    double procent = ((double)maxL / N) * 100.0;
    cout << "Dominanta stanowi " << fixed << setprecision(2) << procent << "% wszystkich danych." << endl << endl;

    return 0;
}
```
- ## Przykładowy rezultat / wynik uzyskany po uruchomieniu powyższego algorytmu (3.2):

 

```bash
 >19  75   3  59  47  36  40  23  39  26  35  80   1  73  39  15  14  98  95  38  66  63  85  33  53  29   2  15  99  82  64  29   5  89  68  49  33  74   7  66  18  20  56  83  27  57   7  70  52   5  39  62  94  32  34  69  43  96  91  87  95  27  87  51  79  26   0  39  53  86  18  62  50  49   5  97  77  95  79  50  92   5  31  42  14  95   9  74  24  31  12  68  50  40  97  74  16  96  15  78  20  92  35  81  59  42  74  12  52  98  80  70  31  53   4  91  35  96  77  33  49  43  56  52  98  77   0   3  31  15  84  41  99  36  44  21  15  39  14 >19  27  94   0  66  88  58  23  93  24  10  86  20  98  60  40  30 >19  72  74  71  36  38  57  89   5  57  56  60  48  77  63  56   8  95  64  78  40  21  74  81  82  47  34  98  72  90  73  78  35  40  52  11  75  60  76  26  13   8  50  81

Dominanta (najczesciej wystepujaca wartosc): 19
Liczba wystapien: 1
Liczba operacji (lo): 20392
Min w tablicy: -1867906996
Max w tablicy: -1
Odleglosc od min: 1867907015
Odleglosc od max: 20
Wniosek: Dominanta jest blizej wartosci ! MAKSYMALNEJ !

Dominanta stanowi 0.50% wszystkich danych.
```

# Kod do zadania (3.3)

```C++
#include <iostream>
#include <iomanip>
#include <cstdlib>
#include <ctime>

using namespace std;

const int N = 200;

int main()
{
    int D[N], *L, i, nL, maxD, minD, maxL, maxp;
    int minL, minp;
    long long lo = 0;
    
    srand(time(NULL));

    for (i = 0; i < N; i++) 
        D[i] = -0 + (rand() % 100);

    cout << "Tablica D: " << endl;
    for (i = 0; i < N; i++) 
        cout << setw(4) << D[i];
    cout << endl << endl; 

    if (D[0] > D[1])
    {
        minD = D[1]; 
        maxD = D[0];
    }
    else 
    {
        minD = D[0]; 
        maxD = D[1];
    }

    lo += 1;

    for (i = 2; i < N; i += 2)
    {
        lo++;
        if (D[i] > D[i + 1])
        {
            lo++;
            if (D[i] > maxD) { maxD = D[i]; lo++; }
            if (D[i + 1] < minD) { minD = D[i + 1]; lo++; }
        }
        else
        {
            lo++;
            if (D[i] < minD) { minD = D[i]; lo++; }
            if (D[i + 1] > maxD) { maxD = D[i + 1]; lo++; }
        }
    }

    nL = maxD - minD + 1;
    L = new int[nL];
    
    lo++;
    for (i = 0; i < nL; i++) 
        L[i] = 0;

    for (i = 0; i < N; i++) {
        L[D[i] - minD]++;
        lo += 2;
    }

    maxL = L[0]; 
    maxp = 0;

    minL = N + 1; 
    minp = -1;
    
    for (i = 0; i < nL; i++){
        lo++;
        if (L[i] > maxL)
        {
            maxL = L[i]; 
            maxp = i;
        }

        if (L[i] > 0) 
        {
            if (L[i] < minL) 
            {
                minL = L[i];
                minp = i;
                lo++;
            }
        }
    }

    int wartoscDominanty = maxp + minD;
    cout << "Dominanta (cyfra / wartosc): " << wartoscDominanty << endl;
    cout << "Liczba wystapien: " << maxL << endl;
    
    cout << "Liczba operacji arytmetycznych (zmienna lo): " << lo << endl;
    
    int distMin = abs(wartoscDominanty - minD);
    int distMax = abs(wartoscDominanty - maxD);
    
    cout << "c) Min zbioru: " << minD << ", Max zbioru: " << maxD << endl;
    cout << " Odleglosc dominanty od min: " << distMin << endl;
    cout << " Odleglosc dominanty od max: " << distMax << endl;
    
    if (distMin < distMax) cout << " Wniosek: Blizej MINIMUM." << endl;
    else if (distMin > distMax) cout << " Wniosek: Blizej MAXIMUM." << endl;
    else cout << " Wniosek: Posrodku." << endl;

    if (minp != -1)
    {
        int wartoscAnty = minp + minD;
        cout << " Anty-dominanta: " << wartoscAnty << endl;
        cout << " Liczba wystapien: " << minL << endl;
    }
    else
    {
        cout << " Nie znaleziono anty-dominanty " << endl;
    }

    cout << endl;
    
    delete [] L;
    
    return 0;
}
```

- ## Przykładowy rezultat / wynik uzyskany po uruchomieniu powyższego algorytmu (3.3):

```bash
Tablica D: 
  39  76  22  82  14  93  53  77  93  39   7  48  78  14  61  74  85   8  20  59  92   0  82  91  56  47  47  12  64  25  47   4  47  82  32  58  68  53  10  17  20  86  48  41   3  87  88  89  78  99  49  66  39  99  76  51  71  14   7  92  49   9   7  56  20  70  30  30  58  43  85  94  18  80  84   9   6  69  94  75  14  30  11  40  53   2  20  67  17   5  75   8  95  52  68  37  93  37  93  23  82  72  27  48  56  45  59  59  53  84  15  46  67  41  29  39  61  44  99  67  60  90  84  90  49  64  41  62  66  53   4  64   8  71  30  88  55  60  90  82  31  49  10  87  41  87  95  33  35   5  78  24  30   9  45  17  38   1  11  43  92  75  91  33  30  43  72  72  33  93  37   2  46  69  40  69  98  57  91  56  80  87  95  23  68  39  54  47  85  89  40  60  43  18  62  44  46  63   5  82

Dominanta (cyfra / wartosc): 30
Liczba wystapien: 6
Liczba operacji arytmetycznych (zmienna lo): 708
c) Min zbioru: 0, Max zbioru: 99
 Odleglosc dominanty od min: 30
 Odleglosc dominanty od max: 69
 Wniosek: Blizej MINIMUM.
 Anty-dominanta: 0
 Liczba wystapien: 1
```

## Wnioski: 

Zadanie 3.2: Algorytm ten jest ulepszoną wersją metody siłowej (brute-force). Zastosowana optymalizacja w pętli (N - maxL) pozwala uniknąć części zbędnych porównań, jednak przy dużej ilości danych nadal jest mało wydajna.

Zadanie 3.3: To rozwiązanie jest najszybsze dla danych o znanym i niewielkim zakresie. Wykorzystanie tablicy liczników (metoda kubełkowa) eliminuje zagnieżdżone pętle.

## Konkluzja:

Wydajność: Algorytm z tablicą liczników (Zadanie 3.3) jest zdecydowanie najbardziej wydajny – osiąga złożoność liniową O(N), co widać po drastycznie niższej liczbie operacji (708 vs 20 000).

Zastosowanie: Metoda z Zadania 3.2 sprawdza się tylko na małych zbiorach danych. Metoda z Zadania 3.3 jest idealna, gdy znamy zakres wartości (np. oceny, wiek), ale zużywa więcej pamięci RAM.
