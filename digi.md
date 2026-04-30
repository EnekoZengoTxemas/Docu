---
layout: page
title: Digi
---

Datuen balioa eta monitorizazioa
Guretzat, datuak uraren kalitatea bezain esentzialak dira. Langileen erosotasuna eta ongizatea bermatzeko, ingurune-baldintzak (tenperatura eta hezetasuna) etengabe neurtzen ditugu, instalazioetan segurtasun eta erosotasun maila optimoak mantentzeko.

Konfidentzialtasuna: Informazio hau barne-erabilerarako besterik ez da. Egoitza bakoitzeko langileek soilik daukate sarbidea, lan-inguruneko parametro espezifikoak direla ziurtatuz eta kanpoko esku-hartzeetatik babestuz.

Osotasuna: Gure sentsoreek jasotako datuak bakarrak, zehatzak eta fidagarriak dira. Horrela, langileek ez dute datuen zuzentasunaz kezkatu behar; informazioa gardena eta errorerik gabea da.

Erabilgarritasuna: Datuak une errealean eskuragarri daude. Horri esker, edozein unetan har daitezke neurri zuzentzaileak hezetasuna edo tenperatura doitzeko, uraren tratamendurako beharrezkoa den doitasun bera aplikatuz gure bulegoetan.

Ekipoen babes teknologikoa
Ura arazteko prozesuetan doitasuna behar dugun bezala, gure hardwarean ere segurtasun zorrotza aplikatzen dugu. Gailu bakoitzak babes-neurri espezifikoak ditu: erabiltzaile bakoitzak bere funtzioetarako beharrezkoak diren baimenak soilik ditu, faktore bikoitzeko autentifikazioa (2FA) erabiltzen dugu eta informazio sentikor guztia enkriptatuta dago.

Sare-arkitektura eta segurtasun globala
Gure sarearen diseinua isolamendu-geruzetan oinarritzen da, filtrazioak ekiditeko. Firewall indartsu baten bidez kanpoko mehatxuak blokeatzen ditugu, eta sarea VLAN desberdinetan segmentatu dugu; horrela, balizko eraso bat gertatuz gero, kutsadura isolatu egiten da (ur-zirkuitu estankoetan bezala), sare osora zabaldu ez dadin. Sistema honek sarbide ororen kontrol erabatekoa bermatzen digu.

Araudia eta babeskopia-plana (Resilience)
Gure konpromisoa erabatekoa da:

Lege-betetzea: Gure sistema guztiek DBEO (RGPD) araudia zorrotz betetzen dute, erabiltzaileen pribatutasuna babestuz.

Datuen babesa (3-2-1 Metodoa): Informazioaren jarraitutasuna ziurtatzeko, hiru kopia gordetzen ditugu euskarri desberdinetan: zerbitzarian, disko fisiko batean eta hodeian.

Ondorioa: Edozein ezustekoren aurrean, gure datuak berreskuratzeko gaitasuna (erresilientzia) erabatekoa da, gure zerbitzuak etenik izan ez dezan.

# Cluster
## Sortuta

MondgoDB Atlas ean erregistratu gara eta cluster bat sortu dugu. 

<img width="2553" height="1179" alt="image" src="https://github.com/user-attachments/assets/5b70138b-9bf2-4516-8433-53f21b459363" />

---

  Gero databasea eta kolekzioa sortu ditugu eta MongoDB-ean erabilitako json-a importatu dugu.

<img width="2501" height="1254" alt="image" src="https://github.com/user-attachments/assets/82f0fc53-8ea6-47aa-9f3c-60d8e796cd87" />



## Ip WhiteList
Soilik gure ip-ak sartzeko cluster-ean ipini ditugu.

<img width="2558" height="1339" alt="image" src="https://github.com/user-attachments/assets/bf3d5cf0-b65d-4f3f-b34a-88e9fbea808a" />


---


## Adimen Artifiziala

Azkenik Adimen Artifiziala gehitu diogu query-ak egiteko.

<img width="2490" height="1105" alt="image" src="https://github.com/user-attachments/assets/d79d65b1-0e4f-4d1a-9e27-308f6d4393cd" />



# Grafikoa


![](images/image.png)

