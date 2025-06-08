# Projekt Zaliczeniowy: System Zarządzania Biblioteką

**Autor:** [Mykyta , Kostiukov], [ 50745 ]

## Spis Treści
1.  [Wprowadzenie](#wprowadzenie)
2.  [Zaimplementowane Funkcjonalności](#zaimplementowane-funkcjonalności)
3.  [Struktura Projektu (Wzorzec MVC)](#struktura-projektu-wzorzec-mvc)
4.  [Technologie](#technologie)
5.  [Instrukcje Uruchomienia Aplikacji](#instrukcje-uruchomienia-aplikacji)
6.  [Kod Źródłowy Aplikacji](#kod-źródłowy-aplikacji)
7.  [Plik z Przykładowymi Danymi Wejściowymi](#plik-z-przykładowymi-danymi-wejściowymi)
8.  [Konfiguracja Docker](#konfiguracja-docker)
9.  [Galeria Zrzutów Ekranu](#galeria-zrzutów-ekranu)

## Wprowadzenie
Niniejszy projekt zaliczeniowy przedstawia prosty system zarządzania biblioteką, zrealizowany w języku Python z wykorzystaniem frameworka Flask. Aplikacja została zaprojektowana zgodnie z architektonicznym wzorcem Model-View-Controller (MVC), co zapewnia jej modularność, łatwość rozbudowy oraz czytelność kodu. Głównym celem projektu jest umożliwienie zarządzania kolekcją książek, autorami oraz osobami wypożyczającymi, a także śledzenie recenzji i wypożyczeń. Projekt spełnia założenia podstawowe oraz rozszerzone wymagania, takie jak dodanie dodatkowych modeli, walidacji danych oraz wsparcia dla Docker.

## Zaimplementowane Funkcjonalności
W ramach projektu zaimplementowano następujące kluczowe funkcjonalności:

-   **Zarządzanie Książkami (CRUD):** Pełny zestaw operacji (Tworzenie, Odczytywanie, Aktualizowanie, Usuwanie) dla rekordów książek.
-   **Zarządzanie Autorami (Implicitne):** Autorzy są tworzeni automatycznie w momencie dodawania nowej książki z nieistniejącym jeszcze autorem (pole tekstowe). Istniejący autorzy są ponownie wykorzystywani.
-   **Zarządzanie Osobami (Implicitne):** Osoby (użytkownicy pozostawiający recenzje lub wypożyczający książki) są tworzone automatycznie przy dodawaniu recenzji z nową nazwą (pole tekstowe). Istniejące osoby są ponownie wykorzystywane.
-   **Wyszukiwanie i Filtrowanie Książek:** Możliwość wyszukiwania książek na stronie głównej listy, zarówno po tytule, jak i nazwisku autora.
-   **System Recenzji i Ocen:**
    -   Szczegółowa strona dla każdej książki, wyświetlająca jej pełne informacje oraz wszystkie przypisane recenzje.
    -   Możliwość dodawania recenzji wraz z oceną (w skali 1-5 gwiazdek) dla danej książki.
    -   Automatyczne obliczanie i wyświetlanie średniej oceny dla każdej książki na stronie szczegółów.
-   **Śledzenie Wypożyczeń:** Podstawowe modele (`Borrowing`) umożliwiające rejestrację, która osoba wypożyczyła daną książkę (bez interfejsu użytkownika w tej wersji, dane dodawane skryptem).
-   **Responsywny Interfejs Użytkownika:** Przyjazny dla użytkownika interfejs webowy, zbudowany z wykorzystaniem biblioteki Bootstrap, zapewniający adaptację do różnych rozmiarów ekranu.
-   **Podstawowa Walidacja Danych:** Walidacja po stronie klienta (HTML5) oraz serwera, zapewniająca poprawność wprowadzanych danych w formularzach (np. zakres roku wydania, wymagane pola).

## Struktura Projektu (Wzorzec MVC)
Projekt jest zorganizowany zgodnie z wzorcem architektonicznym Model-View-Controller:
-   **Model:** Warstwa odpowiedzialna za logikę danych i interakcje z bazą danych. Obejmuje pliki w katalogu `app/models/` (np. `Book.py`, `Author.py`, `Person.py`, `Borrowing.py`, `Review.py`).
-   **Controller:** Warstwa obsługująca żądania HTTP od użytkownika, wchodzi w interakcje z modelami w celu pobrania/zmiany danych, a następnie przekazuje przetworzone dane do widoków. Główny kontroler to `book_controller.py` w katalogu `app/controllers/`.
-   **View:** Warstwa odpowiedzialna za prezentację danych użytkownikowi. Są to szablony HTML znajdujące się w katalogu `app/templates/` (np. `base.html`, `book_list.html`, `book_form.html`, `book_detail.html`). Do stylizacji użyto dodatkowych plików CSS (`app/views/static/css/style.css`) oraz JS (`app/views/static/js/main.js`).

## Technologie
-   **Backend:** Flask (Python), Flask-SQLAlchemy, SQLite (baza danych)
-   **Frontend:** Jinja2 (szablony HTML), Bootstrap 5 (CSS/JS)
-   **Infrastruktura:** Docker, Docker Compose (konteneryzacja)

## Instrukcje Uruchomienia Aplikacji
Aby uruchomić aplikację lokalnie, wykonaj poniższe kroki:

1.  **Sklonuj repozytorium:**
    ```bash
    git clone [tutaj wstaw link do swojego repozytorium GitHub]
    cd [nazwa_katalogu_projektu_np_library_project]
    ```
2.  **Utwórz i aktywuj wirtualne środowisko:**
    Zalecane jest użycie wirtualnego środowiska w celu izolowania zależności projektu.
    ```bash
    python -m venv .venv
    # Dla systemu Windows:
    .venv\Scripts\activate
    # Dla systemów macOS/Linux:
    source .venv/bin/activate
    ```
3.  **Zainstaluj zależności:**
    Wszystkie wymagane pakiety Python są wymienione w pliku `requirements.txt`.
    ```bash
    pip install -r requirements.txt
    ```
4.  **Zainicjuj bazę danych:**
    To polecenie utworzy wszystkie niezbędne tabele w bazie danych SQLite (`library.db`). Pamiętaj, że ponowne uruchomienie tej komendy usunie istniejące dane.
    ```bash
    python init_db.py
    ```
5.  **Uruchom aplikację:**
    ```bash
    python run.py
    ```
6.  Otwórz przeglądarkę internetową i przejdź pod adres: `http://127.0.0.1:5000`

## Kod Źródłowy Aplikacji
Kod źródłowy aplikacji znajduje się w głównym katalogu projektu, zorganizowany zgodnie z wzorcem MVC:
-   `app/`: Główny katalog aplikacji Flask, zawierający moduły `models`, `controllers`, `templates` (views) oraz `static` (dla CSS/JS).
-   `config.py`: Plik konfiguracyjny aplikacji.
-   `run.py`: Główny skrypt uruchamiający aplikację Flask.
-   `init_db.py`: Skrypt do inicjalizacji bazy danych.
-   `requirements.txt`: Lista zależności Python.

## Plik z Przykładowymi Danymi Wejściowymi
Aplikacja zawiera skrypt `add_test_data.py`, który służy do szybkiego wypełnienia bazy danych przykładowymi danymi (autorami, książkami, osobami i recenzjami). Jest to szczególnie przydatne po pierwszej inicjalizacji bazy danych lub po jej zresetowaniu. Aby dodać te dane, uruchom:
```bash
python add_test_data.py
```

## Konfiguracja Docker
Projekt został przygotowany do uruchomienia w kontenerach Docker, co ułatwia jego deployment i testowanie w różnych środowiskach. Do uruchomienia aplikacji wraz z bazą danych PostgreSQL używany jest Docker Compose.

1.  **Zbuduj obraz Docker:**
    ```bash
    docker-compose build
    ```
2.  **Uruchom aplikację (wraz z bazą danych PostgreSQL) za pomocą Docker Compose:**
    ```bash
    docker-compose up
    ```
    Aplikacja będzie dostępna pod adresem `http://localhost:5000` (lub `http://127.0.0.1:5000`).

## Galeria Zrzutów Ekranu

### Strona główna - Lista Książek
*Wstaw zrzut ekranu przedstawiający główną stronę aplikacji z listą książek i paskiem wyszukiwania. Upewnij się, że widać kilka książek i funkcję wyszukiwania.*

### Formularz Dodawania Książki
*Wstaw zrzut ekranu przedstawiający formularz dodawania nowej książki (dostępny po kliknięciu 'Add New Book'). Pokaż, że pole autora jest tekstowe.*

### Strona Szczegółów Książki i Recenzje
*Wstaw zrzut ekranu przedstawiający stronę szczegółów konkretnej książki, w tym informacje o książce, sekcję recenzji z istniejącymi recenzjami oraz formularz do dodawania nowej recenzji (z widocznym polem tekstowym na imię).*

### Formularz Dodawania Recenzji
*Wstaw zrzut ekranu przedstawiający sam formularz dodawania recenzji (może być ten sam co na stronie szczegółów książki, ale skupiony na formularzu), z widocznymi polami 'Your Name', 'Rating' i 'Comment'.* 