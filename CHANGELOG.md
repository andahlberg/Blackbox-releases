# Ändringslogg

Alla versioner av Blackbox. Installationsprogrammen finns i [Blackbox-releases](https://github.com/andahlberg/Blackbox-releases/releases). Från 0.2.3 kan en administratör uppdatera inifrån appen, under *Uppdatera* i menyn.

## 0.2.6 – 2026-10-02

### Rättat
- **Overlayen är genomskinlig på riktigt.** Bara texten syns, och det som ligger under overlayen syns igenom. I 0.2.5 blev bakgrunden svart.
- **En skadad lokal historik** läggs nu undan automatiskt som `history.skadad-<datum>.db`, och inspelningen fortsätter i en ny fil. Tidigare visades samma fel varje sekund. Den lokala historiken används när bakgrundstjänsten inte är installerad.

### Ändrat
- **Graferna är tomma där inget spelades in**, till exempel när datorn var avstängd eller sov. Tidigare ritades en linje på noll. Det gäller även kärnornas färgremsa.
- **Tjänster:** starttypen visas som en färgad etikett.
  - Automatisk: grön
  - Manuell: blå
  - Inaktiverad: orange
  - Start: lila
  - System: turkos
  - Okänd: röd
- **Hälsa** har två kolumner och mindre tom yta.
  - Till vänster: tabellerna för uppstart och viloläge.
  - Till höger: uppstartsgrafen, diskarnas hälsa och anslutningen som kompakta kort.
- **Disk Analys** har mindre tom yta.
  - Analysens nyckeltal står bredvid diskrutan.
  - Sidopanelen visas bara när något är markerat.
  - Tabellerna fördelar bredden bättre.

## 0.2.5 – 2026-10-02

### Säkerhet
Efter en säkerhetsgranskning av hela koden:
- **Uppdateringen** laddas nu ner och kontrolleras av Blackbox egen bakgrundsdel med administratörsrätt, i en mapp som bara administratörer kan skriva i. Tidigare låg filen i användarens temp-mapp, där ett skadligt program kunde byta ut den medan frågan om administratörsbehörighet visades.
- **Bakgrundstjänsten kraschar inte längre** av en fil med ett omöjligt datum eller av konstiga värden i Windows loggar. Tidigare kunde vem som helst stoppa inspelningen så.
- **Falska händelser:** Application-loggen kan alla program skriva i. Från den sparas nu högst 300 händelser per källa och timme, och assistenten får veta att de kan vara förfalskade.
- **Som administratör sparar appen ingenting i profilmappen** (tema, overlay och kolumnbredder gäller bara sessionen), och dumpfiler hamnar i `C:\Windows\Temp`.
- **Privata mappar utanför `C:\Users`** syns inte längre med innehåll för andra användare i Disk Analys.
- **Mindre rättningar:**
  - Installationen stänger bara Blackbox egen process.
  - Livedata återhämtar sig om något upptar dess namn.
  - Bara riktiga versionsnummer godtas vid uppdatering.

### Nytt
- **Klicka på ett fynd i Översikt** för att öppna det i Diagnos, utfällt.
- **Autostart:**
  - Sortera på namn, utgivare, status, just nu eller plats.
  - Status visas som en grön eller röd etikett.

### Ändrat
- **Overlayen** har ingen bakgrund och ingen ram, bara texten med en svag skugga.
  - Valen ligger i en panel med kryssrutor, som öppnas bredvid overlayen och stannar kvar tills du klickar utanför.
- **Diagnos:** tätare fyndkort.
  - Orsakerna tar en rad var.
  - Råden står under mätvärdena.
  - Kolumnerna fyller bredden.

## 0.2.4 – 2026-10-01

### Nytt
- **Overlay:** ett litet fönster som alltid ligger överst på skärmen och visar de värden du bockar i. Du kan välja processor, minne, disk, nätverk, GPU, processorns effekt, temperatur och de program som använder mest CPU och minne. Välj under *Overlay* i menyn eller högerklicka på overlayen. Den går att dra vart som helst och kommer ihåg vad den visar och var den står. Värdena uppdateras varje sekund utan att overlayen tar fokus.

### Ändrat
- **Autostart:** *Aktivera* och *Inaktivera* lyser bara när de ändrar något. På en rad som redan är inaktiverad är *Inaktivera* grå.
- **Tjänster:** *Starta* är grå på en tjänst som redan körs. *Stoppa* och *Starta om* är grå på en stoppad tjänst.

### Rättat
- **Installationen hängde sig** när den inte kunde stänga en äldre Blackbox. Nu väntar den högst tre sekunder och stänger sedan appen med tvång. Appens data sparas av bakgrundstjänsten, så inget går förlorat.
- **Bakgrundstjänsten kunde bli stoppad** om installationen avbröts. Nu startas den igen.

## 0.2.3 – 2026-10-01

### Nytt
- **Uppdateringar inifrån appen.** Under *Uppdatera* i menyn kan en administratör söka efter en ny version och installera den. Appen laddar ner filen, kontrollerar SHA-256-summan, ber om administratörsbehörighet, installerar och startar om. Historiken behålls.
  - Att söka automatiskt varje dygn är avstängt från början. Det gäller hela datorn och slås på i samma meny, eller vid installation med `/AUTOUPDATE=1`.
  - Användare utan administratörsrätt ser ingenting om uppdateringar.
- **Avsluta flera processer samtidigt:** markera dem med Ctrl- eller Shift-klick. Markeringen följer processerna när listan sorteras om. Fler än en bekräftas först.
- **Nytt utseende på alla sidor:** Diagnos, Hälsa, Assistent, Processer, Autostart och Tjänster har fått nyckeltalsrutor och paneler som Översikt.

### Rättat
- **Installationen kunde inte stänga Blackbox**, eftersom krysset bara gömmer appen i meddelandefältet. Nu avslutas appen när installationen ber den att stänga.
- **Tomrummet ovanför sidrubrikerna är borta.** Dolda meddelanderader tog plats på varje sida.
- **Rutan för viloläge i Hälsa** räknar bara viloperioder på minst 30 minuter, som diagnosregeln gör. Annars blev värdet missvisande högt.

## 0.2.1 – 2026-10-01

### Ändrat
- **Assistenten använder OpenAI** (modellen `gpt-5`) i stället för Claude. Skapa en nyckel på platform.openai.com och lägg in den under *Assistent*. Nyckeln tas bort automatiskt efter en timme.
- **Disk Analys** har fått det nya utseendet: diskarna som rutor, och analysen och detaljerna i paneler.
- **Översikt:**
  - Listan med alla program och händelser ligger bredvid fynden.
  - Knapparna för spåren har spårets egen färg.

### Rättat
- **Graferna** går ner till noll där inget spelades in, i stället för att dra ett streck över luckan.

## 0.2.0 – 2026-10-01

### Nytt
- **Nytt utseende ("Instrumentpanel"):** mörka paneler, orange accentfärg och menyn överst.
- **Ny Översikt:**
  - Åtta nyckeltal med senaste minuten.
  - En tidslinje med alla spår, som kan slås av och på, och kärnorna som en färgremsa.
  - En sidopanel med fynd, program och händelser för det valda tidsfönstret.
- **Hälsa:** uppstartstid och vad som bromsade, viloläge och batteri, diskarnas hälsa och anslutningen.
- **Nya regler:** långsam uppstart, viloläge som drar batteri, långsamt nätverk, diskhälsa och program som arbetar mer än vanligt.
- **Rapport:** exportera ett tidsfönster som HTML till IT-support, med personliga uppgifter maskerade.
- **Minivy:** ett klick på ikonen i meddelandefältet visar läget just nu.
- **Installerade uppdateringar och drivrutiner** syns på tidslinjen.
- **Kärntyp per kärna** (P- och E-kärnor) i processorns delgrafer.

### Ändrat
- **API-nyckeln** tas bort automatiskt efter en timme.

## 0.1.5 – 2026-09-30

### Nytt
- **Delgrafer i Översikt:** varje disk, nätverkskort, GPU-motor och kärna går att fälla ut.
- **Ikon i meddelandefältet:** krysset döljer fönstret, och inspelningen fortsätter.

### Ändrat
- **Minutsnitten sparas i 14 dagar** i stället för 30, och historiken är komprimerad.

## 0.1.0 – 2026-09-29

Första versionen med installationsprogram:
- Ersätter Aktivitetshanteraren: processer, prestanda, autostart och tjänster.
- Bakgrundstjänsten spelar in dygnet runt, så att du kan spola tillbaka i historiken.
- Regelmotorn förklarar varför datorn var seg.
- Strömövervakning och temperatur.
- AI-assistent.
- Disk Analys.
