# Riskbaserad tidplanering och optimering

### Utveckling av en stokastisk tidplansmodell för riskanalys, Monte Carlo-simulering och kostnadseffektiv projektstyrning

**Johan Jönsson | Lunds tekniska högskola (LTH) | 2026**

## Projektbeskrivning

Hur kan en projektorganisation utveckla en realistisk tidplan, bedöma risken för förseningar och identifiera vilka åtgärder som faktiskt är värda att genomföra?

I stora infrastrukturprojekt är tidplanering en central del av projektstyrningen. Traditionella deterministiska tidplaner ger en uppskattning av när projektet kan färdigställas, men tar inte fullt hänsyn till osäkerheter i aktiviteternas varaktigheter, gemensamma riskfaktorer eller hur förseningar kan spridas genom projektets aktivitetsnätverk.

Syftet med detta projekt är att demonstrera hur **riskbaserad tidplanering kan utvecklas från grundläggande projektdata till ett kvantitativt beslutsunderlag för projektledning och strategisk resursplanering**.

Arbetet omfattar hela analysprocessen: från rekonstruktion av en projekttidplan utifrån publicerade data och uppbyggnad av en fungerande tidplansmodell, till modellering av osäkerheter, Monte Carlo-simulering, analys av kritiska aktiviteter och utveckling av ekonomiskt motiverade åtgärdsstrategier.

Ett centralt fokus är att kombinera etablerade metoder för projektplanering med sannolikhetsteori, matematisk modellering och ekonomisk beslutsanalys. På så sätt kan projektets tidplan användas som mer än en statisk plan: den blir ett verktyg för att undersöka möjliga framtida utfall och jämföra konsekvenserna av olika beslut.

Projektet genomfördes inom kursen *Tillämpad riskutredning (VRSN60)* vid Lunds tekniska högskola och bygger på publicerade projektdata från ett verkligt infrastrukturprojekt i Nederländerna.

---

## Bakgrund – SAA-projektet

Fallstudien utgår från ett delprojekt inom det nederländska vägprogrammet **Schiphol–Amsterdam–Almere (SAA)**, ett omfattande infrastrukturprogram med syfte att förbättra vägkapacitet, framkomlighet och restider i Amsterdamregionen.

Analysen bygger på projektdata publicerade av Kammouh et al. (2022) i artikeln *Dynamic control for construction project scheduling on-the-run*.

Det publicerade materialet innehåller en förenklad representation av det verkliga projektet, där känslig information har modifierats av sekretesskäl.

Det tillgängliga underlaget omfattar:

- **37 projektaktiviteter** med tillhörande tidsuppskattningar och logiska beroenden.
- **14 gemensamma osäkerhetsfaktorer** som påverkar flera aktiviteter.
- **19 identifierade riskhändelser** med sannolikheter och möjliga tidskonsekvenser.
- **19 riskreducerande åtgärder** med uppskattade kostnader och tidsbesparingar.
- En planerad projektvaraktighet på **1 466 dagar**.
- Ett ekonomiskt incitament på **3 000 EUR per dag** vid tidigare eller senare färdigställande.

Den övergripande utmaningen är att utveckla en sammanhängande modell som fångar samspelet mellan dessa komponenter och sedan använda modellen för att bedöma vilka riskhanteringsåtgärder som ger störst nytta.

## 1. Konstruktion och utveckling av tidplansmodellen

Projektets första och mest grundläggande del bestod av att rekonstruera en fungerande tidplan utifrån publicerade projektdata.

Till skillnad från en analys där en redan färdigställd tidplan används som utgångspunkt behövde projektets aktivitetsstruktur, ordningsföljd, tidsuppskattningar och beroenden sammanställas och implementeras i ett tidplaneringsverktyg.

Tidplansmodellen utvecklades med utgångspunkt i rekommendationerna från **Project Management Institute (PMI), Practice Standard for Scheduling, Third Edition**.

### Modellering av aktivitetsnätverket

Projektet representeras som ett nätverk av aktiviteter där varje aktivitet har en definierad varaktighet och relationer till andra aktiviteter.

Genom att beskriva dessa relationer skapas en dynamisk tidplan där en aktivitets start- och sluttid bestäms av föregående aktiviteters färdigställande.

Detta är särskilt viktigt för större projekt där många aktiviteter genomförs parallellt och där förseningar i en del av projektet kan påverka flera efterföljande aktiviteter.

