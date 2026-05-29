---
title: "Busztopológia és IP-multiplexelt architektúra értékelése gyári biztonsági rendszerekben: Műszaki útmutató kereskedelmi riasztó-disztribútorok és rendszerintegrátorok számára"
date: 2026-05-20T09:00:00+08:00
draft: false
type: "posts"
description: "Átfogó műszaki mérnöki útmutató az RS-485 busz topológia és az IP multiplexelt architektúra értékeléséhez nagyüzemi gyártólétesítményekben. Ismerje meg az EMI mérséklését, a távolsági korlátok leküzdését, a feszültségesés kiküszöbölését és a SCADA/épületfelügyeleti rendszer platformokkal való integrációt."
keywords: [Factory Security Systems, Bus-Topology Alarm, IP-Multiplexing Architecture, Commercial Alarm Distributors, System Integrators, Industrial Intrusion Alarm, RS-485 Alarm Bus, SIA DC-09, Factory Alarm System Design]
---

Egy 40 000 m²-es gyártókomplexum védelmének tervezésekor a mérnöki döntések közvetlen hatással vannak a rendszer hosszú távú stabilitására és a karbantartási költségekre. Az ipari környezetek olyan egyedi elektromos és topológiai korlátokat támasztanak, amelyek gyorsan felszínre hozzák az alacsonyabb kategóriájú rendszerek strukturális gyengeségeit. 

