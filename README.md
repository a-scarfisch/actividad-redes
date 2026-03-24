# actividad-redes
actividad bootcamp lunes 23 de marzo
# 🌐 Fase 1: Investigación - Dispositivos de Red

Este documento contiene la base teórica sobre los dispositivos fundamentales de infraestructura de red, diseñada para estudiantes de desarrollo que necesitan entender cómo viajan sus datos.

---

## 🧩 1. ¿Qué es cada dispositivo?

| Concepto | Definición simple | Nivel técnico (breve) | Ejemplo real |
| :--- | :--- | :--- | :--- |
| **Router** | El "director de tráfico" que conecta tu casa con el mundo exterior (Internet). | Gestiona la capa 3 del modelo OSI utilizando direcciones **IP** para mover paquetes entre distintas redes. | El aparato que instala la compañía de internet para darte Wi-Fi. |
| **Switch** | El "organizador" que permite que varios equipos en un mismo lugar se hablen entre sí. | Opera en la capa 2, usando direcciones **MAC** para enviar datos exclusivamente al destinatario correcto. | El dispositivo que conecta todas las computadoras en un laboratorio de computación. |
| **Hub** | Un conector antiguo que repite lo que recibe a todos los que estén conectados. | Dispositivo de capa 1 que reenvía datos por **Broadcast** (difusión a todos), causando colisiones. | Una "zapatilla" eléctrica, pero de datos: lo que entra por un puerto sale por todos los demás. |

---

## ⚙️ 2. ¿Cómo funciona realmente?

* **¿Qué hace el router con los paquetes de datos?**
    Actúa como un guía. Recibe un paquete, lee la dirección **IP** de destino y decide, según sus tablas de rutas, cuál es el mejor camino para enviarlo fuera de tu red local hacia el servidor correcto.
* **¿Cómo decide un switch a dónde enviar la información?**
    Mira la dirección **MAC** (identificador físico único). El switch aprende en qué puerto físico está conectada cada MAC y envía el mensaje directo a ese cable, evitando molestar a los demás.
* **¿Por qué el hub es considerado obsoleto?**
    Porque es ineficiente y ruidoso. Al usar **Broadcast** para todo, satura la red con tráfico innecesario y permite que cualquier dispositivo conectado "escuche" datos que no le corresponden.

---

## 💻 3. Conexión directa con desarrollo (CLAVE)

* **Rol del router en un `fetch()` a una API:**
    Cuando ejecutas `fetch("https://api.miapp.com")`, el router es quien recibe la solicitud y se encarga de que tus datos salgan de tu red local para encontrar la ruta hacia el servidor donde vive la API.
* **Importancia del switch en un backend o data center:**
    Permite que tu servidor de aplicación y tu base de datos se comuniquen a velocidades altísimas con latencia mínima, asegurando que el backend reciba la información casi instantáneamente.
* **Problemas de red que afectan tu app (código "correcto"):**
    Si hay una saturación en el router o pérdida de paquetes, el usuario verá errores de conexión o *Timeouts*. El código está bien, pero el "puente" de comunicación está roto.

---

## 🌍 4. Caso práctico real: "App caída en producción"

* **¿Podría ser problema de router?**
    **Sí.** Si las tablas de enrutamiento fallan, el tráfico de los usuarios nunca llegará al servidor. La app está viva, pero es inaccesible.
* **¿Podría ser problema de switch?**
    **Sí.** Si falla el switch que une tu servidor con la base de datos, tu app no podrá consultar información y se quedará "colgada".
* **¿Cómo distinguir si es red o código?**
    Si un `ping` al servidor responde pero la app devuelve un error `500`, suele ser **código**. Si no hay respuesta al `ping` o el comando `traceroute` se corta a mitad de camino, es un problema de **red**.

---

## 🧪 5. Analogías para entender de verdad

* **Router** = Oficina de correos entre ciudades (mueve paquetes entre grandes distancias).
* **Switch** = Conserje de un edificio (sabe exactamente en qué departamento entregar la carta).
* **Hub** = Persona que grita el mensaje a todos en la plaza (todos escuchan, aunque no sea para ellos).

---

**TL;DR:** El **Router** nos conecta a Internet (IP), el **Switch** organiza la comunicación interna eficiente (MAC) y el **Hub** es una reliquia ineficiente que enviaba todo a todos por broadcast.