Tidplanen konstruerades därför så att aktiviteternas start- och sluttider i huvudsak beräknas utifrån aktivitetsnätverkets logiska struktur, snarare än genom individuellt låsta datum.

Denna konstruktion möjliggör att förändringar i aktiviteternas varaktigheter får genomslag i den övergripande tidplanen.

### Utveckling från deterministisk till stokastisk tidplan

Efter att den grundläggande tidplansmodellen hade etablerats utvecklades den vidare för att representera osäkerhet.

I stället för att anta att varje aktivitet tar ett exakt antal dagar tilldelades aktiviteterna sannolikhetsfördelningar baserade på trepunktsskattningar:

- Optimistisk varaktighet.
- Mest sannolik varaktighet.
- Pessimistisk varaktighet.

Triangelfördelningar användes huvudsakligen för att representera variationen i aktiviteternas varaktigheter.

Det innebär att varje simulering kan ge olika aktivitetstider och därmed en annan projektplan och sluttidpunkt.

Modellen kan således användas för att bedöma inte bara när projektet förväntas bli färdigt, utan även hur stor osäkerheten kring denna tidpunkt är.

## 2. Modellering av projektrisker och beroenden

En viktig del av utvecklingsarbetet var att integrera riskhändelser och gemensamma osäkerhetsfaktorer i tidplansmodellen.

I verkliga projekt påverkas aktiviteter sällan av helt oberoende osäkerheter. Exempelvis kan organisatoriska problem, resursbrist eller förändrade tekniska förutsättningar påverka flera aktiviteter samtidigt.

För att representera detta modellerades de 14 gemensamma osäkerhetsfaktorerna så att samma slumpmässiga utfall påverkar samtliga aktiviteter som är kopplade till respektive faktor.

Detta skapar samvariation mellan aktiviteternas varaktigheter och ger en mer sammanhängande representation av hur gemensamma projektförhållanden kan påverka tidplanen.

Därutöver modellerades de 19 identifierade riskhändelserna med sannolikheter för inträffande och tillhörande osäkra tidskonsekvenser.

På detta sätt integreras tre typer av tidsosäkerhet:

1. Osäkerhet i enskilda aktiviteters grundläggande varaktighet.
2. Gemensamma osäkerhetsfaktorer som påverkar flera aktiviteter.
3. Specifika riskhändelser som kan orsaka ytterligare förseningar.

Den resulterande modellen fångar därmed både direkta förseningar och hur deras konsekvenser påverkar projektets övergripande färdigställandetid genom aktivitetsnätverket.

## 3. Monte Carlo-simulering och tidsriskanalys

Den utvecklade tidplansmodellen analyserades genom Monte Carlo-simulering i programvaran **RiskyProject**.

För varje simulering genereras slumpmässiga aktivitetstider, gemensamma osäkerhetsutfall och eventuella riskhändelser. Därefter beräknas projektets totala varaktighet utifrån aktivitetsnätverkets beroenden.

Samtliga slutliga analyser genomfördes med **50 000 Monte Carlo-iterationer per modellkonfiguration**.

Genom simuleringarna kunde projektets färdigställandetid analyseras som en sannolikhetsfördelning i stället för ett enskilt deterministiskt datum.

Detta gör det möjligt att beräkna:

- Förväntad projekttid.
- Sannolikheten att färdigställa projektet före ett visst datum.
- Sannolikheten och omfattningen av förseningar.
- Percentiler för projekttiden, exempelvis P50 och P90.
- Variation i projektets ekonomiska utfall.
- Hur riskreducerande åtgärder påverkar fördelningen av möjliga sluttider.

Resultaten ger ett mer informativt underlag än traditionella deterministiska prognoser och gör det möjligt att bedöma hur stor tidsmässig osäkerhet som behöver hanteras genom projektstyrningen.

## 4. Kritiska aktiviteter och känslighetsanalys

En central fråga inom tidplanering är vilka aktiviteter som faktiskt påverkar projektets sluttid.

Den deterministiska kritiska linjen är inte nödvändigtvis densamma när aktiviteternas varaktigheter varierar.

I en stokastisk tidplan kan därför olika aktiviteter och aktivitetsvägar bli kritiska i olika simuleringar.

För att analysera detta användes två kompletterande mått.

### Kritikalitetsindex (Criticality Index)

