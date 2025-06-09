System Zarządzania Biblioteką

Autor: Mykyta Kostiukov, 50745

Spis Treści

Wprowadzenie

Zaimplementowane Funkcjonalności

Struktura Projektu (Wzorzec MVC)

Technologie

Instrukcje Uruchomienia Aplikacji

Kod Źródłowy Aplikacji

Plik z Przykładowymi Danymi Wejściowymi

Konfiguracja Docker

Galeria Zrzutów Ekranu

Wprowadzenie

Projekt przedstawia prosty system zarządzania biblioteką, napisany w Pythonie z użyciem frameworka Flask. System umożliwia zarządzanie książkami, autorami, osobami wypożyczającymi, recenzjami oraz śledzenie wypożyczeń. Architektura projektu opiera się na wzorcu Model-View-Controller (MVC), co zapewnia przejrzystość i łatwość rozbudowy1.

Zaimplementowane Funkcjonalności

⦁	Zarządzanie książkami (CRUD): Dodawanie, przeglądanie, edycja i usuwanie książek.

⦁	Zarządzanie autorami: Autorzy tworzeni są automatycznie przy dodawaniu książki z nowym autorem.

⦁	Zarządzanie osobami: Osoby (czytelnicy, recenzenci) są tworzone automatycznie przy dodawaniu recenzji lub wypożyczeniu.

⦁	Wyszukiwanie i filtrowanie: Możliwość wyszukiwania książek po tytule i autorze.

⦁	System recenzji i ocen: Dodawanie recenzji z oceną (1-5 gwiazdek), wyświetlanie średniej oceny na stronie książki.

⦁	Śledzenie wypożyczeń: Rejestracja, kto wypożyczył daną książkę (dane dodawane skryptem).

⦁	Responsywny interfejs: Interfejs webowy oparty na Bootstrap, dostosowujący się do różnych urządzeń.

⦁	Walidacja danych: Walidacja po stronie klienta (HTML5) i serwera (np. zakres roku wydania, wymagane pola)1.

Struktura Projektu (Wzorzec MVC)

⦁	Model: Logika danych i interakcje z bazą danych (app/models/).

⦁	Controller: Obsługa żądań HTTP, logika biznesowa (app/controllers/).

⦁	View: Szablony HTML (app/templates/), statyczne pliki CSS/JS (app/static/).

⦁	Główne pliki:

⦁	config.py – konfiguracja aplikacji

⦁	run.py – uruchomienie aplikacji

⦁	init_db.py – inicjalizacja bazy danych

⦁	add_test_data.py – dodanie przykładowych danych

⦁	requirements.txt – zależności projektu1.

Technologie

⦁	Backend: Flask (Python), Flask-SQLAlchemy, SQLite

⦁	Frontend: Jinja2, Bootstrap 5

⦁	Infrastruktura: Docker, Docker Compose1.

Instrukcje Uruchomienia Aplikacji
1. Sklonuj repozytorium:
git clone https://github.com/Nersaa/Mvc-Project.git
cd project 
2. Utwórz i aktywuj wirtualne środowisko:
Python –m venv .venv
.venv\Scripts\activate
3. Zainstaluj zależności:
Pip install –r requirements.txt
4. Zainicjuj bazę danych:
Python init_db.py
5. Dodaj przykładowe dane:
Python add_test_data.py
6. Uruchom aplikację:
Python run.py
7. Otwórz przeglądarkę i przejdź pod adres:

8. https://127.0.0.1:5000

Kod Źródłowy Aplikacji

⦁	Wszystkie pliki źródłowe znajdują się w katalogu app/:

⦁	models/ – modele danych (Book, Author, Person, Borrowing, Review)

⦁	controllers/ – logika aplikacji

⦁	templates/ – szablony HTML

⦁	static/ – pliki CSS/JS

⦁	Pliki pomocnicze: config.py, init_db.py, add_test_data.py, run.py, requirements.txt1.


Plik z Przykładowymi Danymi Wejściowymi

Aby załadować przykładowe dane do bazy, uruchom:

bash

python add_test_data.py

Dane obejmują przykładowe książki, autorów, osoby i recenzje

Konfiguracja Docker
1. Zbuduj obraz Docker: 

Docker-compose build

2. Uruchom aplikację w kontenerze: 

Docker-compose up

3. Aplikacja będzie dostępna pod adresem:

https://127.0.0.1:5000