Ez az útmutató bemutatja a hagyományos analóg vezetékezés, a [címezhető RS-485 busz topológia](https://athenalarm.com/athenalarm-technical-documents/burglar-alarm-knowledge/matters-485-wiring/) és a modern [IP multiplexelt architektúra](https://athenalarm.com/network-alarm-system/network-alarm-monitoring-system-application/) közötti mérnöki kompromisszumokat a nagyüzemi gyártólétesítmények fizikai védelmében.

---

## Az ipari EMI hatása a riasztóbusz-kommunikáció megbízhatóságára

A gyártócsarnokok elektromágneses szempontból kifejezetten ellenséges környezetnek minősülnek. A szállítószalagok motorjaiban és a CNC munkaállomásokon alkalmazott frekenciaváltó eszközök szélessávú vezetett zajt generálnak a 10 kHz és 30 MHz közötti frekvenciatartományban. Ez az elektromágneses interferencia (EMI) közvetlenül csatolódik a tápvezetékekkel párhuzamosan futó, árnyékolatlan jelkábelekbe. A nagyfeszültségű ipari kapcsolóberendezések az átkapcsolási események során 50–200 V közötti feszültségtüskéket indukálhatnak a szomszédos kisfeszültségű vezérlővezetékeken. 

A hagyományos [behatolásjelző rendszerek](https://athenalarm.com/burglar-alarm/) analóg zónái nem rendelkeznek érdemi zajvédelemmel. Bármely indukált feszültség, amely meghaladja a riasztási központ detektálási küszöbértékét, téves zónariasztást eredményez a gyártóterületeken. A frekenciaváltó berendezések szélessávú vezetett zajt juttatnak a párhuzamos RS-485 nyomvonalakba, ami adatcsomag-sérülést és hibás triggerelést okoz.

Annak érdekében, hogy az integrátorok elkerüljék a visszatérő hibák miatti unbillable truck roll költségeket, differenciális jelátvitelt kell alkalmazniuk. Az RS-485 busz topológia differenciális jelátvitele 20–40 dB közös módusú zajelnyomást biztosít. Ez a védelem a könnyűipari környezetek többségében elegendő. A nehézipari üzemekben azonban a frekenciaváltó berendezések hálózati komponensei még mindig torzíthatják az adatkereteket, ha a kábelek elhelyezése nem megfelelő, vagy ha a buszhossz megközelíti a protokoll fizikai korlátait.

![Athenalarm AS-9000 riasztóközpont telepítési és kapcsolási rajza az ipari buszvezetékezés optimalizálásához](https://athenalarm.com/wp-content/uploads/2023/03/Athenalarm-burglar-alarm-manufacturer-scaled.jpg)

Az optikai Ethernet átviteli réteget alkalmazó IP multiplexelt architektúra teljesen kiküszöböli a vezetett elektromágneses interferenciát. Az optikai szálak nem tartalmaznak fémes vezetőket, így nem működnek antennaként a környezeti zajok számára. A hegesztőműhelyekben, transzformátorhelyiségekben és vegyipari feldolgozó zónákban az optikai gerinchálózati visszacsatolás jelenti az egyetlen olyan megoldást, amely szoftveres szűrési kompromisszumok nélkül is stabil működést garantál.

---

## Az RS-485 távolsági korlátai és a feszültségesésből adódó kihívások

Az EIA/TIA RS-485 szabvány 100 kbps sebesség mellett legfeljebb 1200 méteres kábelhosszt engedélyez megfelelően lezárt hálózatok esetén. A kereskedelmi riasztóközpontok alkalmazásában – ahol a buszsebesség jellemzően 9600 és 38400 baud között mozog – a valós működési korlát ismétlők nélkül 800–1000 méter. Ez a távolság jelentősen lecsökkenhet magas kábelkapacitás vagy helytelen lezáró ellenállások alkalmazása esetén.

A nagy kiterjedésű gyári kerítések vagy a különálló raktárépületek esetében ez a távolsági korlát kritikus telepítési akadályt jelent. A leggyakoribb helyszíni hiba a legtávolabbi csomópontok időszakos offline állapota. Ezek a hibák a beüzemelés során ritkán jelentkeznek, azonban a kábelköpeny elöregedése és a nedvességtartalom változása miatt a kábellenállás megnövekszik, ami előidézi a hibajelenséget. Bár a vonali jelismétlők alkalmasak a jel regenerálására és a fizikai távolság meghosszabbítására, minden egyes ismétlő 1–3 ms fix késleltetést ad a kommunikációhoz, és újabb potenciális hibaforrást eredményez.

A feszültségesés jelenti a leggyakoribb és leginkább alulértékelt mérnöki problémát a nagy sűrűségű detektoros hálózatokban. Ez a probléma leggyakrabban teljes riasztási terhelés alatt jelentkezik, amikor a hurok összes érzékelője egyidejűleg éri el a maximális áramfelvételt.

A feszültségesés kiszámítására szolgáló standard mérnöki képlet:

$$V_{\text{feszültségesés}} = 2 \times I \times R \times L$$

Ahol:
* $I$ = a hurokban található összes csomópont egyidejű maximális áramfelvétele (Amperben)
* $R$ = a vezető méterenkénti ellenállása ($\Omega/\text{m}$), amelyet a vezeték keresztmetszete határoz meg
* $L$ = a központ és a legtávolabbi csomópont közötti fizikai távolság (meterben)
* A 2-es szorzó az oda- és visszatérő vezető ágakat képviseli

A riasztórendszerek telepítésénél gyakran alkalmazott 22 AWG keresztmetszetű sodrott rézvezeték ellenállása körülbelül $0,054\ \Omega/\text{m}$. Ez az érték 18 AWG keresztmetszetű vezeték esetében $0,021\ \Omega/\text{m}$-re csökken. A hosszú távú detektorhurkok súlyos feszültségveszteséget tapasztalnak teljes riasztási terhelés alatt. Ha egy 12 V DC névleges feszültségű buszrendszerben a távoli modulok feszültsége a 10,5 V DC minimális működési küszöbérték alá esik, az RS-485 busztranszceiverek kommunikációja megszakad. A feszültségesés mérsékelhető vastagabb vezetékek alkalmazásával, elosztott segédtápok beiktatásával, valamint a nagy sűrűségű zónák rövidebb alhurkokra történő szegmentálásával a busz izolációs modul segítségével.

---

## Hibrid RS-485 és IP multiplexelt architektúra

Az ipari létesítményekben a leghatékonyabb hálózati topológiát a többrétegű hibrid rendszerek biztosíták. Ez a struktúra épületenként elkülönített helyi RS-485 busz topológia hurokból áll, amelyek IP-alapú zónabővítő moduloknál aggregálódnak. Az aggregációs részer az üzem meglévő LAN hálózatát vagy optikai gerinchálózati visszacsatolás infrastruktúráját használja a központi vezérlőpanel felé történő adattovábbításra.

![Athenalarm hálózati riasztásfelügyeleti rendszer architektúra diagramja az IP-alapú aggregáció szemléltetésére](https://athenalarm.com/wp-content/uploads/2022/05/Athenalarm-network-alarm-monitoring-system-1-1024.jpg)

Ez a hibrid tervezési megközelítés három alapvető fizikai korlátot old meg egyszerre:
1. **Távolság leküzdése:** Minden helyi RS-485 szegmens az adott épületen belül marad, hossza nem haladja meg a 200–400 métert, ami stabil jelszinteket garantál. Az IP-réteg ezt követően tetszőleges távolságra továbbítja az adatokat.
2. **Zónakapacitás növelése:** Egyetlen központi [RS-485 riasztóbuszon](https://athenalarm.com/burglar-alarm/intrusion-alarm-panel/alarm-control-panel/) a fizikai címek száma korlátozott. Az IP-alapú zónabővítők alkalmazásával azonban több ezer zóna integrálható egyetlen felügyeleti rendszerbe.
3. **Hibaelkülönítés és redundancia:** Az egyik épületben keletkező kábelvágás vagy zárlat nem befolyásolja a többi épület zónáinak működését, mivel az IP-modulok közötti hálózati kapcsolatok egymástól teljesen függetlenek.

Az [Athenalarm kereskedelmi behatolásjelző platformjai](https://athenalarm.com/burglar-alarm/intrusion-alarm-panel/alarm-control-panel/) natív módon támogatják ezt a skálázható megközelítést. A telepítés során a helyi hurkok ellenőrzése és címzése külön egységként történik, majd az IP-modul csatlakoztatásával a központ az egyes épületeket nagy kapacitású logikai egységként kezeli.

![Athenalarm hibrid hálózati riasztó vezérlőpanel ipari zónaaggregációs modulokkal felszerelve](https://athenalarm.com/wp-content/uploads/2022/02/Athenalarm-alarm-control-panel.jpg)

Fontos mérnöki szempont, hogy ez az architektúra nagymértékben függ a gyári LAN hálózat rendelkezésre állásától. Olyan létesítményekben, ahol az IT-biztonsági szabályzatok szigorúak, javasolt dedikált biztonsági VLAN vagy teljesen elkülönített fizikai hálózat kiépítése az integrációs konfliktusok elkerülése érdekében.

### Kommunikációs architektúrák műszaki összehasonlítása

| Műszaki paraméter | Hagyományos analóg zónák | Ipari RS-485 busz topológia | IP multiplexelt architektúra |
| :--- | :--- | :--- | :--- |
| **Maximális topológiai távolság** | ~300 m (hurokellenállás korlát) | Max. 1200 m szegmensenként ismétlő nélkül | Korlátlan a LAN/optikai gerinchálózat révén |
| **Maximális zónakapacitás** | 1 zóna vezetékes nyomvonalanként | 128–256 csomópont hurkonként (központfüggő) | Több ezer zóna IP-aggregátorokon keresztül |
| **Zajvédelem (EMI/RFI)** | Gyenge – érzékeny az indukált feszültségre | Magas – a differenciális jelátvitel elnyomja a zajt | Kiváló – galvanikusan leválasztott optikai média |
| **Hibatűrő redundancia** | Nincs – a vezető szakadása letiltja a zónát | Busz izolációs modulok – zárlat korlátozása a szegmensre | Kettős útvonal / Spanning Tree Protocol (STP) |
| **Diagnosztikai képesség** | Bináris: kizárólag szakadás vagy zárlat | Csomóponti szint: cím, állapot, szabotázs, tápfeszültség | Csomagszintű telemetria, valós idejű IP ping és heartbeat |
| **Tényező alapú TCO (10 év)** | Magas – bővítés esetén teljes újrakábelezés szükséges | Közepes – moduláris bővítés a buszkapacitáson belül | Alacsony – szoftveres bővítés fizikai kábelezés nélkül |

---

## SIA DC-09 és távfelügyeleti integráció

A legacy Contact ID protokoll analóg telefonvonalakon keresztül, DTMF hangfrekvenciás jelekkel továbbítja a riasztási eseményeket. Egy teljes esemény átvitele 3–8 másodpercet vesz igénybe a PSTN kapcsolaton keresztül. Ez a sávszélesség nem elegendő egy olyan ipari behatolásjelző rendszerben, amely egy kerületi incidens során egyidejűleg több tucat zónariasztást – optikai sorompók, mozgásérzékelők és szabotázsjelzések láncolatát – generál.

A SIA DC-09 egy natív IP-jelentési protokoll, amely strukturált adatcsomagokat továbbít közvetlenül TCP vagy UDP kapcsolatokon keresztül a távfelügyeleti vevőegységnek. Minden csomag tartalmazza az ügyfélkódot, a milliszekundumos felbontású időbélyeget, az eseménykódot és a kiterjesztett adatmezőket.

A SIA DC-09 ipari alkalmazásának fő előnyei:
* **Adatbiztonság:** Támogatja az eseményadatok AES-256 szabvány szerinti titkosítását.
* **Kézbesítési nyugtázás:** Tartalmazza a vevőoldali visszaigazolást, így hiba esetén a központ azonnal képes újrapróbálkozni.
* **Szöveges azonosítás:** Lehetővé teszi a részletes szöveges zónacímkék közvetlen átvitelét, megkönnyítve a diszpécserek munkáját.

A kritikus fontosságú gyári környezetekben a kettős kommunikációs modul alkalmazása kötelező mérnöki előírás. A vállalati WAN-kimaradások egypontos hibalehetőséget hoznak létre a riasztási jelentésekben. A kettős kommunikációs modul biztosítja, hogy az elsődleges LAN útvonal meghibásodása esetén a rendszer automatikusan és késleltetés nélkül átváltson a másodlagos 4G LTE mobilhálózati útvonalra, miközben a felügyeleti központ folyamatos heartbeat üzenetekkel ellenőrzi mindkét csatorna integritását.

---

## SCADA, épületfelügyeleti rendszer és CCTV riasztási integráció

Nagyobb gyártólétesítmények esetében alapvető követelmény, hogy a biztonsági rendszerek képesek legyenek együttműködni az operatív technológiai (OT) infrastruktúrával.

![Hálózati ipari riasztásfelügyeleti rendszer integrációs diagramja internetes felületen keresztül](https://athenalarm.com/wp-content/uploads/2022/05/Network-alarm-monitoring-system-diagram-01-1024.jpg)

### Modbus-TCP integráció SCADA platformokkal
A biztonsági központok Modbus-TCP interfésze lehetővé teszi a SCADA rendszerek számára, hogy regiszterértékek formájában olvassák a zónák állapotát és a rendszer egészségi adatait. A SCADA platform meghatározott időközönként (jellemzően 1–5 másodperc) lekérdezi a riasztóközpont regisztereit. Az adatok alapján automatizált folyamatleállításokat, vészvilágítás-aktiválást vagy zónalezárásokat képes végrehajtani veszélyes üzemekben.

### ONVIF Profile S videó-verifikáció
A kerületi védelmi vonalon (pl. infravörös sorompó aktiválódása) történő események esetén a riasztórendszernek közvetlenül vezérelnie kell a legközelebbi PTZ kamerákat. Az ONVIF Profile S szabvány alkalmazásával a riasztóközpont vagy annak IP-kommunikációs modulja közvetlen parancsokat küld a videómenedzsment-rendszernek (VMS), meghatározva a célzott kamera IP-címét és a szükséges PTZ preset pozíciót.

Az [Athenalarm platform](https://athenalarm.com/) natív SDK könyvtárakat és REST API végpontokat biztosít az integrátorok számára. Ez lehetővé teszi, hogy a behatolásjelző rendszert egyedi szoftveres felületekbe vagy PSIM (Physical Security Information Management) platformokba ágyazzák, ami jelentős versenyelőnyt biztosít a komplex ipari tendereken.

---

## Strukturált hibaelhárítási keretrendszer a távoli csomópontok hibáihoz

A nedvesség okozta kábellenállás szakaszos távoli csomópont offline hibákat eredményezhet az ipari hurkokban. A hibák okainak (feszültségesés, EMI vagy földelési hiba) pontos behatárolásához a helyszíni mérnököknek az alábbi szekvenciális diagnosztikai protokollt kell követniük.

* **1. lépés:** Mérje meg a DC feszültséget egy digitális multiméterrel az érintett offline csomópont tápcsatlakozóin. A mért érték alapján kövesse a megfelelő diagnosztikai ágat:

### A diagnosztikai ág: A mért feszültség < 10,5V DC (Súlyos feszültséghiány)
A csomópont tápfeszültsége a transzceiver működési küszöbértéke alatt van, ami túlzott feszültségesésre utal. Hajtsa végre a következő lépéseket:
* **Vezeték keresztmetszet ellenőrzése:** Vizsgálja felül, hogy a nyomvonalon alkalmazott kábel keresztmetszete megfelel-e a távolságnak (alkalmazzon 18 AWG vagy 16 AWG kábelt a 22 AWG helyett).
* **Áramfelvétel mérése:** Ellenőrizze, hogy a hurokhoz csatlakozó eszközök összesített áramfelvétele nem haladja-e meg a tápegység névleges kapacitását.
* **Vonali jelismétlő beépítése:** Hosszú szakaszok esetén helyezzen el egy RS-485 jelismétlőt a jelszintek helyreállítására.
* **Földhurok ellenőrzése:** Mérje meg, hogy nincs-e kóbor áram az árnyékoláson az eltérő földelési potenciálok miatt.
* **Segédtápegységek telepítése:** Helyezzen el elosztott kiegészítő tápegységeket a hurok felezőpontjánál vagy a távoli szegmenseknél a helyi feszültségszint növelésére.

### B diagnosztikai ág: A mért feszültség 10,5V és 11,5V DC között van (Kritikus tartomány)
A csomópont egy instabil működési zónában van, ami terhelésnövekedés esetén kommunikációs hibát okoz. Hajtsa végre a következő megelőző intézkedéseket:
* **Teljes terhelési teszt:** Aktiválja az összes detektort és kimeneti relét egyidejűleg, és kövesse nyomon a feszültség további csökkenését.
* **Kábelcsere ütemezése:** Tervezze meg a hurok érintett szakaszának átkábelezését nagyobb keresztmetszetű vezetőre a következő ütemezett gyári karbantartás során.

### C diagnosztikai ág: A mért feszültség ≥ 11,5V DC (Megfelelő tápellátás / Jelprobléma)
A tápellátás megfelelő, a hibát digitális jeltorzulás, EMI vagy címzési konfliktus okozza. Hajtsa végre a következő mélyreható vizsgálatokat:
* **AC búgófeszültség mérése:** Ellenőrizze oszcilloszkóppal vagy multiméterrel a frekenciaváltó berendezések által indukált magas frekvenciás váltakozó áramú zaj jelenlétét a jelvezetékeken.
* **Buszlezárás ellenőrzése:** Győződjön meg arról, hogy az RS-485 busz fizikai végpontjain elhelyezett $120\ \Omega$-os lezáró ellenállások értéke és jelenléte megfelelő.
* **Címzési audit:** Ellenőrizze a hardveres DIP-kapcsolók beállításait a hurokban található eszközökön az azonos buszcímekből adódó ütközések kiszűrésére.
* **Árnyékolás folytonosság vizsgálata:** Biztosítsa, hogy az árnyékolt sodrott érpár kábel árnyékolása a teljes nyomvonalon folytonos legyen, és kizárólag a központi riasztópanel felőli végén csatlakozzon a földeléshez.

![Kettős kommunikációt alkalmazó hálózati riasztásfelügyeleti rendszer diagramja 4G mobilhálózati tartalékúttal](https://athenalarm.com/wp-content/uploads/2022/05/Network-alarm-monitoring-system-diagram-06-1024.jpg)

---

## Kereskedelmi érték a disztribútorok és B2B importőrök számára

A strukturált, moduláris felépítésű riasztórendszerek jelentős gazdasági előnyt biztosítanak a disztribútorok számára az eszközök raktározása és forgási sebessége terén. Ahelyett, hogy különböző méretű (16, 64 vagy 256 zónás) fix központokat tartanának készleten, a moduláris felépítés lehetővé teszi, hogy egyetlen univerzális alapközpontot egészítsenek ki RS-485 bővítőkkel vagy IP-modulokkal a projekt méretétől függően. Ez minimalizálja a raktározott SKU-k számát és csökkenti az avulási kockázatot.

A végfelhasználók számára a 10 éves teljes birtoklási költség (TCO) optimalizálása jelenti a legerősebb pénzügyi érvet. Az open-architecture alapú RS-485 busz topológia és a szabványos SIA DC-09 protokoll alkalmazása biztosítja, hogy a gyár későbbi bővítései során ne legyen szükség a teljes rendszer cseréjére. A nyílt szabványok megvédik a beruházást a gyártóspecifikus termékkivezetésektől, és lehetővé teszik a rugalmas távfelügyeleti szolgáltatóváltást is.

---

## Műszaki FAQ ipari beszerzési menedzserek számára

**Kérdés: Képes-e az RS-485 busz topológia alapú riasztórendszer kezelni a videó-verifikációs adatfolyamokat?**
**Válasz:** Igen, mivel a videóátvitel dedikáltan az IP-rétegen történik, nem pedig magán az RS-485 buszon. Az RS-485 hurok kizárólag a zónariasztási eseményeket és metaadatokat továbbítja a központnak, amely ezzel párhuzamosan ONVIF Profile S parancsokat küld a VMS felé a helyi IP-hálózaton keresztül. A két hálózati réteg egymástól függetlenül működik.

**Kérdés: Hogyan védik meg a busz izolációs modulok a gyári hálózatok integritását?**
**Válasz:** A busz izolációs modul folyamatosan felügyeli a leágazó RS-485 szegmens vonali impedanciáját és feszültségszintjét. Ha a külső nyomvonalon zárlat vagy fizikai sérülés keletkezik, a modul milliszekundumokon belül lekapcsolja a meghibásodott szakaszt, így a busz többi része zavartalanul üzemel tovább.

**Kérdés: Miért kötelező a SIA DC-09 alkalmazása a Contact ID protokollal szemben ipari környezetben?**
**Válasz:** A SIA DC-09 natív IP-alapú protokollként ezredmásodperces időbélyeget, AES-256 titkosítást és azonnali kézbesítési nyugtázást biztosít. A Contact ID analóg DTMF hangátvitelre épül, amelynek 3–8 másodperces ciklusideje képtelen kezelni a nagy ipari komplexumokban egy perimeter incidens során fellépő egyidejű eseményáradatot.

**Kérdés: Milyen minimális vezeték-keresztmetszet ajánlott 300 métert meghaladó gyári RS-485 szakaszokhoz?**
**Válasz:** A 300 és 800 méter közötti szakaszokon a 18 AWG méretű árnyékolt sodrott érpár kábel alkalmazása a kötelező mérnöki minimum. Amennyiben a nyomvonal hossza megközelíti az 1000 métert, vagy a csomópontok száma meghaladja a 40 egységet, 16 AWG méretű kábel szükséges a teljes terhelés melletti feszültségesés kompenzálására.

**Kérdés: Hogyan befolyásolja a frekenciaváltó eszközök jelenléte a mozgásérzékelők kiválasztását?**
**Válasz:** A frekenciaváltó közelében elhelyezett érzékelőknek emelt szintű EMI-szűréssel és digitális jelfeldolgozással kell rendelkezniük. A téves riasztások elkerülése érdekében kombinált (PIR + mikrohullámú) technológiát alkalmazó, ipari kivitelű detektorok telepítése szükséges, amelyek szűrik a motorok indításakor fellépő elektromos tranzienseket.

---

## Mérnöki fogalomtár és hivatkozási mátrix

* **RS-485 busz topológia:** Kétvezetékes differenciális soros kommunikációs szabvány, amely max. 1200 méteres hosszig biztosít terepi eszköz-kommunikációt.
* **IP multiplexelt architektúra:** Olyan hálózati struktúra, amely az IP-alapú csomagkapcsolt adatátvitelt használja a helyi riasztási zónák aggregálására és központosítására.
* **busz izolációs modul:** Olyan elektronikus védelmi eszköz, amely zárlat vagy hiba esetén leválasztja a sérült buszszakaszt a fővonal védelme érdekében.
* **feszültségesés:** A vezető ellenállása miatt fellépő feszültségcsökkenés a forrás és a távoli fogyasztó között, amely kritikus szint alatt eszközleállást okoz.
* **kettős kommunikációs modul:** Olyan átviteli hardver, amely egyidejűleg IP (LAN) és mobilhálózati (LTE) útvonalon is fenntartja a távfelügyeleti kapcsolatot.
* **földhurok:** Olyan nemkívánatos elektromos áramút, amely az eltérő pontokon leföldelt árnyékolások között alakul ki, 50/60 Hz-es zajt indukálva a jelvezetékben.
* **árnyékolt sodrott érpár:** Olyan kábeltípus, amelynél a csavart érstruktúra és a külső fémfólia együttesen biztosít védelmet a környezeti EMI zajok ellen.
* **SIA DC-09:** Titkosított, natív IP-alapú riasztási adatátviteli szabvány felügyeleti központok részére.
* **Contact ID:** Korábbi, DTMF hangfrekvenciás alapú analóg riasztásjelentési protokoll.
* **Modbus-TCP:** Nyílt ipari kommunikációs protokoll, amely lehetővé teszi a riasztási regiszterek közvetlen beolvasását SCADA rendszerekbe.
* **ONVIF Profile S:** Szabványosított IP-videó protokoll, amely biztosítja a riasztásvezérelt PTZ kameramozgatást és rögzítésindítást.
* **frekenciaváltó:** Ipari motorvezérlő elektronika, amely jelentős szélessávú vezetett és sugárzott elektromágneses zajt (EMI) termel.
* **SCADA:** Ipari folyamatfelügyelő és adatgyűjtő számítógépes rendszer.
* **épületfelügyeleti rendszer:** Az épületek gépészeti és elektromos funkcióit automatizáló és ellenőrző központi rendszer.
* **optikai gerinchálózati visszacsatolás:** Nagy távolságú, zavarvédett optikai adatátviteli gerincvonal a helyi hálózati szegmensek és a központ között.

---

Az Athenalarm professzionális behatolásjelző gyártó és kereskedelmi biztonságtechnikai beszállító. Címezhető riasztóközpontokat, hálózati riasztásfelügyeleti infrastruktúrát, valamint OEM/ODM fejlesztési szolgáltatásokat biztosít globális disztribútorok, integrátorok és távfelügyeleti állomások számára. A részletes specifikációk és a telepítési útmutatók elérhetők az [Athenalarm műszaki támogatási portálon](https://athenalarm.com/athenalarm-technical-documents/technical-support/).
