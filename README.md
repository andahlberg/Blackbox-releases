# Blackbox – installationsprogram

Här finns installationsprogrammen för **Blackbox**, ett Windows-program som ersätter Aktivitetshanteraren och förklarar varför datorn är seg. Källkoden ligger i ett privat repo; det här repot innehåller bara färdiga versioner.

## Installera

1. Öppna [senaste versionen](https://github.com/andahlberg/Blackbox-releases/releases/latest) och ladda ner `Blackbox-<version>-setup.exe`.
2. Kör filen och godkänn frågan om administratörsbehörighet.
3. Programmet är inte signerat än, så Windows SmartScreen kan varna för en okänd utgivare: välj *Mer information* > *Kör ändå*.

Kontrollera gärna filen mot SHA-256-summan i `.sha256`-filen bredvid:

```powershell
Get-FileHash .\Blackbox-<version>-setup.exe -Algorithm SHA256
```

## Uppdateringar

Från version 0.2.2 letar Blackbox själv efter nya versioner här, vid start och en gång per dygn. När en ny finns visas en rad överst i appen med knappen *Uppdatera*. Historiken på datorn behålls vid uppdatering.
