# Configuración de Servidor DHCP en Linux

## :spades: Descripción

En este ejercicio configuraremos mediante vagrant un servidor DHCP en un entorno Linux, junto con dos clientes que obtendrán su configuración de red de forma automática. El cliente `c2` se configurará para recibir una dirección IP específica basada en su dirección MAC.

## :hearts: Requisitos

- Una máquina virtual (MV) Linux configurada como servidor DHCP.
- Dos máquinas virtuales (MV) Linux configuradas como clientes DHCP (`c1` y `c2`).
- Acceso a Internet para la descarga de paquetes necesarios.

## :clubs: Configuración del Servidor DHCP

1. **Instalación del Servicio DHCP**
   - Asegúrate de que el servicio DHCP no esté instalado en el equipo.
   - Instala el servicio DHCP utilizando el gestor de paquetes de tu distribución.

2. **Configuración de Interfaces de Red**
   - Configura dos tarjetas de red en la máquina virtual del servidor:
     - **Tarjeta 1**: Red privada solo-anfitrión `192.168.56.0/24` con IP `192.168.56.10`.
     - **Tarjeta 2**: Red interna `192.168.57.0/24` con IP `192.168.57.10`.

3. **Verificación de Configuración de Red**
   - Utiliza el comando `ip a` para verificar que la configuración de red de las interfaces es correcta.

4. **Configuración del Archivo DHCP**
   - Realiza una copia de seguridad del archivo de configuración del servicio DHCP:
     ```bash
     cp /etc/dhcp/dhcpd.conf /etc/dhcp/dhcpd.conf.bak
     ```
   - Modifica el archivo de configuración para definir las subredes y las opciones DHCP:
     - Rango de direcciones IP: `192.168.57.25` a `192.168.57.50`.
     - Tiempo de concesión por defecto: 1 día, máximo: 8 días.
     - Dirección de difusión: `192.168.57.255`.
     - Puerta de enlace: `192.168.57.10`.
     - Servidores DNS: `8.8.8.8` y `4.4.4.4`.
     - Nombre de dominio: `micasa.es`.

5. **Reinicio del Servicio DHCP**
   - Reinicia el servicio DHCP y verifica que no haya errores.

## :diamonds: Configuración de Clientes DHCP

1. **Configuración de `c1`**
   - Configura la máquina virtual `c1` en modo red interna y asegúrate de que esté en la misma red interna que el servidor DHCP.
   - Configura su interfaz como cliente DHCP y reinicia la interfaz de red.

2. **Configuración de `c2`**
   - Añade la configuración necesaria en el servidor DHCP para que `c2` obtenga siempre la IP `192.168.57.4` mediante MAC, puedes utilizar la MAC `5CA1AB1E0001`, con un tiempo de concesión de 1 hora y servidor DNS `1.1.1.1`.

## :black_joker: Ejecución

Para ejecutar el ejercicio, sigue los pasos de configuración mencionados anteriormente y asegúrate de que todos los servicios estén funcionando correctamente. Puedes verificar la asignación de direcciones IP en los clientes utilizando el comando `ip a`.
