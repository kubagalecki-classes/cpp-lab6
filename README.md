# Laboratorium VI
## Wstęp
Dzisiejsze zajęcia dotyczyły będą algorytmów biblioteki STL.
Zanim przejdziemy do ich opisu, podsumujmy pokrótce poznane dotychczas zagadnienia, które pozwolą nam na zrozumienie zasady ich działania:
- szablony funkcji - wszystkie algorytmy dostępne w STL to szablony funkcji
- kontenery i iteratory - algorytmy operują na zakresach elementów kontenerów zdefiniowanych przez parę iteratorów
- przeciążanie operatorów - działanie algorytmów możemy 

## Anatomia std::algorytmu

#### Zadanie 1
Wygeneruj wektor losowych liczb całkowitych.
Wyświetl go.
Posortuj go rosnąco używając algorytmu `std::sort`.
Zweryfikuj poprawność działania algorytmu wyświetlając ponownie wektor.

## Funktory

#### Zadanie 2
Wygeneruj wektor losowych liczb całkowitych.
Wyświetl go.
Posortuj go malejąco używając algorytmu `std::sort` i odpowiedniego funktora.
Zweryfikuj poprawność działania algorytmu wyświetlając ponownie wektor.

### Lambdy

#### Zadanie 3

## Ćwiczenia
Poniżej zamieszczono zadania treningowe, rozwiązanie których pomoże poznać kilka nowych algorytmów oraz przećwiczyć pracę z szablonami funkcji dostępnymi w nagłówkach `algorithm` i `numeric`.
Kolejność zadań dobrana została zgodnie z rosnącym stopniem trudności (w opinii autora).
Zachęcamy czytelnika do wykonania jak największej ich liczby.
Zdecydowanie wskazane jest wykonanie przynajmniej pierwszego zadania z każdej kategorii poza ostatnią.

### Bezpośrednie zastosowania algorytmów
#### Ćwiczenie I - szukanie identycznych sąsiadów
Napisz program, który wcztuje z klawiatury ciąg znaków (`std::string`) i zwraca `1` jeżeli występują w nim 2 te same znaki pod rząd i `0` w innym wypadku.
użyj algorytmu `std::adjacent_find`.

#### Ćwiczenie II - szukanie podciągu
Napisz program, który wczytuje z klawiatury ciąg znaków, a następnie zwraca `1` jeżeli podany ciąg zawiera w sobie podciąg "piesek" lub "kotek" i `0` w innym wypadku.
Użyj algorytmu `std::search`.

#### Ćwiczenie III - odwracanie ciągów
Napisz program, który wczytuje z klawiatury ciąg znaków, a następnie drukuje go do konsoli w odwróconej kolejności.
Użyj algorytmu `std::reverse`.

#### Ćwiczenie IV - iloczyn skalarny
Stwórz 2 wektory liczb zmiennoprzecinkowych.
Oblicz ich iloczyn skalarny używając algorytmu `std::inner_product`.

### Łączenie algorytmów
#### Ćwiczenie V - sortowanie podciągu
Stwórz wektor losowych liczb całkowitych z przedziału \[0, 10\].
Znajdź w nim pierwsze wystąpienie liczby 7.
Posortuj elementy wektora występujące przed znalezioną liczbą 7 (lub cały wektor, jeżeli 7 nie występuje).
Użyj `std::find` i `std::sort`.

Przykład:
- input: \[3 2 1 7 9 7 8 10\]
- output: \[1 2 3 7 9 7 8 10\]

#### Ćwiczenie VI - idiom *remove-erase*
Stwórz wektor losowych liczb całkowitych z przedziału \[0, 10\].
Następnie usuń z niego wszystkie wystąpienia liczby 3.
Użyj algorytmu `std::remove` oraz metody wektora `erase`.
Spróbuj wykonać zadanie w 1 linijce (wyjąwszy stworzenie wektora).
Rozmiar (*size*) wektora powinien być po operacji mniejszy o liczbę wystąpień liczby 3.

