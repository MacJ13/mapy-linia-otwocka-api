# Projekt [mapy-linia-otwocka-api] - Backend

Repozytorium zawierające logikę biznesową, API oraz obsługę bazy danych dla projektu strony Mapy: Linia Otwocka

---

## 1. Główne założenia 
Ta aplikacja jest to część backendowa projektu związanego z przeglądaniem map na stronie. Będzie odpowiedzialna aby zarządzać danymi związanymi z mapami liniii otwockiej i jest przeznaczona wyłącznie dla aministratorów strony. Panel Administratora będzie mieć możliwość wprowadzania, akutalizowania, edytowania oraz usuwania danych. Aplikacja również będzie udostępniać API, które w formacie JSON będzie komunikować się z frontendem projektu

## 2. Funkcjonalności
- [] Jako użytkownik (administrator) mogę zarejestrować się i zalogować
- [] Jako zalogowany administrator mogę wprowadzać dane odnośnie miejsc, warst mapy itd.
- [] Jako zalogowany administrator mogę edytować oraz usuwać te dane

## 3. Model Bazy danych
* ***User:** id | password_hash | user_name | role
* ***Place:** id | place_name | place_area | coords | description | category | year | url_link | url_img
* ***Place_Area:** id | place_area_name | coords
* ***Place_Category:** id | category_name
* ***Historic_Map:** id | name | coords
* ***Layer_Map:**  id | layer_map_name | url_img

## 4. Planowanie API (REST)
aplikacja backend będzie przesyłać dane w formacie JSON gdy klient (aplikacja webowa frontedn) będzie wykonywać zapytanie do serwera. 
Gdy frontend będzie potrzebować np. dane miejsc to będzie wykonywać zapytanie odnośnie miejsc za pomocą metody i trasy GET api/map_places/ i będzie zwracać plik JSON z danymi które są przychowywane w DB.
Głownie w aplikacji będą to metody GET. Natomiast pozostałe metody tj. POST, PUT czy DELETE będą już w obrębie aplikacji serwerowej

### Trasy API (Zwracają JSON dla aplikacji w React)
* `GET /api/map_places` - pobranie listy miejsc na mapie
* `GET /api/map_places?category=[category]&area=[area]` - filtrowanie miejsc
* `GET /api/map_places/:place_id` - pobranie pojedynczego miejsca
* `GET /api/categories` - pobranie listy kategorii
* `GET /api/areas` - pobranie listy obszarów
* `GET /api/layers` - pobranie listy warstw
* `GET /api/historic_maps` - pobranie listy historycznych map

### Trasy Panelu Administratora (Renderowane przez EJS po stronie serwera)
* `GET /admin/login` - formularz logowania dla administratora
* `GET /admin/dashboard` - lista wszystkich miejsc z opcjami Edytuj / Usuń
* `GET /admin/places/new` - formularz dodawania nowego miejsca (wysyła POST do /admin/places)
* `POST /admin/places` - akcja zapisu nowego miejsca w bazie
* `GET /admin/places/:id/edit` - formularz edycji miejsca (wysyła POST/PUT do /admin/places/:id)
* `POST /admin/places/:id/delete` - akcja usunięcia miejsca z bazy

---

## 5. Technologie
* **Runtime:** Node.js + TypeScript
* **Framework:** Express.js
* **Baza danych:** Postgresql z rozszerzeniem PostGis
* **ORM:** Prisma
* **View Engine:** EJS (do wyrenderowania panelu administracyjnego)
