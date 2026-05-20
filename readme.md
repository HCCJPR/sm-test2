## 7.a) Dați exemple de doua tipuri de reglare care se pot implementa cu un sistem cu microprocesor și ilustrați diferența între ele?
> Reglare în buclă deschisă: un sistem de irigare care pornește pompa pentru o perioadă fixă de timp, fără a măsura umiditatea solului.
> Reglare în buclă închisă: un termostat care măsoară temperatura camerei și ajustează puterea caloriferului pentru a menține temperatura dorită.
> Diferența este că în buclă deschisă nu există feedback, iar în buclă închisă există un mecanism de feedback care ajustează acțiunea în funcție de rezultatul măsurat.
## 7.b) Din punctul de vedere al timpului, ce este esențial pentru implementarea unei rutine de control care să poată exploata cu ușurință proprietățile transformatei z?
> definirea perioadei de eșantionare și control
## 7.c) Ce compromis trebuie să asigure alegerea perioadei de eșantionare și control într-un sistem care reglează viteza unui motor DC în buclă închisă folosind un encoder în cuadratură și o punte H?
> o perioadă de eșantionare mare nu va asigura stabilitatea sistemului 
(acesta va evolua semnificativ între momentele de intervenție ale regulatorului). 
O perioadă de eșantionare prea redusă poate face imposibilă finalizarea execuției rutinei de reglare, sau poate limita semnificativ rezoluția senzorilor folosiți, 
în funcție de modul de exploatare al acestora) 
## 7.e) Ce trebuie făcut într-o implementare de rutină de control PI pentru a limita efectele nedorite ale acumulării efectului erorii pe termen lung?
> Se poate introduce o limitare a valorii maxime a termenului integral, sau se poate introduce o resetare a termenului integral la anumite 
> intervale de timp sau condiții specifice (de exemplu, când eroarea este foarte mică sau când sistemul atinge o stare stabilă).

## 7.g) Cum trebuie prelucrată referința de intrare pentru un motor DC  caruia i se controlează viteza pentru a-i reduce uzura?
> Se poate implementa o rampă de accelerație și decelerație pentru a asigura o tranziție lină între viteze

## 7.i) Cum se poate prelucra (ușor) referința de viteză  pentru un motor DC pentru a evita cazuri de instabilitatea a sistemului de reglare și în același timp să se obțină o dinamică mai bună?
> folosind un filtru de ordin I (cu caracteristică exponențial negativă) care este foarte ușor de implementat în sisteme digitale

