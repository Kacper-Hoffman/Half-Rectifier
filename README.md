⚠️ WIP ⚠️
# Sterowany Prostownik Jednopołówkowy z Optoizolacją - LTSpice 🇵🇱
## Wstęp
W ramach zajęć laboratoryjnych wykonałem model prostownika jednopołówkowego w LTSpice. Nie jest to jednak model 'banalny' składający się z jednej diody; To jest pełny model zawierający sterowanie tyrystorowe, optoizolację oraz obciążenie mogące posiadać każdy charakter (rezystancyjny, indukcyjny, pojemnościowy oraz kombinacje trzech). Do stworzenia modelu wykorzystano program LTSpice. Użyte zostały w więkrzości elementy z bibliotek LTSpice, jednak potencjometr oraz wystarczająco rozbudowany model optoizolacji musiały być pobrane z internetowych zasobów.
## Układ
Stworzony układ składa się z 5 elementów - Inicjalizacja, Główny prostownik, Optoizolacja, Komparator oraz Potencjometr.

![Model](https://github.com/Kacper-Hoffman/Half-Rectifier/blob/main/model_signed.png)

Inicjalizacja polega na ustawieniu parametrów symulacji. Tutaj określamy, że chcemy wykonać symulację typu transient ("przejściowa", symulacja względem czasu), wykorzystujemy biblioteki EC103D1 i MOC3020 oraz element potentiometer. Obok tych warunków zaznaczamy również wykorzystane źródła napięcia. Tutaj stosujemy sygnał piłowy Vsaw zdefiniowany przez powtarzane PWL (Piecewise Linear Function, funkcja liniowa złożona z wielu elementów), napięcie zasilające Vcc oraz sygnał odniesienia Vsmax wartośli szczytowej piły. Głównym prostownikiem jest tyrystor EC103D1 z rezystorem ochronnym R4 oraz ustawianym obciążeniem R1, L1, C1. Ten akurat prostownik może pracować nawet dla napięcia sieciowego, ale łatwo zmodyfikować układ na napięcie niskie. Rolę optoizolacji spełnia optotriak MOC3020 z kluczem tranzystorowym Si1555DL_N, rezystor R3 i bramkowy R2. Komparator LT1721 porównuje sygnał piłowy z napięciem potencjometra. Potencjometr połączono z komparatorem przez wtórnik napięciowy złożony ze wzmacniacza AD549.

## Sposób działania
Prostownik sterowany jednopołówkowy stosuje zachowanie tyrystora do blokowania ujemnej połowy sygnału wejściowego jak i również zablokowania części dodatniej aż do ustawionej wartości na potencjometrze. Potencjometr posiada pewną rezystancję Rtot oraz ustawienie wiper. Wartość wiper określa jaką część napięcia aktualnie się przenosi. Może ona się zmieniać od 0 do 1, oznaczając całkowite uziemienie lub przeniesienie. Wtórnik napięciowy jest niezbędny do połączenia z resztą układu. Sygnał przechodzi na komparator. Komparator służy do porównania wartości sygnału piłowego z napięciem potencjometra. Wybrano sygnał piłowy ponieważ liniowo odpowiada poziomom napięcia z prostownika - dla połówki okresu wartość piły wynosi 5 V, dla ćwierci 2.5 V, dla jednej ósmej 1.25 V itd. Te napięcia z kolej odpowiadają ustawieniom wiper równym 1, 0.5 oraz 0.25 co daje proste sterowanie. Sygnał z komparatora przechodzi potem na optoizolację. Służy ona do galwanicznego oddzielenia sterowania od prostownika z obciążeniem. Układ izolacyjny MOC3020 to dioda LED po stronie wejściowej oraz optotriak po stronie wyjściowej. Przenoszenie sygnału polega na sterowaniu tranzystorowym. Dioda jest zasilana stale przez rezystor R3, ale nie może świecić jeśli tranzystor zablokuje drogę dla prądu. Dopiero pojawienie się wystarczająco wysokiego napięcia na źródle. Na koniec sygnał z izolacji przechodzi przez rezystor bramkowy R2 i steruje prostownikiem EC103D1.

## Test Prostownika
Prawidłowe działanie prostownika można potwierdzić przez testowanie układu. Uruchamia się symulację dla różnych obciążeń oraz obserwuje napięcie i prąd na wyjściu. Dla obciążenia rezystancyjnego prąd i napięcie powinny mieć identyczny kształt. Ujemna połowa zostanie zablokowana, a dodatnia połowa zacznie przewodzić dopiero od napięcia ustalonego przez potencjometr. Dla obciążenia indukcyjnego prąd nie może się zmieniać nagle, dlatego jego wzrost i spadek zostaną opóźnione. Z tego powodu napięcie zacznie być przewodzone później i na koniec przeniesiony zostanie fragment ujemny. W obciążeniu pojemnościowym zauważalne będzie ładowanie i rozładowanie się kondensatora. Poziom napięcia i prądu będą spadać znacznie wolniej niż wcześniej, tak że w ujemnej połowie napięcia widoczne będzie rozładowanie.

![Resistance Load](https://github.com/Kacper-Hoffman/Half-Rectifier/blob/main/resistance5.png)

![Inductance Load](https://github.com/Kacper-Hoffman/Half-Rectifier/blob/main/induction5.png)

![Capacitance Load](https://github.com/Kacper-Hoffman/Half-Rectifier/blob/main/capacitance5.png)

Jak widać, symulacja w pełni odpowiada rzeczywistemu układowi prostownika sterowanego jednopołówkowego.

Szczegółowy opis stworzonego modelu dostępny jest w ![moim projekcie](https://github.com/Kacper-Hoffman/Half-Rectifier/blob/main/Kacper%20Hoffman%20-%20Projekt%20Elektronika.pdf).

---
# Controlled Half Wave Rectifier with Optoisolation - LTSpice 🇬🇧
