Kas yra GIS? 
GIS:
- Duomenų konteineris, kuriame saugomi geografiniai (duomenys, susiję su X, Y ir Z koordinatėmis) ir atributiniai duomenys;
- Žemėlapių konteineris, kuriame yra ištraukiama labai maža dalis specializuotų duomenų (pavyzdžiui, geoterminiai duomenys, keliai, upės), norint juos atvaizduoti. Esmė, kad duomenų yra labai daug ir ištraukti specifinius žemėlapio duomenis yra sunku;
- Įrankiai - algoritmai skirti išspręsti erdvines užklausas, pavyzdžiui, pasirinkti objektus, kurie yra naudotojo matomame ekrane. Arba surasti arčiausiai esantį "Bolt" vairuotoją. Gali būti kelis skirtingi algoritmai: surasti trumpiausią kelią pagal laiką arba pagal atstumą;
- Sprendimų priėmimo sistemos - turint duomenis galima planuotis rizikas: kokios zonos bus užliejamos trūkus vamzdžiui, ar kokios vietos yra pavojaus zonoje, esant nuošliaužoms (tam reikia reljefo duomenų, kurie gaunami lazeriniais įrankiais);
- Erdvės analizė - kur statyti parduotuvę (žiūrint pagal gyvenamųjų namų skaičių), kur tiesti vandentiekį (žiūrint pagal žemės kietumą), t.t.

GIS naudojamas:
- Realaus laiko sistemos -  Lėktuvų, mašinų žemėlapiai
- Predictive modeling - simuliuoja ateities scenarijus (klimato anomalijų rizika)
- Citizen engagement tools - paslaugų radimo servisai (kavinės, parduotuvės)
- Augmented reality and 3D visualization - erdviniai duomenys naudojami interaktyviam planavimui
- Field data collection system - statybų aikštelės skenavimas dronais;
- Storytelling medium - komunikuoja erdvės kitimą per interaktyvius kitimo žemėlapius (muziejai, kur rodomas reljefo kitimas). Balsavimo duomenys, savivaldybės balsavimo aktyvumas;

Sudėtingiausias uždavinys - duomenų gavimas. Norint ypač tikslių duomenų juos gali tekti pirkti iš Google.

Kursas siesis su erdvės saugojimą duomenų bazėje. Koks duomenų tipas naudojamas, kaip tuos duomenis skaityti, ieškoti, indeksuoti, t.t.

Pratybos vyks per Teams. Bus sudaryta virtuali eilė ir iš eilės kiekvienam dėstytojas skambins.

Programos:
- GUI - Quantum-GIS
- DB - PostGRE/PostGIS

GIS (Graphical Information System):
- Hardware - įrankiai, kuriuos naudoja kartografai matuodami/filmuodami žemę;
- Software - programinė įranga ir algoritmai, kurie suvienodina duomenis, pavyzdžiui, išima žemės paviršiaus išsigaubimą ir pateikia duomenis normalioje skalėje;
- Network - terpė, per kurį surinkti duomenys yra perduodami;
- Data - surinkti duomenys, kurie tam tikru formatu saugomi kompiuteryje;
- People - darbuotojai (kartografai, statybininkai, architektai);
- Procedures - duomenų analizė, statistika, tvarkymas;

Viena didžiausių problemų yra žemėlapio saugojimas, nes jis užima labai daug vietos

Egzaminas bus iš paskaitų medžiagos: principai, medžiaga, teorija. Bus daug trumpų klausimų, kuriuos reikės atsakyti

Geo-Database (Geo duomenų bazė) - sudaro sluoksniai, pavyzdžiui, pastatai, gatvės, medžiai. Visi duomenys saugomi ne vienoje visumoje, o tiesiog vienas ant kito atvaizduojami sluoksniai.

Main Questions to GIS:
1. a
2. Where is the place matching given conditions?
	- Purpose: Locate areas that meet specific criteria.
	- Examples: where does the soil density match specific requirements?
3. What has changed in given location during some given time duration?
	- Purpose: Detect and analyze temporal changes.
	- Examples; how has the urban area changes over the past decade?
4. What are the spatial patterns?
5. What would happen is some condition satisfied some given criteria in a location?