Kritikalitetsindexet beskriver sannolikheten att en aktivitet ligger på en kritisk väg.

En aktivitet med ett kritikalitetsindex på exempelvis 80 % är kritisk i ungefär 80 % av simuleringarna.

Måttet gör det möjligt att identifiera aktiviteter där tidsreducerande åtgärder har störst potential att påverka projektets totala varaktighet.

### Känslighetsanalys

Som komplement analyserades sambandet mellan enskilda aktiviteters varaktigheter och projektets totala varaktighet genom Spearmans rangkorrelation.

Detta visar vilka aktiviteter vars tidsvariation samvarierar starkast med variationen i den totala projekttiden.

Genom att kombinera kritikalitetsindex och känslighetsanalys kan analysen skilja mellan aktiviteter som påverkar sluttiden direkt och aktiviteter som främst samvarierar med andra betydelsefulla projektförhållanden.

Detta är särskilt relevant för projektstyrning eftersom en aktivitet med stor tidsvariation inte nödvändigtvis är den aktivitet där extra resurser ger störst effekt.

## 5. Utveckling av kostnadseffektiva åtgärdsstrategier

Nästa steg var att använda den utvecklade tidplansmodellen för att identifiera vilka riskreducerande åtgärder som bör prioriteras.

Projektet omfattar 19 möjliga riskreducerande åtgärder, vilket motsvarar totalt **524 288 möjliga kombinationer**.

Att genomföra alla åtgärder kan ge en kortare projekttid, men också mycket stora kostnader.

Samtidigt kan vissa åtgärder vara relativt billiga men sakna betydelse för projektets sluttid eftersom de berörda aktiviteterna inte ligger på någon kritisk väg.

För att hantera detta utvecklades en stegvis metod för urval och utvärdering av åtgärdspaket.

### Kritikalitetsviktad kostnadseffektivitet

Utgångspunkten är att en aktivitets förkortning inte automatiskt ger samma reduktion av projektets totala varaktighet.

En aktivitet som inte är kritisk kan förkortas utan att projektet blir färdigt tidigare.

Därför kombinerades åtgärdernas förväntade tidsreduktion och kostnad med aktiviteternas kritikalitetsindex.

Det resulterande måttet uppskattar kostnaden per kritikalitetsviktad vunnen projektdag.

Eftersom varje dags avvikelse från den planerade sluttiden värderas till 3 000 EUR kunde detta användas som en initial gräns för att identifiera potentiellt kostnadseffektiva åtgärder.

### Matematisk analys och fördjupad optimering

För att motivera urvalsmetoden genomfördes även en matematisk analys av sambandet mellan kritikalitetsindex och förändringar i projektets förväntade varaktighet.

Under angivna antaganden härleddes att kritikalitetsindexet motsvarar den lokala känsligheten hos den förväntade projekttiden med avseende på en liten förkortning av aktiviteten.

Detta ger en matematisk grund för att använda kritikalitetsindex som en approximation av en åtgärds möjliga nytta.

Metoden utvecklades därefter genom:

- Ett initialt urval av kostnadseffektiva åtgärder.
- Ny simulering av tidplanen efter att åtgärderna inkluderats.
- Uppdatering av aktiviteternas kritikalitetsindex.
- Härledning och tillämpning av övre och undre gränser för åtgärdernas möjliga ekonomiska nytta.
- Identifiering av ytterligare åtgärder som kan vara motiverade att lägga till eller ta bort.
- Slutlig jämförelse av de utvalda alternativen genom Monte Carlo-simulering.

Detta är särskilt viktigt eftersom en åtgärd kan förändra vilka aktiviteter som blir kritiska.

En åtgärd som initialt bedöms vara mindre lönsam kan därmed bli intressant när andra aktiviteter redan har förkortats.

Metodiken gör det möjligt att systematiskt förbättra ett åtgärdspaket utan att behöva simulera samtliga möjliga kombinationer. Den ger dock inte någon garanti för att den globalt optimala kombinationen identifieras.

## 6. Resultat – jämförelse av åtgärdsstrategier

Resultaten visar tydligt hur riskbaserad tidplanering kan användas för att förbättra både projektets tidsmässiga och ekonomiska utfall.

