---
layout: page
title: Markatze Lengoaiak
---

# Javascript

## script.js

Hasteko javascript fitxategia aldatzen hasi ginen. Gure helburua zen xml batetik datuak dinamikoki jasotzea. Orduan hasierako var hauek guztiz kendu genituen eta hau gehitu genuen.

```javascript
 $.ajax({
        url: 'data/1waterplant2026.xml',
        dataType: 'xml',
        success: function (xml) {
            UrPlantaDatuak = [];

            $(xml).find('data').each(function () {
                var site     = $(this).find('site_id').text().trim();
                var sensor   = $(this).find('sensor_id').text().trim();
                var timestamp = $(this).find('rango_horario').text().trim();
                var flowAvg  = parseFloat($(this).find('flow_avg').text().trim());
                var flowMin  = parseFloat($(this).find('flow_min').text().trim());
                var flowMax  = parseFloat($(this).find('flow_max').text().trim());
                var phAvg    = parseFloat($(this).find('ph_avg').text().trim());
                var phMin    = parseFloat($(this).find('ph_min').text().trim());
                var phMax    = parseFloat($(this).find('ph_max').text().trim());
                var pressAvg = parseFloat($(this).find('pressure_avg').text().trim());
                var pressMin = parseFloat($(this).find('pressure_min').text().trim());
                var pressMax = parseFloat($(this).find('pressure_max').text().trim());

                if (!site || !timestamp || isNaN(flowAvg) || isNaN(phAvg) || isNaN(pressAvg)) return;

                UrPlantaDatuak.push({
                    timestamp: timestamp,
                    location:  site,
                    sensorId:  sensor,
                    flowAvg:   flowAvg,
                    flowMin:   isNaN(flowMin) ? flowAvg : flowMin,
                    flowMax:   isNaN(flowMax) ? flowAvg : flowMax,
                    phAvg:     phAvg,
                    phMin:     isNaN(phMin) ? phAvg : phMin,
                    phMax:     isNaN(phMax) ? phAvg : phMax,
                    pressAvg:  pressAvg,
                    pressMin:  isNaN(pressMin) ? pressAvg : pressMin,
                    pressMax:  isNaN(pressMax) ? pressAvg : pressMax
                });
            });


```

Kode hau xml-tik ajax erabiliz datuak dinamikoki jasotzen ditu. Datu horiek array batzuetan gordetzeko kode hau erabili dut. For erabili beharrean .each erabili dut, hau da, erregistro bakoitzean UrPlantaDatuak array-a timestamp, site, sensor... gordeko ditu.

---

Gero Kontrol-Panelean filtratzeko kode hau erabili dugu:

```javascript
            var egunak = [];
            for (var j = 0; j < UrPlantaDatuak.length; j++) {
                var eguna = UrPlantaDatuak[j].timestamp.split(' ')[0];
                if (egunak.indexOf(eguna) === -1) egunak.push(eguna);
            }
            egunak.sort();
            $('#eguna-select').empty();
            for (var k = 0; k < egunak.length; k++) {
                $('#eguna-select').append('<option value="' + egunak[k] + '">' + egunak[k] + '</option>');
            }

            var lekuak = [];
            for (var l = 0; l < UrPlantaDatuak.length; l++) {
                var lekua = UrPlantaDatuak[l].location;
                if (lekuak.indexOf(lekua) === -1) lekuak.push(lekua);
            }
            lekuak.sort();
            $('#lekua-select').empty();
            for (var m = 0; m < lekuak.length; m++) {
                $('#lekua-select').append('<option value="' + lekuak[m] + '">' + lekuak[m] + '</option>');
            }

            $('#bistaratu-btn').prop('disabled', false).text('Bistaratu');
        }
```

Kode hau for batekin datuak dituzten egunak array batean gordetzen ditu eta gero aukera bezala erakusten ditu. Lekuekin berdina egiten du.

---





