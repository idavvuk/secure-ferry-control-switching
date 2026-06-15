# Säker Styrlägesväxling för Passagerarfärja

Kandidatarbete vid Chalmers tekniska högskola och Göteborgs Universitet, utvecklat i samarbete med CStrider och IFM Electronic.
 
## Översikt
 
Det här projektet implementerar ett säkerhetskritiskt system för att hantera övergångar mellan olika styrstationer på en liten autonom färja. Systemet säkerställer att exakt en styrstation har kontroll åt gången och att alla övergångar sker på ett säkert och deterministiskt sätt.
 
Systemet är implementerat i CoDeSys och körs på en IFM CR710S styrenhet med två separata PLCer, en Standard PLC för styrlogik och en Safety PLC för övervakning.
 
## Styrstationer
Systemet stödjer följande styrstationer:
 
- **Manuell**: fysisk körstation ombord på färjan
- **Fjärr (Remote)**: körstation på land
- **Autonom (Auto)**: autonom styrning
- **Mobil fjärr (Remote Mobile)**: mobil fjärrstyrning

## Systemarkitektur
Systemet är uppdelat enligt designmönstret monitor-actuator:
 
- **ActuationChannel** (Standard PLC): hanterar förfrågningar om kontroll och genomför övergångar mellan styrstationer
- **MonitoringChannel** (Safety PLC): övervakar systemets hälsa via heartbeat-signaler och kan utlösa nödavstängning

## Säkerhetsfunktioner

- Heartbeat-övervakning för varje styrstation — om aktiv stations heartbeat slutar fungera går systemet direkt till FAILSAFE
- IntegrityCheck blockerar motstridiga signaler innan de når styrlogiken
- Timeout-mekanism avbryter en påbörjad övergång om den inte slutförs i tid
- Safety PLC övervakar Standard PLC oberoende och kan utlösa nödlarm

### Krav
 
- CoDeSys V3.5 SP11 eller senare
- IFM CR710S hårdvara (eller CoDeSys simulator)
- IFM IOWrapper-bibliotek

## Begränsningar
 
- Systemet är implementerat och simulerat i CoDeSys — ej testat i full driftmiljö
- Fokus på funktionell säkerhet, ej cybersäkerhet
- Realtidsaspekter har ej beaktats
- Arkitekturen beskriver MVP-implementationen med manuell och fjärrstyrning som primära styrstationer

## Utvecklat av
Kandidatarbetesgrupp 20A, Chalmers tekniska högskola & Göteborgs Universitet. 
