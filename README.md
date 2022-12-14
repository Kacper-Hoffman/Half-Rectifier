# Sterowany Prostownik Jednopo艂贸wkowy z Optoizolacj膮 - LTSpice 馃嚨馃嚤
## Wst臋p
W ramach zaj臋膰 laboratoryjnych wykona艂em model prostownika jednopo艂贸wkowego w LTSpice. Nie jest to jednak model 'banalny' sk艂adaj膮cy si臋 z jednej diody; To jest pe艂ny model zawieraj膮cy sterowanie tyrystorowe, optoizolacj臋 oraz obci膮偶enie mog膮ce posiada膰 ka偶dy charakter (rezystancyjny, indukcyjny, pojemno艣ciowy oraz kombinacje trzech). Do stworzenia modelu wykorzystano program LTSpice. U偶yte zosta艂y w wi臋kszo艣ci elementy z bibliotek LTSpice, jednak potencjometr oraz wystarczaj膮co rozbudowany model optoizolacji musia艂y by膰 pobrane z internetowych zasob贸w.
## Uk艂ad
Stworzony uk艂ad sk艂ada si臋 z 5 element贸w - Inicjalizacja, G艂贸wny prostownik, Optoizolacja, Komparator oraz Potencjometr.

![Model](https://github.com/Kacper-Hoffman/Half-Rectifier/blob/main/model_signed.png)

Inicjalizacja polega na ustawieniu parametr贸w symulacji. Tutaj okre艣lamy, 偶e chcemy wykona膰 symulacj臋 typu transient ("przej艣ciowa", symulacja wzgl臋dem czasu), wykorzystujemy biblioteki EC103D1 i MOC3020 oraz element potentiometer. Obok tych warunk贸w zaznaczamy r贸wnie偶 wykorzystane 藕r贸d艂a napi臋cia. Tutaj stosujemy sygna艂 pi艂owy Vsaw zdefiniowany przez powtarzane PWL (Piecewise Linear Function, funkcja liniowa z艂o偶ona z wielu element贸w), napi臋cie zasilaj膮ce Vcc oraz sygna艂 odniesienia Vsmax warto艣li szczytowej pi艂y. G艂贸wnym prostownikiem jest tyrystor EC103D1 z rezystorem ochronnym R4 oraz ustawianym obci膮偶eniem R1, L1, C1. Ten akurat prostownik mo偶e pracowa膰 nawet dla napi臋cia sieciowego, ale 艂atwo zmodyfikowa膰 uk艂ad na napi臋cie niskie. Rol臋 optoizolacji spe艂nia optotriak MOC3020 z kluczem tranzystorowym Si1555DL_N, rezystor R3 i bramkowy R2. Komparator LT1721 por贸wnuje sygna艂 pi艂owy z napi臋ciem potencjometra. Potencjometr po艂膮czono z komparatorem przez wt贸rnik napi臋ciowy z艂o偶ony ze wzmacniacza AD549.

## Spos贸b dzia艂ania
Prostownik sterowany jednopo艂贸wkowy stosuje zachowanie tyrystora do blokowania ujemnej po艂owy sygna艂u wej艣ciowego jak i r贸wnie偶 zablokowania cz臋艣ci dodatniej a偶 do ustawionej warto艣ci na potencjometrze. Potencjometr posiada pewn膮 rezystancj臋 Rtot oraz ustawienie wiper. Warto艣膰 wiper okre艣la jak膮 cz臋艣膰 napi臋cia aktualnie si臋 przenosi. Mo偶e ona si臋 zmienia膰 od 0 do 1, oznaczaj膮c ca艂kowite uziemienie lub przeniesienie. Wt贸rnik napi臋ciowy jest niezb臋dny do po艂膮czenia z reszt膮 uk艂adu. Sygna艂 przechodzi na komparator. Komparator s艂u偶y do por贸wnania warto艣ci sygna艂u pi艂owego z napi臋ciem potencjometra. Wybrano sygna艂 pi艂owy poniewa偶 liniowo odpowiada poziomom napi臋cia z prostownika - dla po艂贸wki okresu warto艣膰 pi艂y wynosi 5 V, dla 膰wierci 2.5 V, dla jednej 贸smej 1.25 V itd. Te napi臋cia z kolej odpowiadaj膮 ustawieniom wiper r贸wnym 1, 0.5 oraz 0.25 co daje proste sterowanie. Sygna艂 z komparatora przechodzi potem na optoizolacj臋. S艂u偶y ona do galwanicznego oddzielenia sterowania od prostownika z obci膮偶eniem. Uk艂ad izolacyjny MOC3020 to dioda LED po stronie wej艣ciowej oraz optotriak po stronie wyj艣ciowej. Przenoszenie sygna艂u polega na sterowaniu tranzystorowym. Dioda jest zasilana stale przez rezystor R3, ale nie mo偶e 艣wieci膰 je艣li tranzystor zablokuje drog臋 dla pr膮du. Dopiero pojawienie si臋 wystarczaj膮co wysokiego napi臋cia na 藕r贸dle pozwala na przenoszenie. Na koniec sygna艂 z izolacji przechodzi przez rezystor bramkowy R2 i steruje prostownikiem EC103D1.

## Test Prostownika
Prawid艂owe dzia艂anie prostownika mo偶na potwierdzi膰 przez testowanie uk艂adu. Uruchamia si臋 symulacj臋 dla r贸偶nych obci膮偶e艅 oraz obserwuje napi臋cie i pr膮d na wyj艣ciu. Dla obci膮偶enia rezystancyjnego pr膮d i napi臋cie powinny mie膰 identyczny kszta艂t. Ujemna po艂owa zostanie zablokowana, a dodatnia po艂owa zacznie przewodzi膰 dopiero od napi臋cia ustalonego przez potencjometr. Dla obci膮偶enia indukcyjnego pr膮d nie mo偶e si臋 zmienia膰 nagle, dlatego jego wzrost i spadek zostan膮 op贸藕nione. Z tego powodu napi臋cie zacznie by膰 przewodzone p贸藕niej i na koniec przeniesiony zostanie fragment ujemny. W obci膮偶eniu pojemno艣ciowym zauwa偶alne b臋dzie 艂adowanie i roz艂adowanie si臋 kondensatora. Poziom napi臋cia i pr膮du b臋d膮 spada膰 znacznie wolniej ni偶 wcze艣niej, tak 偶e w ujemnej po艂owie napi臋cia widoczne b臋dzie roz艂adowanie.

![Resistance Load](https://github.com/Kacper-Hoffman/Half-Rectifier/blob/main/resistance5.png)

![Inductance Load](https://github.com/Kacper-Hoffman/Half-Rectifier/blob/main/induction5.png)

![Capacitance Load](https://github.com/Kacper-Hoffman/Half-Rectifier/blob/main/capacitance5.png)

Jak wida膰, symulacja w pe艂ni odpowiada rzeczywistemu uk艂adowi prostownika sterowanego jednopo艂贸wkowego.

Szczeg贸艂owy opis stworzonego modelu dost臋pny jest w [moim projekcie](https://github.com/Kacper-Hoffman/Half-Rectifier/blob/main/Kacper%20Hoffman%20-%20Projekt%20Elektronika.pdf).

---
# Controlled Half Wave Rectifier with Optoisolation - LTSpice 馃嚞馃嚙
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

The detailed description of the model is available in [my project (馃嚨馃嚤 only)](https://github.com/Kacper-Hoffman/Half-Rectifier/blob/main/Kacper%20Hoffman%20-%20Projekt%20Elektronika.pdf).
