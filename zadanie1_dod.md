# Technologie chmurowe Zadanie nr 1 część nieobowiązkowa punkt 2
## Piotr Zalewski I1S6 TI 6.2

Aplikacja webowa wyświetlająca informacje o pogodzie w wybranym miejscu z listy dostępnych. Jest zbudowana w oparciu obraz bazowy z Node.js i Alpine.

Instrukcja uruchomienia:
1. Utworzyć nowy katalog i pobrać do niego zawartość repozytorium: `https://github.com/pzlab33/zadanie1`
2. Ustawić katalog roboczy na folder z pobraną zawartością repozytorium
3. Zbudować obraz poleceniem: `docker build -f Dockerfile_zadanie_nr_1 -t weather-app .`
4. Uruchomić kontener z obrazu poleceniem: `docker run -d -p 8080:8080 --name weather-run weather-app`
5. Uruchomić przeglądarkę internetową i połączyć się z adresem: `http://localhost:8080/`

Pozostałe polecenia do części obowiązkowej:
1. Sprawdzenie logów aplikacji: `docker logs weather-run`
2. Sprawdzenie liczby warstw w zbudowanym obrazie: `docker inspect weather-app | jq '.[].RootFS'`
3. Sprawdzenie rozmiaru zbudowanego obrazu: `docker image ls weather-app`

Polecenia wykorzystane w części nieobowiązkowej dla punktu 2 (wymagane zalogowanie na konto DockerHub pzlab33; w sprawozdaniu w pliku pdf dano zrzuty ekranu z wynikami poleceń):
1. Utworzenie buildera opartego na sterowniku docker-container: `docker buildx create --name testbuilder --driver=docker-container --use --bootstrap`
2. Zbudowanie obrazu z cache z użyciem eksportera registry oraz backend-u inline: `docker buildx build -f Dockerfile_zadanie_nr_1 -t pzlab33/weather-app:v1 --platform linux/amd64,linux/arm64 --cache-to type=inline --cache-from type=registry,ref=pzlab33/weather-app:v1 --push .`
3. Potwierdzenie zbudowania obrazu na dwie wymagane w zadaniu platformy sprzętowe: `docker buildx imagetools inspect pzlab33/weather-app:v1`
4. Analiza CVE z wykorzystaniem narzędzia Trivy: `trivy image pzlab33/weather-app:v1`
