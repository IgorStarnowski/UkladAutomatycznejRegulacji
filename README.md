# ⚙️ Układ Automatycznej Regulacji (UAR) – Symulator

Aplikacja desktopowa napisana w języku **C++** z wykorzystaniem frameworka **Qt**, służąca do symulacji, konfiguracji oraz wizualizacji w czasie rzeczywistym pracy Układu Automatycznej Regulacji (UAR). 

Program pozwala na badanie zachowania obiektu regulacji (model ARX), dobór parametrów regulatora oraz prowadzenie symulacji w trybie lokalnym i sieciowym przez protokół TCP/IP.

---

## ✨ Główne funkcjonalności

* **Symulacja pętli UAR:** Badanie odpowiedzi układu na różne sygnały zadane i zakłócenia w czasie rzeczywistym.
* **Konfiguracja modelu ARX:** Dedykowane okno dialogowe (`dialogarx`) pozwalające na dynamiczną modyfikację wielomianów A i B, opóźnienia transportowego oraz parametrów zakłóceń.
* **Wizualizacja na żywo:** Rysowanie dynamicznych wykresów przebiegów sygnałów (wartość zadana, regulowana, uchyb, sterowanie) przy użyciu biblioteki **QCustomPlot**.
* **Praca w trybie sieciowym (TCP/IP):** Wbudowana obsługa komunikacji klient-serwer (`klienttcp`, `serwertcp`, `dialogsiec`) umożliwiająca rozproszoną symulację (np. regulator na jednym stanowisku, obiekt regulacji na drugim).
* **Architektura warstwowa:** Oddzielenie logiki obliczeniowej symulatora (`UAR`, `UARService`) od warstwy prezentacji (`mainwindow`).

---

## 🛠️ Stos technologiczny

* **Język:** C++
* **Framework GUI oraz Sieć:** Qt (Qt Widgets, Qt Network, system sygnałów i slotów)
* **Wizualizacja wykresów:** QCustomPlot (`qcustomplot.h` / `qcustomplot.cpp`)
* **System budowania:** qmake (`projektUAR.pro`)

---

## 👥 Zespół projektowy i podział prac

Projekt został zrealizowany w zespole dwuosobowym:

* **Igor Starnowski** – Główna odpowiedzialność za warstwę interfejsu graficznego (Qt Widgets / `.ui`), wizualizację danych na wykresach (`QCustomPlot`), integrację warstwy prezentacji z logiką biznesową (`UARService`) oraz drobne poprawki w logice backendowej.
* **Krzysztof Bierzanek** – Główna odpowiedzialność za architekturę i logikę obliczeniową backendu (implementacja algorytmów pętli `UAR`, modelu `ARX` oraz komunikacji sieciowej TCP/IP), a także wsparcie i poprawki w warstwie interfejsu użytkownika.

---

## 📂 Struktura Repozytorium

* `UAR.h` / `UAR.cpp` — główna logika matematyczna i algorytmiczna układu regulacji.
* `UARService.h` / `UARService.cpp` — warstwa serwisowa pośrednicząca między symulacją a interfejsem użytkownika.
* `mainwindow.h` / `mainwindow.cpp` / `mainwindow.ui` — główne okno aplikacji oraz obsługa interakcji z użytkownikiem.
* `dialogarx.h` / `dialogarx.cpp` / `dialogarx.ui` — okno konfiguracyjne parametrów obiektu ARX.
* `dialogsiec.h` / `dialogsiec.cpp` / `dialogsiec.ui` — okno konfiguracji połączenia sieciowego.
* `klienttcp.*` / `serwertcp.*` — moduły odpowiedzialne za komunikację sieciową przez gniazda TCP.
* `qcustomplot.h` / `qcustomplot.cpp` — biblioteka do generowania wykresów w czasie rzeczywistym.
* `projektUAR.pro` — plik konfiguracyjny projektu dla narzędzia `qmake`.

---

## 🚀 Uruchomienie projektu lokalnie

### Wymagania wstępne
* Zainstalowane środowisko **Qt** (Qt 5 lub Qt 6) wraz z kompilatorem C++ (np. MinGW lub MSVC).
* Środowisko **Qt Creator** (zalecane) lub dostęp do narzędzia `qmake` z poziomu terminala.

### Sposób 1: Uruchomienie w Qt Creator (Zalecane)

1. Sklonuj repozytorium na swój dysk lokalny:

       git clone https://github.com/IgorStarnowski/UkladAutomatycznejRegulacji.git

2. Otwórz program **Qt Creator**, wybierz `File` -> `Open File or Project...` i wskaż plik `projektUAR.pro` z głównego folderu repozytorium.
3. Skonfiguruj zestaw narzędzi (Kit) dla swojego kompilatora, a następnie skompiluj i uruchom projekt skrótem `Ctrl + R` (lub zielonym przyciskiem **Run**).

### Sposób 2: Budowanie z wiersza poleceń

1. Przejdź do folderu z projektem:

       cd UkladAutomatycznejRegulacji

2. Wygeneruj plik `Makefile` za pomocą `qmake`:

       qmake projektUAR.pro

3. Skompiluj projekt (w zależności od używanego kompilatora):

       make