| Åtgärdsstrategi | Förväntad projekttid | Förväntad nettokostnad |
|---|---:|---:|
| Inga åtgärder | 1 832 dagar | 1,098 MEUR |
| Samtliga åtgärder | 1 570 dagar | 4,734 MEUR |
| Endast åtgärder för kritiska aktiviteter | 1 570 dagar | 2,194 MEUR |
| Selektivt kostnadseffektivt åtgärdspaket | 1 663 dagar | 1,081 MEUR |
| Selektivt paket med extra underhållsingenjörer | 1 618 dagar | 1,092 MEUR |
| Selektivt paket utan kringutrustning i beredskap | 1 732 dagar | 1,085 MEUR |

*Den ekonomiska nettokostnaden omfattar kostnader för riskreducerande åtgärder samt tidsrelaterade kostnader eller belöningar vid avvikelse från den planerade projekttiden. Projektets ordinarie genomförandekostnader ingår inte.*

### Centrala resultat

**1. Alla åtgärder är inte ekonomiskt motiverade**

Att genomföra samtliga 19 åtgärder ger i princip samma förväntade projekttid som att endast genomföra åtgärder kopplade till kritiska aktiviteter.

Däremot är den förväntade kostnaden betydligt högre när samtliga åtgärder genomförs.

Detta illustrerar vikten av att analysera aktivitetsnätverkets kritikalitet innan resurser fördelas.

**2. Ett selektivt åtgärdspaket kan minska kostnaderna och samtidigt förbättra tidplanen**

Det initialt identifierade kostnadseffektiva åtgärdspaketet minskar den förväntade projekttiden från cirka 1 832 till 1 663 dagar.

Samtidigt blir den förväntade totala ekonomiska kostnaden något lägre än i alternativet utan åtgärder.

Detta visar att riskreducerande investeringar kan motiveras ekonomiskt när deras tidsmässiga effekter utvärderas på projektnivå.

**3. Ytterligare 45 dagars tidsreduktion till en begränsad merkostnad**

Den fördjupade analysen identifierade att komplettering av det selektiva åtgärdspaketet med extra underhållsingenjörer minskar den förväntade projekttiden med cirka 45 dagar.

Denna förbättring uppnås till en ökning av den förväntade nettokostnaden på endast cirka 10 300 EUR.

Detta illustrerar värdet av en iterativ analys där aktiviteternas kritikalitet och åtgärdernas kostnadseffektivitet omvärderas när tidplanen förändras.

Ingen av de analyserade strategierna gav dock en förväntad projekttid kortare än det ursprungliga målet på 1 466 dagar.

## 7. Metoder och verktyg

Projektet kombinerar etablerad metodik för tidplanering med kvantitativ riskanalys och matematisk beslutsmodellering.

**Projektplanering och modellutveckling**
- Konstruktion av aktivitetsnätverk och beroenderelationer.
- Critical Path Method (CPM).
- Tidplansmodellering enligt PMI:s *Practice Standard for Scheduling*.
- Utveckling av en stokastisk tidplansmodell utifrån publicerade projektdata.

**Sannolikhetsmodellering och simulering**
- Monte Carlo-simulering.
- Triangelfördelningar och jämförelse med beta-PERT.
- Modellering av gemensamma osäkerhetsfaktorer.
- Sannolikhetsbaserad modellering av riskhändelser.
- Analys av fördelningar för färdigställandetid och ekonomiskt utfall.

**Kritikalitetsanalys och optimering**
- Criticality Index.
- Spearmans rangkorrelation.
- Känslighetsanalys.
- Matematiska approximationer av åtgärders tidsmässiga nytta.
- Analytiska gränser för kostnadseffektivitet.
- Stegvis utveckling och jämförelse av åtgärdspaket.

**Programvara**
- RiskyProject för modellering och Monte Carlo-simulering av projekttidplanen.
- Kalkylbladsbaserad bearbetning och sammanställning av simuleringsresultat.
- LaTeX för matematisk dokumentation och rapportframställning.

## 8. Praktisk tillämpning inom projektstyrning

Den viktigaste tillämpningen är att använda kvantitativ tidsriskanalys som ett stöd för beslut under planering och genomförande av komplexa projekt.

En deterministisk tidplan visar när projektet förväntas färdigställas utifrån givna antaganden. En riskbaserad tidplansmodell kompletterar detta genom att beskriva osäkerheten kring sluttiden och hur olika beslut kan påverka den.

Metodiken kan därmed stödja projektledare och beslutsfattare i flera centrala frågor:

