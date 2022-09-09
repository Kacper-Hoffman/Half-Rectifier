# Sterowany Prostownik Jednopołówkowy z Optoizolacją - LTSpice 🇵🇱
## Wstęp
W ramach zajęć laboratoryjnych wykonałem model prostownika jednopołówkowego w LTSpice. Nie jest to jednak model 'banalny' składający się z jednej diody; To jest pełny model zawierający sterowanie tyrystorowe, optoizolację oraz obciążenie mogące posiadać każdy charakter (rezystancyjny, indukcyjny, pojemnościowy oraz kombinacje trzech). Do stworzenia modelu wykorzystano program LTSpice. Użyte zostały w większości elementy z bibliotek LTSpice, jednak potencjometr oraz wystarczająco rozbudowany model optoizolacji musiały być pobrane z internetowych zasobów.
## Układ
Stworzony układ składa się z 5 elementów - Inicjalizacja, Główny prostownik, Optoizolacja, Komparator oraz Potencjometr.

![Model](https://github.com/Kacper-Hoffman/Half-Rectifier/blob/main/model_signed.png)

Inicjalizacja polega na ustawieniu parametrów symulacji. Tutaj określamy, że chcemy wykonać symulację typu transient ("przejściowa", symulacja względem czasu), wykorzystujemy biblioteki EC103D1 i MOC3020 oraz element potentiometer. Obok tych warunków zaznaczamy również wykorzystane źródła napięcia. Tutaj stosujemy sygnał piłowy Vsaw zdefiniowany przez powtarzane PWL (Piecewise Linear Function, funkcja liniowa złożona z wielu elementów), napięcie zasilające Vcc oraz sygnał odniesienia Vsmax wartośli szczytowej piły. Głównym prostownikiem jest tyrystor EC103D1 z rezystorem ochronnym R4 oraz ustawianym obciążeniem R1, L1, C1. Ten akurat prostownik może pracować nawet dla napięcia sieciowego, ale łatwo zmodyfikować układ na napięcie niskie. Rolę optoizolacji spełnia optotriak MOC3020 z kluczem tranzystorowym Si1555DL_N, rezystor R3 i bramkowy R2. Komparator LT1721 porównuje sygnał piłowy z napięciem potencjometra. Potencjometr połączono z komparatorem przez wtórnik napięciowy złożony ze wzmacniacza AD549.

## Sposób działania
Prostownik sterowany jednopołówkowy stosuje zachowanie tyrystora do blokowania ujemnej połowy sygnału wejściowego jak i również zablokowania części dodatniej aż do ustawionej wartości na potencjometrze. Potencjometr posiada pewną rezystancję Rtot oraz ustawienie wiper. Wartość wiper określa jaką część napięcia aktualnie się przenosi. Może ona się zmieniać od 0 do 1, oznaczając całkowite uziemienie lub przeniesienie. Wtórnik napięciowy jest niezbędny do połączenia z resztą układu. Sygnał przechodzi na komparator. Komparator służy do porównania wartości sygnału piłowego z napięciem potencjometra. Wybrano sygnał piłowy ponieważ liniowo odpowiada poziomom napięcia z prostownika - dla połówki okresu wartość piły wynosi 5 V, dla ćwierci 2.5 V, dla jednej ósmej 1.25 V itd. Te napięcia z kolej odpowiadają ustawieniom wiper równym 1, 0.5 oraz 0.25 co daje proste sterowanie. Sygnał z komparatora przechodzi potem na optoizolację. Służy ona do galwanicznego oddzielenia sterowania od prostownika z obciążeniem. Układ izolacyjny MOC3020 to dioda LED po stronie wejściowej oraz optotriak po stronie wyjściowej. Przenoszenie sygnału polega na sterowaniu tranzystorowym. Dioda jest zasilana stale przez rezystor R3, ale nie może świecić jeśli tranzystor zablokuje drogę dla prądu. Dopiero pojawienie się wystarczająco wysokiego napięcia na źródle pozwala na przenoszenie. Na koniec sygnał z izolacji przechodzi przez rezystor bramkowy R2 i steruje prostownikiem EC103D1.

## Test Prostownika
Prawidłowe działanie prostownika można potwierdzić przez testowanie układu. Uruchamia się symulację dla różnych obciążeń oraz obserwuje napięcie i prąd na wyjściu. Dla obciążenia rezystancyjnego prąd i napięcie powinny mieć identyczny kształt. Ujemna połowa zostanie zablokowana, a dodatnia połowa zacznie przewodzić dopiero od napięcia ustalonego przez potencjometr. Dla obciążenia indukcyjnego prąd nie może się zmieniać nagle, dlatego jego wzrost i spadek zostaną opóźnione. Z tego powodu napięcie zacznie być przewodzone później i na koniec przeniesiony zostanie fragment ujemny. W obciążeniu pojemnościowym zauważalne będzie ładowanie i rozładowanie się kondensatora. Poziom napięcia i prądu będą spadać znacznie wolniej niż wcześniej, tak że w ujemnej połowie napięcia widoczne będzie rozładowanie.

![Resistance Load](https://github.com/Kacper-Hoffman/Half-Rectifier/blob/main/resistance5.png)

![Inductance Load](https://github.com/Kacper-Hoffman/Half-Rectifier/blob/main/induction5.png)

![Capacitance Load](https://github.com/Kacper-Hoffman/Half-Rectifier/blob/main/capacitance5.png)

Jak widać, symulacja w pełni odpowiada rzeczywistemu układowi prostownika sterowanego jednopołówkowego.

Szczegółowy opis stworzonego modelu dostępny jest w [moim projekcie](https://github.com/Kacper-Hoffman/Half-Rectifier/blob/main/Kacper%20Hoffman%20-%20Projekt%20Elektronika.pdf).

---
# Controlled Half Wave Rectifier with Optoisolation - LTSpice 🇬🇧
## Introduction
During laboratory classes I have creaded a model of a half wave rectifier. However, this is not a 'trivial' model that has one diode; It's a full model containing thyristor controlling, optoizolation and a load that can have any character (resistance, inductance, capacitance and any combination of the three). LTSpice was used to create this model. Most elements used were available in LTSpice libraries, but the potencjometer and a ufficiently advanced model of optoisolation had to be downloaded from internet resources.
## Model
The created model has five regions - Initialisation, Main rectifier, Optoizolation, Comparator and Potencjometer.

![Model](https://github.com/Kacper-Hoffman/Half-Rectifier/blob/main/model_signed.png)

Initialisation is the settings of the simulation. Here we determine that we want a transient type simulation (time based simulation), that we use libraries for EC103D1, MOC3020 and potentiometer. We also define voltage sources. Here we use a saw signal Vsaw defined with PWL (Piecewise Linear Function), source voltage Vcc and Vsmax as the maximum value of Vsaw. The main rectifier is EC103D1 with protective resistor R4 and the load R1, L1, C1. This rectifier can work even under high voltage, but modifying the model for lower voltage is easy. Optoisolation is based on MOC3020 with is connected to the comparator through a voltage follower consisting of AD549.

## Function
Controlled half wave rectifier is used to block the negative half of the wave, as well as the part of the positive half before the voltage set with the potentiometer. Potencjometer has a certain resistance Rtot as well as the wiper setting. The value of wiper determines what part of the voltage is transferred. It can change from 0 to 1, which is total grounding or total transfer. The voltage follower is necessary to connect the potentiometer to the rest of the circut. The signalthen goes to the comparator. The comparator compares the saw signal with the comparator voltage. The saw signal was used due to its linear relation with source voltage - for one half the value of the saw signal is 5 V, for a quarter we have 2.5 V, for one eight we have 1.25 V etc. Those correspond to wiper values of 1, 0.5 and 0.25 which gives simple control. The signal from the comparator goes to optoisolation. It's used for galvanically isolating the control signal from the rectifier itself. Isolation MOC3020 is a LED diode from the input side and an optotriac from the output side. The signal is transferred thought transistor keying. The diode is powered through the R3 resistor, but it can't emit light if the transistor is blocking the current. Only a sufficiently hight current allows transfer. Finally the signal arrives at the gate resistor R2 and controlls EC103D1.

## Rectifier Test
Whether the rectifier works can be tested. We start the simulation for different loads and observe output voltage and current. For a resistive load the voltage and current should be identical. The negative half should be blocked, and the positive should start conducting only after reaching the potentiometer voltage. For inductive load the current cannot change suddenly, and so its rise and fall will be slower. Because of this the voltage will start conducting later and a part of the negative half will be transferred. In the capacitive load the charging and discharging of the caparicot will be visible. Voltage and current will fall slower than before, and even during the negative half we will see the discharging.

![Resistance Load](https://github.com/Kacper-Hoffman/Half-Rectifier/blob/main/resistance5.png)

![Inductance Load](https://github.com/Kacper-Hoffman/Half-Rectifier/blob/main/induction5.png)

![Capacitance Load](https://github.com/Kacper-Hoffman/Half-Rectifier/blob/main/capacitance5.png)

As we can see, the simulation works as a real controlled half wave rectifier.

The detailed description of the model is available in [my project (🇵🇱 only)](https://github.com/Kacper-Hoffman/Half-Rectifier/blob/main/Kacper%20Hoffman%20-%20Projekt%20Elektronika.pdf).
