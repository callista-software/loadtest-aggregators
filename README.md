loadtest-aggregators
====================

Detta projekt är ett [jmeter](http://jmeter.apache.org/) projekt som används för att last- och robusthetstesta agregerande tjänster i den [nationella tjänsteplattformen (NTjP)](https://skl-tp.atlassian.net/wiki/display/NTJP/NTjP+Home).


## Uppbyggnad ##
Testplanen håller fem stycken trådgrupper varav fyra är till för lasttester och en för robusthetstester, se prefix i namnet. Alla dessa är tänkte att gå i sekvens efter varandra. Det finns ytterliga två trådgrupper i testplanen och den ena är Shared Modules där, som namnet säger, det finns delade moduler. Den andra trådgruppen är Archive och den är endast en behållare för att arkivera artifakter som vi inte vill slänga.

I testplanen finns det flera variabler definierade som används när testerna körs. Dessa variabler är:
 * **BASE_URL** - Bas url:en till tjänstern, t.ex _https://qa.esb.ntjp.se/vp_
 * **LOGICAL_ADDRESS** - Logiska adress som skall användas när tjänsterna anropas.
 * **LOADTEST_DURATIONTIME_SEC** - Antal sekunder som lasttesten skall pågå.
 * **ROBUSTNESSTEST_DURATIONTIME_SEC** - Antal sekunder som ribusthetstesten skall pågå.
 * **NO_OF_THREADS** - Antal trådar som skall användas för varje trådgrupp.
 * **RAMP_UP_PERIOD_SEC** - Totalt antal sekunder det skall ta för att starta upp alla trådar i trådgruppen


Det finns en datafil (users.csv) som används för att mata tjänsteanropen med data. Denna filen är en komma separerad fil som håller patientinformation såsom personid och typ av person id.

### Assertions ###
Alla fel som inträffar vid anrop loggas till disk. Det finns en lyssnare "Save Failed Responses to file" som skriver ner alla fallerade svar till ~/logs/FailedResponsesLog_. ~ betyder att filerna skrivs till samma katalog som testplanen finns.

Den finns en assertion vid varje anrop som validera med hjälp av XPath att det inte finns några ProcessingStatusList/statusCode med texten NoDataSynchFailed
 
## Att köra testplanen ##

Då vi använder oss av SSL så måste man själv tala om vilket certifikat som skall användas. Detta gör man genom att välja certifikat _Option > SSL Manager_ (cmd+M). Lösenord anges först när du startar en körning.

Kör testplanen genom att köra följande steg:
 1. Kontrollera att Loop Count i alla trådgrupper har Forever ikryssat. Detta innebär att trådgruppen kommer köras för evigt enligt schemaläggaren (Scheduler) där vi använder Duration för att beskriva hur länge testen skall köras. Vill du endast testa skriptet så är det lämpligt att avmarkera Forever och istället sätta ett värde i count.
 1. Sätt önskade värden för testomgången. Dessa finns under User Defined Variables under Test Plan.
 1. Ta bort alla gamla resultat genom att välja Run > Clear All (cmd+E).



