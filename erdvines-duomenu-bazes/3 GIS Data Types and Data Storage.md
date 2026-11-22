Duomenų struktūrų palyginimas:
- Vektoriniai duomenys gali būti išsaugoti savo originalia rezoliucija.
- Vektorinio žemėlapio kiekvienas taškas turi būti išsaugotas, o rastiniame to nereikia, tad gaunasi greitesnis duomenų rinkimas.
- Vektorinius duomenis gali reikėti konvertuoti į topologinę struktūrą, norint juos nagrinėti. O rastinius duomenis galima atsidaryti as-is
- Vektorinių duomenų algoritmai yra daug sudėtingesni.
- Rastiniai duomenys gali turėti didelę paklaidą, o vektoriniai turi fiksuotą (palydovo) paklaidą

GIS bazėse yra duomenų tipai:
- Erdviniai duomenys - geometrija, X, Y taškai (pagrindinė problema yra saugant šituos duomenis: įvedant, ištrinant ir valdomant. Tam turime hierarchine struktūrą, kur lengva rasti kas kam priklauso. Greita paieška bet duomenų dubliavimas. Galime susikurti indeksą, jei svarbu greita paieška ir nesvarbu dublaivimas)
- Atributiniai duomenys - aprašomi duomenys (saugomi jau žinomose bet kokiose duomenų bazėse. Todėl daugelis GIS leidžia jungtis prie išorinių DB)
	- Nominaliniai (namas, obuolys, pastatas)
	- Ordinaliniai duomenys (pirma, antra trečia klasė, galima rūšiuoti, bet nežinome ką tiksliai leidžia "trečia" klasė)
	- Intervalinis tipas (temperatūra, nes žinomas skirtumas tarp 10 laipsnių ir -10 laipsnių)
	- Santykis

Duomenys gali būti saugomi:
- Tinklinėje duomenų struktūroje (pigesnis, mažiau duplikavimo, bet sunkiau daryti pakeitimus)
- Hierarchinėje duomenų struktūroje (daugiau duplikacijos, bet lengviau suprasti struktūrą)
- Reliacinė duomenų struktūra (duomenys saugomi lentelėje ir kiekviena eilutė turi ID)
- Objektinis modelis (apjungia objektus ir savyje saugo )

Struktūros:
- Arc/Node RDBMS
- Object RDBMS
- CompactRaster RDBMS
- Quadtree RDBMS
	- Leidžia duomenis saugoti periodiškai mažėjančiuose kvadratuose. Galime smulkinti pagal norimą detalumą. Didžiausias tikslumas yra tose vietose, kur kažkas kinta. Saugoma ir optimizuojama atmintis

![[Pasted image 20260916171443.png]]

Sluoksniai griežtai skirstomi pagal tipą: taškiniai arba laužtiniai

![[Pasted image 20260916172333.png]]

![[Pasted image 20260916172914.png]]