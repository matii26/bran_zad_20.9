# bran_zad_20.9


#include <iostream>
#include <vector>
#include <algorithm>
#include <fstream>
#include <cstdlib>
#include <ctime>

using namespace std;

/*
Sortuje podany wektor liczb w porządku rosnącym.
nazwa funkcji: sortuj
argumenty funkcji: 
- liczby - wektor liczb całkowitych
wartość zwracana przez funkcję: brak
*/
void sortuj(vector<int>& liczby) {
    sort(liczby.begin(), liczby.end());
}

/*
Wyszukuje wartość w podanym wektorze liczb metodą liniową.
nazwa funkcji: wyszukajWartosc
argumenty funkcji: 
- liczby - wektor liczb całkowitych
- wartosc - liczba do wyszukania
wartość zwracana przez funkcję: indeks liczby w wektorze (jeśli znaleziono), -1 w przeciwnym wypadku
*/
int wyszukajWartosc(const vector<int>& liczby, int wartosc) {
    for (size_t i = 0; i < liczby.size(); ++i) {
        if (liczby[i] == wartosc) {
            return i; // Zwraca indeks znalezionej liczby
        }
    }
    return -1; // Jeśli nie znaleziono
}

/*
Oblicza medianę dla posortowanego wektora liczb.
nazwa funkcji: mediana
argumenty funkcji: 
- liczby - wektor liczb całkowitych (posortowany)
wartość zwracana przez funkcję: mediana liczb w postaci liczby zmiennoprzecinkowej
*/
double mediana(const vector<int>& liczby) {
    size_t n = liczby.size();
    if (n % 2 == 0) {
        return (liczby[n / 2 - 1] + liczby[n / 2]) / 2.0;
    } else {
        return liczby[n / 2];
    }
}

/*
Zapisuje posortowany wektor liczb do pliku o podanej nazwie.
nazwa funkcji: zapiszDoPliku
argumenty funkcji: 
- liczby - wektor liczb całkowitych
wartość zwracana przez funkcję: brak
*/
void zapiszDoPliku(const vector<int>& liczby) {
    ofstream plik("twoje_imie_i_pierwsza_litera_nazwiska.txt");
    if (plik.is_open()) {
        for (int liczba : liczby) {
            plik << liczba << endl;
        }
        plik.close();
    } else {
        cerr << "Nie można otworzyć pliku do zapisu!" << endl;
    }
}

int main() {
    vector<int> liczby;
    char odpowiedz;
    cout << "Czy wczytać z pliku? (t/n): ";
    cin >> odpowiedz;

    if (odpowiedz == 't' || odpowiedz == 'T') {
        string nazwaPliku;
        cout << "Podaj nazwę pliku: ";
        cin >> nazwaPliku;
        ifstream plik(nazwaPliku);

        if (plik.is_open()) {
            int liczba;
            while (plik >> liczba) {
                liczby.push_back(liczba);
            }
            plik.close();
        } else {
            cerr << "Nie można otworzyć pliku!" << endl;
            return 1;
        }
    } else {
        srand(time(0));
        for (int i = 0; i < 100; ++i) {
            liczby.push_back(rand() % 999 + 1);
        }
    }

    // Sortowanie
    sortuj(liczby);

    // Wyświetlanie posortowanych wartości
    cout << "Posortowane wartości: ";
    for (int liczba : liczby) {
        cout << liczba << " ";
    }
    cout << endl;

    // Wyszukiwanie wartości
    int szukanaWartosc;
    cout << "Podaj wartość do wyszukania: ";
    cin >> szukanaWartosc;
    int indeks = wyszukajWartosc(liczby, szukanaWartosc);
    if (indeks != -1) {
        cout << "Znaleziono wartość " << szukanaWartosc << " na indeksie " << indeks << "." << endl;
    } else {
        cout << "Nie znaleziono wartości " << szukanaWartosc << "." << endl;
    }

    // Obliczanie mediany
    cout << "Mediana: " << mediana(liczby) << endl;

    // Zapis do pliku
    zapiszDoPliku(liczby);

    return 0;
}
