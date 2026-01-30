# Pruebas en modo activo y pasivo

![](https://raw.githubusercontent.com/JosecarlosGlr/PruebasEnModoActivoYPasivo/refs/heads/main/1.png)

Lo primero que hago es configurar el rango de los puertos pasivos en el servidor. He definido un rango personalizado que va desde el puerto **50000** hasta el **50100** para gestionar las conexiones de datos entrantes.

![](https://raw.githubusercontent.com/JosecarlosGlr/PruebasEnModoActivoYPasivo/refs/heads/main/2.png)
![](https://raw.githubusercontent.com/JosecarlosGlr/PruebasEnModoActivoYPasivo/refs/heads/main/3.png)

Para realizar la primera prueba, configuro el cliente FileZilla forzando el modo de transferencia en **Activo**. Utilizo el usuario `anonymous` y me aseguro de que el protocolo esté configurado como FTP sobre TLS.

![](https://raw.githubusercontent.com/JosecarlosGlr/PruebasEnModoActivoYPasivo/refs/heads/main/4.png)  

Como se observa en el log del cliente, la conexión en **modo activo** se ha establecido correctamente, permitiendo el listado del directorio tras el intercambio de certificados TLS.

![](https://raw.githubusercontent.com/JosecarlosGlr/PruebasEnModoActivoYPasivo/refs/heads/main/5.png)
![](https://raw.githubusercontent.com/JosecarlosGlr/PruebasEnModoActivoYPasivo/refs/heads/main/6.png)

A continuación, repito el proceso pero forzando el modo de transferencia en **Pasivo**. En esta configuración, el cliente solicitará al servidor que abra un puerto dentro del rango (50000-50100) que definimos anteriormente.

![](https://raw.githubusercontent.com/JosecarlosGlr/PruebasEnModoActivoYPasivo/refs/heads/main/7.png)  

La conexión en **modo pasivo** también funciona con éxito. FileZilla Client me ha permitido mantener ambas sesiones abiertas simultáneamente en pestañas separadas, facilitando la comparativa técnica entre ambos métodos.

---

### Análisis: ¿Qué modo funciona mejor en redes con Firewall?

En este entorno de pruebas local ambos han funcionado, pero en un entorno real el **Modo Pasivo** es el estándar más fiable.

**¿Por qué?**
La mayoría de redes actuales utilizan **NAT** y firewalls que bloquean por defecto cualquier conexión iniciada desde el exterior.

* **Modo Activo:** El servidor intenta iniciar la conexión de datos hacia el cliente. El firewall del cliente suele interpretar esto como una intrusión y bloquea la conexión.
* **Modo Pasivo:** El cliente inicia tanto el canal de control como el de datos. Como los firewalls permiten el tráfico de salida por defecto, la conexión suele establecerse sin necesidad de configurar el router del cliente.

| Característica | Modo Activo | Modo Pasivo |
| :--- | :--- | :--- |
| **Inicio de datos** | El Servidor conecta al Cliente. | El Cliente conecta al Servidor. |
| **Firewall (Cliente)** | Suele fallar al bloquear la entrada. | **Funciona correctamente** (tráfico de salida). |
| **Configuración** | Requiere abrir puertos en el cliente. | Requiere abrir un rango en el servidor (50000-50100). |
| **Uso actual** | Redes locales o antiguas. | **Estándar en Internet y NAT.** |