## 7.j) Care este rolul diodelor antiparalele de pe tranzistorii din punțile H?
> Aceste diode permit curentului să circule în ambele direcții prin motor, ceea ce este esențial pentru a permite schimbarea direcției de rotație a motorului și pentru a proteja tranzistorii de tensiunile induse generate de motor în timpul schimbării direcției sau opririi.
## 8.a) Cum se configurează o rutină de întrerupere pentru  a detecta tranziția unui pin GPIO de intrare (e.g intrare de encoder)? (exemplicați cu funcții din biblioteca Pico-SDK)
> Se poate folosi funcția `gpio_set_irq_enabled_with_callback()` \
Această funcție permite specificarea pinului GPIO, \
tipul de tranziție (de exemplu, rising edge, falling edge sau ambele), și callback-ul care va fi apelat atunci când întreruperea este declanșată.
## 8.b) Cum se identifică pinul GPIO care a declanșat o întrerupere de schimbare de stare dacă a fost activată pentru mai mulți pini? (exemplicați în contextul funcțiilor din biblioteca Pico-SDK)
folosind funcția `gpio_get_irq_status()`. Această funcție returnează un bitmask în care fiecare bit corespunde unui pin GPIO. \
Pentru a determina care pin a declanșat întreruperea, se poate itera prin bitmask și verifica care bit este setat.
## 8.c) Cum poate fi utilizat instrumentul software picotool pentru a reporni o aplicație de pe RPi Pico în module BOOTSEL, daca aplicația care rulează pe place suportă reset prin USB?
> `picotool reboot `
## 8.d) Cum poate fi utilizat instrumentul software picotool pentru a reporni o aplicație de pe RPi Pico în module aplicație dacă placa este conectată în modul BOOTSEL?
> `picotool reboot --app`
## 9.a) Care sunt cele două semnalele de date esențiale pentru protocolul UART și care este principiul lor de denumire?
> Semnalele esențiale sunt Tx (Transmit) și Rx (Receive). \
Principiul de denumire este că Tx este semnalul de ieșire al dispozitivului\
care transmite date și Rx este semnalul de intrare al dispozitivului care primește date.
## 9.b) Dati două exemple de semnale auxiliare (de control al fluxului de date) pentru protocolul UART si menționați rolul și direcția (intrare/ieșire) fiecăruia
> RTS (Request to Send) - semnal de ieșire care indică că dispozitivul este gata să transmită date. \
CTS (Clear to Send) - semnal de intrare care indică că dispozitivul este gata să primească date. \
Aceste semnale sunt folosite pentru a controla fluxul de date între două dispozitive, prevenind pierderea de date atunci când unul dintre dispozitivee nu este pregătit să transmită sau să primească date.
## 9.c) Ce tip de ieșire au circuitele TSOP98638 pentru decodarea semnalelor infraroșii modulate ca trenuri de impulsuri?
> Ieșirea este de tip digitală, oferind un semnal logic care indică prezența sau absența unui semnal infraroșu modulat detectat.
## 9.d) Cum trebuie modulat semnalul de activare a unui LED infraroșu pentru ca acesta să fie detectat de senzorul TSOP98638?
> Semnalul de activare trebuie să fie modulat la o frecvență specifică (de obicei în jur de 38 kHz) pentru a fi detectat corect de senzorul TSOP98638. \
Acest lucru se poate realiza prin generarea unui tren de impulsuri la frecvența respectivă, asigurându-se că LED-ul infraroșu emite lumina în mod intermitent la acea frecvență. 
## 9.e) Pentru ce este util perifericul PIO (Programable Input Output) din structura RP2040 (ce exemple de implementări sunt prezentate în documentație)?
> Perifericul PIO este util pentru a implementa protocoale de comunicație personalizate sau pentru a extinde funcționalitatea pinilor GPIO. \
Exemple de implementări prezentate în documentație includ: \
- Implementarea unui protocol de comunicație personalizat, cum ar fi un protocol de comunicație serială care nu este nativ suportat de hardware-ul RP2040. \
- Generarea de semnale precise pentru controlul unor dispozitive, cum ar fi LED-uri sau motoare, folosind secvențe de instrucțiuni programabile. \
- Implementarea unor funcții de temporizare sau de generare de semnale care necesită o precizie mai mare decât cea oferită de funcțiile standard de temporizare ale microcontroller-ului.
## 9.f) Care este sursa interferențelor observate cu osciloscopul în semnalele C1 și C3?
> Interferențele observate în semnalele C1 și C3 pot fi cauzate de mai mulți factori, cum ar fi: \
- Cuplajul capacitiv sau inductiv între firele de semnal și alte componente
- Zgomotul electromagnetic generat de alte dispozitive sau circuite din apropiere \
- Probleme de împământare sau de ecranare a cablurilor
## 9.g) Care este nivelul de tensiune obișnuit al liniei de ieșire Tx în timpul transmiterii biților de stop de către perifericele UART ale RP2040? Cum se poate inversa polaritatea din micropython?
> 3.3V  \
Pentru a inversa polaritatea din MicroPython, se poate utiliza o rezistență pull-up sau pull-down externă pentru a forța linia Tx să fie la nivel logic scăzut atunci când nu transmite date.
## 9.h) Analizând captura de osciloscop estimați întârzierea între semnalul transmis și cel recepționat (prin propagare locală)
> Întârzierea poate fi estimată măsurând timpul dintre începutul semnalului transmis și începutul semnalului recepționat pe captura de osciloscop. \
## 10.a) Care sunt semnalele uzuale pentru protocolul SPI? (menționați o variantă de abreviere pentru fiecare și expandarea acesteia)?
> - SCK (Serial Clock)
> - MOSI (Master Out Slave In) - semnalul de date care transportă datele de la master către slave
> - MISO (Master In Slave Out) - semnalul de date care transportă datele de la slave către master
> - SS (Slave Select) - semnalul de selecție a slave-ului care indică care dispozitiv slave este activ în comunicare
## 10.b) Care este avantajule convenției de denumire a semnalelor SPI comparativ cu convenția din protocolul UART? Exemplificați pe scurt.
> Convenția de denumire a semnalelor SPI este mai intuitivă și mai descriptivă în ceea ce privește direcția datelor și funcția fiecărui semnal. \De exemplu, în SPI, semnalele MOSI și MISO indică clar direc
ția datelor, ceea ce face mai ușor de înțeles cum se realizează comunicarea între master și slave. \În contrast, în UART, \
semnalele Tx și Rx pot fi mai puțin intuitive pentru cei care nu sunt familiarizați cu terminologia, deoarece nu indică în mod explicit direcția
datelor sau funcția fiecărui semnal.
## 10.c) SPI este un protocol sincron sau asincron? Explicați succint.
> SPI este un protocol de comunicație sincron, deoarece utilizează un semnal de ceas (SCK) pentru a sincroniza transferul de date între master și slave.
## 10.d) Care este avantajul folosirii protocolului SPI în aplicații care utilizează elemente de afișare similare afișajelor multilinie alfanumerice (LCD)?
> Un avantaj al folosirii protocolului SPI în astfel de aplicații este viteza mai mare de transfer a datelor comparativ cu alte protocoale, cum ar fi I2C. \
Acest lucru este important pentru afișajele multilinie alfanumerice, deoarece acestea pot necesita transferuri rapide de date pentru a actualiza conținutul afișajului \
în timp real, oferind astfel o experiență vizuală mai fluidă și mai responsivă.
## 10.e) Desenați o diagramă simplă cu un master SPI și două dispozitive slave SPI din care să reiasă modul de interconectare a semnalelor.
![Diagramă SPI](https://i.imgur.com/AK2ppzZ.png)
## 10.f) Care este rolul semnalelor de Slave Select într-un sistem SPI? Menționați un efect al acestui semnal asupra ieșirii perifericului (SO), presupunând acesta dispune de ieșire.
> Determină slave-ul cu care masterul dorește să comunice. SS activ -> slave activ, receptioneaza data si raspunde la comenzi.`
## 10.g) Care este secvența de comenzi pe 8 biți cu care se trece interfața de comunicație a LCD-urilor din familiile HD4460/ în modul de lucru pe 4 biți?
> Pentru a trece interfața de comunicație a LCD-urilor din familiile HD4460 în modul de lucru pe 4 biți, se poate folosi următoarea secvență de comenzi pe 8 biți:
1. Trimiteți comanda 0x33 pentru a inițializa LCD-ul
2. Trimiteți comanda 0x32 pentru a seta modul de lucru pe 4 biți

## 10.h) Cum se controlează contrastul pentru LCD-urile din modulele Microe LCD mini click? 
> Contrastul pentru LCD-urile din modulele Microe LCD mini click se controlează prin intermediul unui potențiometru conectat la pinul de contrast al LCD-ului.
## 10.i) Cum se controlează iluminarea pentru LCD-urile din modulele Microe LCD mini click? 
> Prin intermediul unui pin de control al retro-iluminării, care poate fi conectat la un semnal PWM sau la o tensiune de alimentare.
## 10.j) Desenați o schemă electrică care poate fi folosită pentru controlul retro-iluminării  unui modul LCD folosind RP2040.
![Diagramă control retro-iluminare LCD](https://i.imgur.com/SGWipj3.png)
## 10.k) Desenați schema electronică (numind toate semnalele/conexiunile) pentru trei module SPI conectate în modul daisy-chain la un microcontroller?
![Diagramă SPI Daisy-Chain](https://i.imgur.com/WCRy5CP.png)
## 11.a) Care sunt semnalele specifice protocolului I2C (abreviere si nume) și direcționalitatea lor într-un sistem simplu (multislave, single-master).
> - SDA (Serial Data) - semnal de date bidirecțional care transportă datele între master și slave
> - SCL (Serial Clock) - semnal de ceas generat de master pentru a sincroniza transferul de date între master și slave
## 11.b) Cum se diferențiază între dispozitivele I2C slave conectate pe aceeași magistrală?
> Fiecare dispozitiv I2C slave are o adresă unică pe magistrală, care este utilizată de master pentru a selecta dispozitivul cu care dorește să comunice.
## 11.c) Care este structura uzuală a unui cadru de comunicație I2C (rolul fiecărui octet)?
1. Octetul de start: indică începutul unei transmisii și este generat de master
2. Octetul de adresă: conține adresa dispozitivului slave cu care masterul dorește să comunice, precum și un bit de citire/scriere
3. Octetul de date: conține datele care sunt transmise între master și slave
4. Octetul de stop: indică sfârșitul unei transmisii și este generat de master
## 11.d) Ce particularitate a protocolului I2C ajută la confirmarea funcționării corecte?
> mecanism de recunoaștere (acknowledgment) în care dispozitivul slave răspunde cu un bit de confirmare (ACK) după ce primește fiecare octet de date.
## 11.e) Care dintre protocoalele SPI și I2C este mai potrivit pentru a comunica volume mari de date? De ce?
> SPI este mai potrivit pentru a comunica volume mari de date, deoarece oferă o viteză de transfer mai mare comparativ cu I2C.
## 11.f) Care dintre protocoalele SPI și I2C este mai potrivit pentru a fi extins la mai multe dispozitive slave? De ce?
> I2C este mai potrivit pentru a fi extins la mai multe dispozitive slave, deoarece utilizează o magistrală comună pentru date și ceas, \
permițând conectarea mai multor dispozitive fără a necesita linii de semnal suplimentare pentru fiecare dispozitiv, spre deosebire de SPI \
care necesită o linie de selecție (SS) pentru fiecare dispozitiv slave.
## 11.g) De ce sunt folosite rezistențe de pull-up pentru liniile de comunicație I2C (ce posibil conflict rezolvă)?
> Pentru a asigura că liniile SDA și SCL sunt la un nivel logic înalt atunci când nu sunt active. \
Acest lucru previne stările de flotare care pot duce la interpretarea eronată a semnalelor
## 11.i) Ce adrese sunt rezervate în protocolul I2C? Dați exemple.
> Adresele rezervate în protocolul I2C includ:
- Adresa de general call (0x00) - utilizată pentru a adresa toate dispozitivele slave simultan
- Octetul de Start (0x01) - utilizată pentru a indica începutul unei transmisii
- Adresa de CBUS (0x02) - scopul adresei CBUS este \
de a preveni conflictele de adresare: dispozitivele \
I²C ignoră aceste adrese, iar controlerul poate detecta că un \
dispozitiv CBUS este prezent dacă unul dintre aceste identificatoare apare pe magistrală. În practica modernă, CBUS nu mai este utilizat, dar rezervarea rămâne în standard.
## 11.j) Ce soluție se poate folosi când se dorește utilizarea mai multor dispozitive slave I2C cu aceeași adresă în situația în care nu poate fi schimbată/configurată? 
> Multiplexor I2C, care permite selectarea unui grup de dispozitive slave cu aceeași adresă
## 11.k) Care este secvența pe magistrala I2C care genereză simbolul START (S)?
> Linia SDA trece de la nivel logic înalt la nivel logic scăzut în timp ce linia SCL este la nivel logic înalt. \

## 11.l) Care este secvența pe magistrala I2C care genereză simbolul STOP (P)?
> Linia SDA trece de la nivel logic scăzut la nivel logic înalt în timp ce linia SCL este la nivel logic înalt.
## 11.k) Care este diferența între simbolul START și RESTART pe magistrala I2C?
> Simbolul START indică începutul unei noi transmisii, în timp ce simbolul RESTART indică o continuare a unei transmisii existente fără a genera un simbol de STOP între ele.
## 12.a) Ce este formatul RGB565?
> folosește 16 biți pentru a reprezenta culoarea unui pixel, împărțiți în 5 biți pentru roșu, 6 biți pentru verde și 5 biți pentru albastru.

## 12.b) Care este constanta literală în C pe un sistem little endian care trebuie pusă într-un buffer de pixeli RGB565 (e.g. uint16_t b[100]; b[0]=0xXYZW; )  transmis apoi prin SPI controller-ului OLED SSD1351 pentru a genera pixeli cu componenta verde cu valoare maximă și celelalte componente nule?
> 0x07E0 
## 12.c) Care este succesiunea de comenzi și rolul parametrilor acestora pentru a redesena un bloc de 10 pe 10 pixel RGB565 pe un ecran OLED 128x128 pixeli controlat prin SSD1351?
Pentru a redesena un bloc de 10×10 pixeli cu colțul stânga-sus la (x0, y0), se trimit comenzile (codul folosește macro-ul OLED_WRITE_CMD care expandează în OLED_write_cmd cu datele aferente):

OLED_SET_COLUMN (0x15) – stabilește fereastra orizontală.
Parametri: x0 (coloană start) și x1 = x0 + 9 (coloană finală).
Rol: Definește intervalul de coloane care va fi actualizat.

OLED_SET_ROW (0x75) – stabilește fereastra verticală.
Parametri: y0 (rând start) și y1 = y0 + 9 (rând final).
Rol: Definește intervalul de rânduri care va fi actualizat.

OLED_WRITE_RAM (0x5C) – comandă fără parametri, care inițiază scrierea datelor de pixel în memoria grafică (GRAM).
Rol: Pregătește controlerul să primească datele de culoare.

Transmisia datelor: se trimit 10 × 10 × 2 = 200 de octeți, reprezentând pixeli RGB565 în ordine rând-cu-rând (primul rând de sus, de la stânga la dreapta).
Aceasta se face prin OLED_write_data(buffer, 200), care asertează DC = 1, selectează chip-ul (CS = 0), transmite octeții prin SPI, apoi eliberează CS.

În codul oferit, funcția OLED_draw_block(x0, y0, x1, y1, data, len) încapsulează exact acești pași:
```c
OLED_WRITE_CMD(OLED_SET_COLUMN, x0, x1);
OLED_WRITE_CMD(OLED_SET_ROW,    y0, y1);
OLED_WRITE_CMD(OLED_WRITE_RAM);
OLED_write_data(data, len);
```
## 12.d) De ce se preferă utilizarea unei iluminări mai reduse când se folosește un ecran OLED?
> Deoarece fiecare pixel OLED emite lumină individual și consumă energie în funcție de nivelul de luminozitate. \
Reducerea iluminării poate reduce consumul de energie și, implicit, uzura pixelilor, prelungind astfel durata de viață a ecranului
## 12.e) Ce avantaje are un display OLED? Ce culori trebuie folosite pentru a beneficia de unele dintre aceste avantaje?
> Avantaje:
- Contrast ridicat: fiecare pixel emite lumină individual, oferind un contrast excelent
- Unghiuri de vizualizare largi: culorile și contrastul rămân consistente chiar și atunci când ecranul este privit din unghiuri diferite
- Timp de răspuns rapid: ideal pentru afișaje dinamice sau pentru jocuri
- Consum redus de energie: în special pentru afișaje cu multe zone negre, deoarece pixelii negri sunt complet opriți
- Design subțire și flexibil: permite crearea de ecrane curbe sau flex
Culori recomandate pentru a beneficia de avantajele OLED:
- Negru: pentru a obține un contrast maxim și a reduce consumul de energie
- Culori vii și saturate: pentru a evidenția avantajul contrastului ridicat
## 12.f) Ce compromis trebuie să asigure rata de împrospătare (refresh) pe un ecran OLED într-un sistem care funcționează pe baterii?
> Rata de împrospătare trebuie să fie optimizată pentru a echilibra între performanță și consumul de energie, reducând astfel uzura pixelilor și prelungind durata de viață a ecranului.
## 12.g) Cum se poate crește autonomia unui sistem încorporat cu ecran OLED care funcționează pe baterii?
> - Reducerea luminozității ecranului
## 12.h) Cum se poate implementa un font (cu caractere de dimensiune fixă, pentru ușurință) pentru un subset al caracterelor ASCII tipăribile (e.g. codurile 0x20...0x7E)? Exemplificați inițializarea necesară pentru reprezentarea caracterelor H și L și explicați cum poate fi folosită structura (completă) pentru desenarea unui text la o anumită poziție pe un ecran OLED controlat prin SSD1351.
> Se poate defini o structură de date care să conțină informații despre fiecare caracter, cum ar fi lățimea, înălțimea și un bitmap care reprezintă forma caracterului. \
Pentru inițializarea caracterelor H și L, se poate crea o matrice de biți care să reprezinte forma fiecărui caracter în formatul RGB565. \
Pentru desenarea unui text la o anumită poziție pe ecran, se poate itera prin fiecare caracter al textului, obținând bitmap-ul corespunzător din structura de date și apoi folosind comenzile SSD1351 pentru a scrie pixelii corespunzători în zona specificată de poziția dorită.