#### Ćwiczenie VII - obrót względem wartości
Stwórz wektor losowych liczb całkowitych z przedziału \[0, 10\].
Znajdź w nim pierwsze wystąpienie liczby 7.
Przesuń elementy wektora występujące przed znalezioną liczbą 7 na koniec wektora (zachowaj ich kolejność).
Użyj `std::find` i `std::rotate`.

Przykład:
- input: \[3 2 1 7 9 7 8 10\]
- output: \[7 9 7 8 10 3 2 1\]

### Algorytmy przyjmujące funktory
#### Ćwiczenie VIII - sprawdzenie czy elementy z zakresu spełniają warunek logiczny
Stwórz wektor losowych liczb zmiennoprzecinkowych z przedziału \[-1, 1\].
Sprawdź, czy co najmniej jedna ze stworzonych liczb jest większa niż 0.9.
Użyj algorytmu `std::any_of`.

#### Ćwiczenie IX - sinus zakresu
Stwórz wektor losowych liczb zmiennoprzecinkowych z przedziału \[-1, 1\].
Stwórz drugi wektor tego samego rozmiaru i wypełnij go sinusami wartości z pierwszego wektora.
Użyj algorytmu `std::transform`.

#### Ćwiczenie X - sortowanie elementów wektora mniejszych od wartości
Stwórz wektor losowych liczb całkowitych z przedziału \[0, 10\].
Przestaw jego elementy tak, aby najpierw wystąpiły wszystkie liczby większe od 6 (poza tym wymaganiem mogą być one dowolnie przestawione).
Następnie posortuj część zakresu zawierającą elementy większe od 6.
Użyj `std::partition` i `std::sort`.

Przykład:
- input: \[1 10 2 9 3 8 4 7 5 6\]
- output (jeden z dopuszczalnych): \[7 8 9 10 3 1 5 6 2 4\]

### Zadanie trudniejsze
#### Ćwiczenie XI - indeksy sortowania
Napisz algorytm `sorted_indices`, o sygnaturze:
```C++
template < typename ConstIt, typename Comp >
std::vector< size_t > sorted_indices(ConstIt first, ConstIt last, Comp compare);
```
który zwraca indeksy elementów podanego zakresu `[first, last)` po jego posortowaniu przy użyciu funktora porównującego `compare`.
Algorytm nie powinien modyfikować zakresu.
Zachowanie jest analogiczne do napisania w MATLABie `[~, i] = sort(v)`.
Innymi słowy, poniższy kod powinien się wykonać:
```C++
std::vector<unsigned> v = { /* ... */ };
auto r = sorted_indices(v.begin(), v.end(), std::less<unsigned>{});
int a = 0;
for(size_t i = 0; i < v.size(); ++i)
{
    assert(a <= v[r[i]]);
    a = v[r[i]];
}
```

Przykład:
- input: \[1 10 2 9 3 8 4 7 5 6\]
- output: \[0 2 4 6 8 9 7 5 3 1\]

Podpowiedzi:
1. Załóż, że podany iterator jest losowego dostępu.
Iteratory losowego dostępu mają zdefiniowany operator `[ ]`, który pozwala na indeksowanie elementów następujących po danym iteratorze.
Na przykład:
```C++
std::vector<int> v = {1, 2, 3, 4, 5};
auto it = v.begin();
int a = it[2]; // a ma wartość 3
```
2. Funkcja `std::distance` zwraca odległość między dwoma iteratorami (np. dla `begin` i `end` będzie to rozmiar kontenera).
3. Możesz użyć algorytmu `std::iota` (z nagłówka `numeric`) do generacji wektora kolejnych rosnących liczb całkowitych (zwięźlejszy zapis niż pętla for).
4. W ostateczności możesz spojrzeć na [rozwiązanie](https://godbolt.org/z/3qaE8r).
