loadtest-aggregators
====================

Detta projekt är ett [jmeter](http://jmeter.apache.org/) projekt som används för att last- och robusthetstesta agregerande tjänster i den [nationella tjänsteplattformen (NTjP)](https://skl-tp.atlassian.net/wiki/display/NTJP/NTjP+Home).

Testplanen håller fem stycken trådgrupper varav fyra är till för lasttester och en för robusthetstester, se prefix i namnet. Alla dessa är tänkte att gå i sekvens efter varandra. Det finns ytterliga två trådgrupper i testplanen och den ena är Shared Modules där, som namnet säger, det finns delade moduler. Den andra trådgruppen är Archive och den är endast en behållare för att arkivera artifakter som vi inte vill slänga.

I testplanen finns det flera variabler definierade som används när testerna körs. Dessa variabler är:
* **BASE_URL** - Bas url:en till tjänstern, t.ex _https://qa.esb.ntjp.se/vp_
* **LOGICAL_ADDRESS** - Logiska adress som skall användas när tjänsterna anropas.
* **LOADTEST_DURATIONTIME_SEC** - Antal sekunder som lasttesten skall pågå.
* **ROBUSTNESSTEST_DURATIONTIME_SEC** - Antal sekunder som ribusthetstesten skall pågå.
* **NO_OF_THREADS** - Antal trådar som skall användas för alla trådgrupper.

 