- **Realistisk tidplanering:** Hur sannolikt är det att projektet kan färdigställas enligt den planerade tidplanen?
- **Tidig identifiering av risker:** Vilka aktiviteter och riskfaktorer är särskilt betydelsefulla för möjliga förseningar?
- **Effektiv resursfördelning:** Var kan ytterligare resurser ge störst påverkan på projektets sluttid?
- **Ekonomisk prioritering:** Vilka tidsreducerande åtgärder är ekonomiskt motiverade?
- **Jämförelse av strategier:** Hur påverkas projektets tids- och kostnadsfördelningar av olika åtgärdspaket?
- **Löpande riskstyrning:** Hur kan tidplansanalysen uppdateras när ny information om projektets genomförande blir tillgänglig?

Den utvecklade modellen illustrerar hur dessa frågor kan behandlas inom en sammanhängande analysprocess.

Metodiken är särskilt relevant för större bygg-, anläggnings- och infrastrukturprojekt där många aktiviteter är beroende av varandra, där tidsosäkerheten är betydande och där förseningar har ekonomiska konsekvenser.

## 9. Begränsningar och vidareutveckling

Analysen bygger på en publicerad och förenklad representation av SAA-projektet. Resultaten ska därför främst ses som en tillämpning av riskbaserad tidplanering på ett realistiskt fall, snarare än en fullständig analys av det verkliga projektets genomförande.

Tidplansmodellen omfattar projektets övergripande aktivitetsnätverk och de risker, osäkerhetsfaktorer och åtgärder som ingår i det publicerade underlaget.

Modellen representerar inte alla tekniska, organisatoriska eller ekonomiska samband som förekommer i verkliga infrastrukturprojekt.

Åtgärdsoptimeringen är dessutom stegvis och approximativ. Metoden används för att identifiera lovande strategier, men ger inte någon matematisk garanti för ett globalt kostnadsminimum.

Möjliga vidareutvecklingar omfattar:

- Automatisering av modellkonstruktion och simulering.
- Integration med mer detaljerade tidplaner och aktivitetsdata.
- Löpande uppdatering av sannolikhetsfördelningar utifrån faktiskt projektutfall.
- Utveckling av mer avancerade beroendemodeller för gemensamma riskfaktorer.
- Fortsatt utveckling av algoritmer för att identifiera kostnadseffektiva åtgärdskombinationer.
- Integration av riskbaserad tidplanering i kontinuerlig projektuppföljning och beslutsstöd.

## 10. Slutsats

Projektet demonstrerar hur traditionell projektplanering kan utvecklas till en mer avancerad, riskbaserad modell för analys och styrning av komplexa projekt.

Genom att kombinera **tidplanskonstruktion, sannolikhetsmodellering, Monte Carlo-simulering, kritikalitetsanalys och ekonomisk optimering** kan projektets tidplan användas för att identifiera var insatser har störst förväntad effekt.

Resultaten visar att fler riskreducerande åtgärder inte nödvändigtvis innebär bättre projektstyrning. Det avgörande är i stället att förstå vilka aktiviteter som faktiskt påverkar projektets sluttid och hur kostnaderna för att förkorta dessa står i relation till den förväntade nyttan.

Arbetet illustrerar därmed hur kvantitativa metoder kan bidra till **mer realistiska tidplaner, effektivare resursfördelning och bättre underbyggda beslut om tid, risk och kostnad**.

---

## Referenser

**Kammouh, O., Nogal, M., Binnekamp, R., & Wolfert, A. R. M. (2022).**  
*Dynamic control for construction project scheduling on-the-run.*  
Automation in Construction, 141, 104450.  
https://doi.org/10.1016/j.autcon.2022.104450

**Project Management Institute (2019).**  
*Practice Standard for Scheduling*, Third Edition.  
Project Management Institute.

## Om projektet

Projektet genomfördes under hösten 2026 som en del av kursen **VRSN60 – Tillämpad riskutredning (7,5 hp)** vid Avdelningen för riskhantering och samhällssäkerhet, Lunds tekniska högskola.

Fallstudien bygger på publicerat forskningsmaterial. Analysen har genomförts som ett akademiskt projekt och utgör inte ett officiellt beslutsunderlag framtaget på uppdrag av Rijkswaterstaat.

**Författare:** Johan Jönsson  
**Område:** Projektstyrning, riskbaserad tidplanering, Monte Carlo-simulering och kvantitativ riskanalys.
