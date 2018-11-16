---
title: Solución de problemas de SQL Server en Linux | Microsoft Docs
description: Proporciona sugerencias para solucionar problemas para usar SQL Server en Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 05/01/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.assetid: 99636ee8-2ba6-4316-88e0-121988eebcf9S
ms.openlocfilehash: 4bd04ee62af21255f40363de602c6461aeb350a6
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51677924"
---
# <a name="troubleshoot-sql-server-on-linux"></a>Solución de problemas de SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Este documento describe cómo solucionar problemas de Microsoft SQL Server que se ejecutan en Linux o en un contenedor de Docker. Al solucionar problemas de SQL Server en Linux, no olvide revisar las características admitidas y las limitaciones conocidas en el [SQL Server en Linux Release Notes](sql-server-linux-release-notes.md).

> [!TIP]
> Para obtener respuestas a las preguntas más frecuentes, consulte el [SQL Server en Linux preguntas más frecuentes sobre](sql-server-linux-faq.md).

## <a id="connection"></a> Solución de problemas de errores de conexión
Si tiene dificultades para conectarse a Linux SQL Server, hay algunos aspectos que debe comprobar. 

- Compruebe que el nombre del servidor o dirección IP sea accesible desde el equipo cliente.

   > [!TIP]
   > Para buscar la dirección IP de la máquina Ubuntu, puede ejecutar el comando ifconfig en el ejemplo siguiente:
   >
   >   ```bash
   >   sudo ifconfig eth0 | grep 'inet addr'
   >   ```
   > Para Red Hat, puede usar la dirección ip en el ejemplo siguiente:
   >
   >   ```bash
   >   sudo ip addr show eth0 | grep "inet"
   >   ```
   > Una excepción a esta técnica se relaciona con máquinas virtuales de Azure. Las máquinas virtuales de Azure, [encontrar la dirección IP pública para la máquina virtual en Azure portal](https://docs.microsoft.com/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine#connect).

- Si procede, compruebe que ha abierto el puerto de SQL Server (predeterminado: 1433) en el firewall.

- Las máquinas virtuales de Azure, compruebe que tiene un [regla de grupo de seguridad de red para el puerto de SQL Server predeterminado](https://docs.microsoft.com/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine#remote).

- Compruebe que el nombre de usuario y la contraseña no contienen errores tipográficos o espacios en blanco adicionales o incorrectos mayúsculas y minúsculas.

- Intente establecer explícitamente el número de puerto y protocolo con el nombre del servidor como en el ejemplo siguiente: **tcp:servername, 1433**.

- Problemas de conectividad de red también pueden provocar tiempos de espera y errores de conexión. Después de comprobar la información de conexión y la conectividad de red, intente conectarse de nuevo.

## <a name="manage-the-sql-server-service"></a>Administrar el servicio de SQL Server

Las secciones siguientes muestran cómo iniciar, detener, reiniciar y comprobar el estado del servicio SQL Server. 

### <a name="manage-the-mssql-server-service-in-red-hat-enterprise-linux-rhel-and-ubuntu"></a>Administrar el servicio mssql-server en Red Hat Enterprise Linux (RHEL) y Ubuntu 

Compruebe el estado del servicio SQL Server mediante este comando:

   ```bash
   sudo systemctl status mssql-server
   ```

Puede detener, iniciar o reiniciar el servicio SQL Server según sea necesario mediante los siguientes comandos:

   ```bash
   sudo systemctl stop mssql-server
   sudo systemctl start mssql-server
   sudo systemctl restart mssql-server
   ```

### <a name="manage-the-execution-of-the-mssql-docker-container"></a>Administrar la ejecución del contenedor de Docker mssql

Puede obtener el identificador de estado y el contenedor del contenedor de Docker de SQL Server más reciente creado, ejecute el comando siguiente (el identificador está bajo el **Id. de contenedor** columna):

   ```bash
   sudo docker ps -l
   ```
   
Puede detener o reiniciar el servicio SQL Server según sea necesario mediante los siguientes comandos:
   
   ```bash
   sudo docker stop <container ID>
   sudo docker restart <container ID>
   ```

> [!TIP]
> Para obtener más sugerencias sobre solución de problemas para Docker, consulte [contenedores de Docker de solución de problemas de SQL Server](sql-server-linux-configure-docker.md#troubleshooting).

## <a name="access-the-log-files"></a>Obtener acceso a los archivos de registro
   
Los registros del motor de SQL Server en el archivo /var/opt/mssql/log/errorlog en las instalaciones de Linux y Docker. Debe estar en modo de "superusuario" para buscar este directorio.

El programa de instalación registra aquí: / var/opt/mssql/setup-< marca de tiempo que representa la hora de instalación >, puede examinar los archivos de registro de errores con cualquier herramienta compatible con UTF-16 como 'vim' o 'cat' como este: 

   ```bash
   sudo cat errorlog
   ```

Si lo prefiere, también puede convertir los archivos en UTF-8 para leerlos con 'más' o 'menos' con el siguiente comando:
   
   ```bash
   sudo iconv –f UTF-16LE –t UTF-8 <errorlog> -o <output errorlog file>
   ```
## <a name="extended-events"></a>Eventos extendidos

Eventos extendidos se pueden consultar a través de un comando SQL.  Puede encontrar más información sobre los eventos extendidos [aquí](https://technet.microsoft.com/library/bb630282.aspx):

## <a name="crash-dumps"></a>Los volcados de memoria 

Busque los volcados de memoria en el directorio de registro en Linux. Compruebe en el directorio /var/opt/mssql/log para volcados de memoria de núcleo de Linux (. extensión tar.gz2) o SQL minivolcados (extensión .mdmp)

Para los volcados del núcleo 
   ```bash
   sudo ls /var/opt/mssql/log | grep .tar.gz2 
   ```

For SQL dumps 
   ```bash
   sudo ls /var/opt/mssql/log | grep .mdmp 
   ```
   
## <a name="start-sql-server-in-minimal-configuration-or-in-single-user-mode"></a>Iniciar SQL Server en una configuración mínima o en modo de usuario único

### <a name="start-sql-server-in-minimal-configuration-mode"></a>Iniciar SQL Server en modo de configuración mínima
Esta opción resulta útil si el valor de una opción de configuración (por ejemplo, la confirmación excesiva de memoria) ha impedido el inicio del servidor.
  
   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr -f
   ```

### <a name="start-sql-server-in-single-user-mode"></a>Iniciar SQL Server en modo de usuario único
En determinadas circunstancias, debe iniciar una instancia de SQL Server en modo de usuario único mediante la opción de inicio -m. Por ejemplo, es posible que desee cambiar las opciones de configuración del servidor o recuperar una base de datos maestra dañada u otra base de datos del sistema. Por ejemplo, es posible que desee cambiar las opciones de configuración del servidor o recuperar una base de datos maestra dañada u otra base de datos del sistema   

Iniciar SQL Server en modo de usuario único
   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr -m
   ```

Iniciar SQL Server en modo de usuario único con SQLCMD
   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr -m SQLCMD
   ```
  
> [!WARNING]  
>  Inicie SQL Server en Linux con el usuario "mssql" para evitar problemas de inicio futuros. Ejemplo "sudo -u mssql /opt/mssql/bin/sqlservr [OPCIONES DE INICIO]" 

Si accidentalmente han iniciado SQL Server con otro usuario, debe cambiar la propiedad de los archivos de base de datos de SQL Server al usuario 'mssql' antes de iniciar SQL Server con systemd. Por ejemplo, para cambiar la propiedad de todos los archivos de base de datos de /var/opt/mssql al usuario "mssql", ejecute el siguiente comando

   ```bash
   chown -R mssql:mssql /var/opt/mssql/
   ```

## <a name="rebuild-system-databases"></a>Volver a generar las bases de datos del sistema
Como último recurso, puede elegir volver a generar al maestro y realizar una copia de bases de datos de modelo para versiones predeterminadas.

> [!WARNING]
> Estos pasos le **eliminar todos los datos del sistema de SQL Server** que ha configurado. Esto incluye información acerca de las bases de datos de usuario (pero no las bases de datos de usuario a sí mismos). También eliminará otra información almacenada en las bases de datos del sistema, incluidos los siguientes: información de clave maestra, los certificados cargados en master, la contraseña de inicio de sesión SA, la información relacionada con el trabajo de msdb, información de correo electrónico de base de datos de msdb y las opciones de sp_configure. Use sólo si comprende las implicaciones.

1. Detener SQL Server.

   ```bash
   sudo systemctl stop mssql-server
   ```

1. Ejecute **sqlservr** con el **force-setup** parámetro. 

   ```bash
   sudo -u mssql /opt/mssql/bin/sqlservr --force-setup
   ```
   
   > [!WARNING]
   > Vea la advertencia anterior. Además, debe ejecutar esto como el **mssql** usuario tal como se muestra aquí.

1. Una vez que aparezca el mensaje "Recuperación completada", presione CTRL+C. Esto se apagará de SQL Server

1. Volver a configurar la contraseña de SA.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set-sa-password
   ```
   
1. Iniciar SQL Server y vuelva a configurar el servidor. Esto incluye restaurar o volver a adjuntar las bases de datos de usuario.

   ```bash
   sudo systemctl start mssql-server
   ```

## <a name="improve-performance"></a>Mejorar el rendimiento

Hay muchos factores que afectan al rendimiento, incluidos el diseño de la base de datos, el hardware y las demandas de carga de trabajo. Si desea para mejorar el rendimiento, comience por revisar las prácticas recomendadas en el artículo, [procedimientos recomendados e instrucciones de configuración de SQL Server en Linux](sql-server-linux-performance-best-practices.md). A continuación, explore algunas de las herramientas disponibles para solucionar problemas de rendimiento.

- [Almacén de consultas](../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)
- [Vistas del sistema de administración dinámica (DMV)](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)
- [Panel de rendimiento en SQL Server Management Studio](https://blogs.msdn.microsoft.com/sql_server_team/new-in-ssms-performance-dashboard-built-in/)

## <a name="common-issues"></a>Problemas comunes

1. No se puede conectar a la instancia remota de SQL Server.

   Consulte la sección de solución de problemas del artículo, [conectar con SQL Server en Linux](#connection).

2. ERROR: El nombre de host debe tener 15 caracteres o menos.

   Se trata de un problema conocido que ocurre siempre que el nombre de la máquina que está intentando instalar el paquete de Debian en SQL Server tiene más de 15 caracteres. Actualmente no hay ningún soluciones alternativas que no sea de cambiar el nombre de la máquina. Es una manera de lograr esto, edite el archivo de nombre de host y reiniciar el equipo. La siguiente [Guía del sitio Web](https://www.cyberciti.biz/faq/ubuntu-change-hostname-command/) Esto se explica en detalle.

3. Restablecer la contraseña de administración (SA) del sistema.

   Si ha olvidado la contraseña de administrador (SA) del sistema o necesita restablecerla por algún otro motivo, siga estos pasos.

   > [!NOTE]
   > Los pasos siguientes detenga temporalmente el servicio SQL Server.

   Inicie sesión en el terminal de host, ejecute los comandos siguientes y siga las indicaciones para restablecer la contraseña de SA:

   ```bash
   sudo systemctl stop mssql-server
   sudo /opt/mssql/bin/mssql-conf setup
   ```

4. Uso de caracteres especiales en la contraseña.

   Si usas algunos caracteres en la contraseña de inicio de sesión de SQL Server, es posible que deba aplíqueles una barra diagonal inversa cuando se usan en un comando de Linux en el terminal. Por ejemplo, debe realizar el escape el signo de dólar ($) cada vez que se usa en una secuencia de comandos/shell de comandos de terminal:

   No funciona:

   ```bash
   sudo sqlcmd -S myserver -U sa -P Test$$
   ```

   Funciona:

   ```bash
   sqlcmd -S myserver -U sa -P Test\$\$
   ```

   Recursos: [caracteres especiales](https://tldp.org/LDP/abs/html/special-chars.html)
   [Escaping](https://tldp.org/LDP/abs/html/escapingsection.html)

[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]
