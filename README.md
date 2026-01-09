# Pruebas en modo activo y pasivo


![](https://raw.githubusercontent.com/JosecarlosGlr/PruebasEnModoActivoYPasivo/refs/heads/main/1.png)

Lo primero que hago es configurar el rango de los puertos pasivos

![](https://raw.githubusercontent.com/JosecarlosGlr/PruebasEnModoActivoYPasivo/refs/heads/main/2.png)
![](https://raw.githubusercontent.com/JosecarlosGlr/PruebasEnModoActivoYPasivo/refs/heads/main/3.png)

Aqui voy a realizar una conexión al servidor nuevamente con anonymous pero forzando entrar de modo activo

![](https://raw.githubusercontent.com/JosecarlosGlr/PruebasEnModoActivoYPasivo/refs/heads/main/4.png)  
Ya tengo la conexión activa hecha

![](https://raw.githubusercontent.com/JosecarlosGlr/PruebasEnModoActivoYPasivo/refs/heads/main/5.png)
![](https://raw.githubusercontent.com/JosecarlosGlr/PruebasEnModoActivoYPasivo/refs/heads/main/6.png)

vuelvo a realizar una conexión al servidor nuevamente con anonymous pero forzando entrar de modo pasivo

![](https://raw.githubusercontent.com/JosecarlosGlr/PruebasEnModoActivoYPasivo/refs/heads/main/7.png)  

Ya tengo la conexión pasiva hecha, además filezilla client me ha permitido trabajar con ambos a la vez porque te da la opción de abrir la nueva conexión en otra ventana

### Análisis: ¿Qué modo funciona mejor en redes con Firewall?

Yo realmente no he notado diferencia entre realizar la conexión en modo pasivo o activo, pero según me he informado el **Modo Pasivo** es el que funciona mejor en la mayoría de las redes actuales.

**¿Por qué?**
Hoy en día, casi todos los usuarios están detrás de un router (**NAT**) o un firewall personal (como Windows Defender) que bloquea las conexiones que vienen "de fuera" sin previo aviso.

* **En el modo Activo:** El servidor intenta "llamar" al cliente, pero el firewall del cliente suele bloquear esta conexión entrante ("le cuelga la llamada").
* **En el modo Pasivo:** Es el **cliente** quien inicia la conexión hacia el servidor. Como los firewalls suelen permitir todo el tráfico de salida por defecto, la conexión se establece sin problemas.

| Característica | Modo Activo | Modo Pasivo |
| :--- | :--- | :--- |
| **Quién inicia la conexión de datos** | El **Servidor** se conecta al Cliente. | El **Cliente** se conecta al Servidor. |
| **Comportamiento con Firewall (Cliente)** | Suele fallar. El firewall del cliente bloquea la conexión entrante del servidor. | **Funciona bien.** El firewall suele permitir la salida del cliente hacia el servidor. |
| **Configuración necesaria** | Requiere abrir puertos en el lado del cliente (algo difícil de gestionar). | Requiere abrir un rango de puertos en el lado del servidor (lo que hicimos con el 50000-50100). |
| **Uso recomendado** | Redes internas muy controladas o antiguas. | **Internet y redes modernas (NAT).** Es el estándar actual. |
