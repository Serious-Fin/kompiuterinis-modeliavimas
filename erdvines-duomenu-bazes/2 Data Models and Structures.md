How it looks like - Model
How it works - Process (kaip keičiasi vandens lygis užliejus kažkokį plotą)

Which is more important? Knowledge about the process is more important as it can be used for prediction.

Pagrindinės problemos atvaizduojant realų pasaulį:
- Begalinis sudėtingumas
- Nedeterministiškas
- Kokias detales išimti, o kokias palikti
- Galima atvaizduoti tik dalinai (frakcinis atvaizdavimas)

Model types:
- Field - koks yra vandens lygis virš jūros lygio? Kur virš vandens lygio, ten traktuojam kaip žemę, o kitus - kaip jūrą.
- Object - vienas objektas žemė, o kitas - jūra.

Žemėlapio tipai:
- Rastinis žemėlapis - turime tinklelį, kur kiekviena eilutė suskirstyta į stulpelius. Kiekvienam langeliui priskiriame tam tikrą vertę.
- Vektorinis žemėlapis - sudarytas iš kryptingų vektorių. Viena iš užduočių yra apskaičiuoti, ar pelytės spustelėjimas yra formos viduje, ar išorėje.
	- Vektorinius duomenis galima papildyti topologija - tokia struktūra, kuri parodo sąryšį tarp gretimų objektų

Užduotis:
- Susirasti kokie žemėlapiai yra prieinami, kokie duomenis renkami ir kokie duomenys gaunami
Kokių GIS primityvų reikia, norint ją sukurti (mastelio keitimas, žemėlapio stumdymas, slėpimas pagal mastelį, nuspalvinimas pagal tematiką)
KOkiu duomenų reikėtų, norint tokią sistemą nuklonuoti. Pavyzdžiui, pastatų žemėlapių ir jų energetinių klasių, pastatų koordinačių.
Kokią uzduoti reiketu paduoti programuotojams, norint ta zemelapi sukurti (marsrutizavimo algoritmas, grafo algoritmas). Jei reiketu sukurti nuo nulio, kokiu primityvo reiketu. Parodyti ar paslepti sluosni. Paskui dar kokiu duomenu reikia, kokiu sluoksniu reikia, is kur gatviu pavadinimai atsiranda. Paziureti daugiau is valstybiniu zemelapiu 

Primityvas (turime ekrano X, Y koordinate, sukonvertuoja i ilguma ir platuma ir is duomenu bazes turime primityva, kur istraukiame, kas yra konkreciame taske, gal dar vienas parametras sluoksnis)
Sluoksnio ijungimas isjungimas
Zemelapio zoominimas ir judinimas (pagal ekrano X, Y koordinates gauname informacija tam tikroje ilgumoje platumoje)

Pagal X ir Y surandame objeta, o kitas primityvs - atsiuncia zemelapi, kur objetkas nupaisytas kita spalva

Pagal gatves atributini duomeni surandame gatves ID, paskui pagal ID surandame

Norime, kad parodytu objeta per visa ekrana - scale zemelapi pagal ekrano X, Y duomenis

Primityvas - istraukti duomenis pagal geometrijos ID

Atviras vilnius, vilniaus savivaldybe, gal zemelapio atsisiuntimo funkcija

Pabandyti paziureti su kokia sistema ar biblioteka sukurta

Uzsirasyti i ekseli varda, pavarde ir zemelapi