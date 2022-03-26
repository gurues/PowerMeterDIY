# MEDIDOR DE PONTENCIA A/C DIY (Power Meter DIY 4 canales)

## ANTECEDENTES

### Tengo un medidor de potencia Shelly EM con una pinza que me mide la entrada general. Quería comprar otro y más pinzas, para poder controlar el consumo de los circuitos de mi casa (lavadora, vitro, luces, etc), pero no había en stock. Así que me decidí a realizar mi propio Shelly EM, Power Meter DIY 4 canales. El precio de 2 Shelly EM y 4 pinzas Shelly sería de 74,66€ y el coste del  Power Meter DIY 4 canales, es de menos de 40€.

## DESCRIPCIÓN DEL PROYECTO

### Para la realización del Power Meter DIY de 4 canales necesitaremos los siguientes componentes:

* 1 x Wemos D1 mini (microcontrolador) ~ 3€
* 2 x ADS1115 (convertidor analógico digital de 16 bits) ~ 10€
* 4 x SCT-013-030 (pinza - sensores de corrientes no invasivos, máxima 30A, relación 30A/1V) ~ 20€
* 1 x HT7333-A o ASM1117 3.3V (regulador de voltaje de bajo consumo) ~ 2€ 10 unidades
* 1 x F.A 5v 600~700 mA (Fuente de alimentación) ~ 3€

### Mediante ESPHome se configuran el dispositivos Power Meter DIY 4, creando las siguientes entidades en Home Assistant:

* Sensor de Potencia Wifi del Power Meter DIY 4. Me da una idea de como es la conexión con la red WIFI del dispositivo
* Sensor de Consumo para cada canal del Power Meter DIY 4. Proporciona una salida en tensión proporcional a la intensidad medida (en nuestro caso 30A/1V antes de calibrarlo), que mediante la programación con ESPHome muestra la salida en amperios de cada canal
* Sensor tensión diferencial entre canales del ADS1115 para cada canal del Power Meter DIY 4. Recibe la señal en voltios proporcionada por las pinzas SCT-013-030. Esta señal puede ser positiva y negativa al medir corriente alterna
* Sensor de tensión de entrada a la casa. Puesto que tengo un Shelly EM que registra el consumo total de la casa, obtengo de este dispositivo la tensión real que llega a mi casa. De esta forma los cálculos de potencia son más precisos. Si no se dispone de la tensión de entrada a la casa se puede poner un valor constante de 230VAC
* Sensor de Potencia para cada canal del Power Meter DIY 4. Cada 15 segundos calculo la potencia instantánea de cada canal del dispositivo, mediante multiplicación de los valores de los sensores de consumo y tensión de entrada

### Toda la información necesaria para realizar este proyecto se comparte en este repositorio y la puedes encontrar organizada en las siguiente carpetas o archivos:

* Archivo power.diy-4.yaml. Aquí tienes la configuración ESPHome del Power Meter DIY 4. Aquí puedes modificar el nombre del dispositivo, la ip fija, ajuste de calibración y los parámetros de programación de ESPHome
* Archivo secrets.yaml. Aquí tienes que configurar tus datos WIFI, etc
* Carpeta Ayuda_Montaje. En esta carpeta tienes fotos del dispositivo y un esquema de montaje de un canal. También están en la carpeta 3D, los STL's para la instalación del Power Meter DIY 4 en carril DIN (es posible que tengas que ajustarlos un poco .... yo le tuve que pasar la lima)

## CALIBRACIÓN DE LAS PINZAS AMPERIMÉTRICAS

### Seguí las instrucciones que hay en ESPHome, `https://esphome.io/components/sensor/ct_clamp.html`. Calibré cada pinza con un consumo constate de 10A (radiador eléctrico de aceite) y ajuste el parámetro "calibrate_linear" para obtener ese valor en la pinza amperimétrica. Posteriormente instale mi Power Meter DIY 4 en mi cuadro eléctrico y contraste sus valores con una pinza amperimétrica Fluke calibrada. Los resultados obtenidos son sorprendentemente precisos.

## ENLACES Y AGRADECIMIENTOS

### Este proyecto surgió ante la falta de stock de Shelly. Un millón de gracias a Shelly por no dar a basto a sus cliente,"Power Meter DIY 4 canales"

* `https://www.luisllamas.es/arduino-sensor-corriente-sct-013/`
* `https://www.luisllamas.es/entrada-analogica-adc-de-16-bits-con-arduino-y-ads1115/`
* `https://forum.jeedom.com/viewtopic.php?t=41112#p671120`
* `https://esphome.io/`
* `https://esphome.io/components/sensor/ct_clamp.html`
* `https://www.thingiverse.com/thing:4625751`

* Un Loco y su Tecnología, `https://www.youtube.com/channel/UC2zp7AWsYhZaGmYTjP8hZ7A`. Por su magnífico canal de Youtube donde comparte todos sus conocimientos

* `https://www.luisllamas.es/`. El mejor bloc para aprender a cacharrear con Arduino, ESP8266, ESP32 y mucho más

## Realizado por gurues (gurues@3DO ~ 2022 ~ ogurues@gmail.com)

