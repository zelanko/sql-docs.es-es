---
title: Solucionar problemas de SQL Server en Linux | Documentos de Microsoft
description: Proporciona sugerencias para solucionar problemas para utilizar SQL Server 2017 en Linux.
author: annashres
ms.author: anshrest
manager: jhubbard
ms.date: 05/08/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 99636ee8-2ba6-4316-88e0-121988eebcf9S
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 21b7d94bcf15e1ae2d99dd44f4b0030929b92111
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="troubleshoot-sql-server-on-linux"></a>Solucionar problemas de SQL Server en Linux

Este documento describe cómo solucionar problemas de Microsoft SQL Server que se ejecutan en Linux o en un contenedor de Docker. Cuando solucione problemas de SQL Server en Linux, asegúrese de recordar las limitaciones de esta versión de vista previa privada. Puede encontrar una lista de estas opciones en el [notas de la versión](sql-server-linux-release-notes.md).

## <a id="connection"></a>Solucionar problemas de errores de conexión
Si tiene dificultades para conectarse a SQL Server de Linux, hay algunas cosas para comprobar. 

- Compruebe que el nombre del servidor o la dirección IP sea accesible desde el equipo cliente.

   > [!TIP]
   > Para buscar la dirección IP de la máquina de Ubuntu, puede ejecutar el comando ifconfig como en el ejemplo siguiente:
   >
   >   ```bash
   >   sudo ifconfig eth0 | grep 'inet addr'
   >   ```
   > Para Red Hat, puede utilizar la dirección ip como en el ejemplo siguiente:
   >
   >   ```bash
   >   sudo ip addr show eth0 | grep "inet"
   >   ```
   > Una excepción a esta técnica se relaciona con máquinas virtuales de Azure. Para las máquinas virtuales de Azure, [buscar la dirección IP pública para la máquina virtual en el portal de Azure](sql-server-linux-azure-virtual-machine.md#connect).

- Si es aplicable, compruebe que ha abierto el puerto de SQL Server (predeterminado: 1433) en el firewall.

- Para las máquinas virtuales de Azure, compruebe que tiene un [regla de grupo de seguridad de red para el puerto de SQL Server predeterminado](sql-server-linux-azure-virtual-machine.md#remote).

- Compruebe que el nombre de usuario y la contraseña no contienen los errores tipográficos o espacios en blanco adicionales o incorrecta entre mayúsculas y minúsculas.

- Intente establecer explícitamente el número de puerto y protocolo con el nombre del servidor similar al siguiente: **tcp:servername, 1433**.

- Problemas de conectividad de red también pueden provocar tiempos de espera y errores de conexión. Después de comprobar la información de conexión y la conectividad de red, intente conectarse de nuevo.

## <a name="manage-the-sql-server-service"></a>Administrar el servicio de SQL Server

Las secciones siguientes muestran cómo iniciar, detener, reiniciar y comprobar el estado del servicio SQL Server. 

### <a name="manage-the-mssql-server-service-in-red-hat-enterprise-linux-rhel-and-ubuntu"></a>Administrar el servicio mssql server en Red Hat Enterprise Linux (RHEL) y Ubuntu 

Compruebe el estado del estado del servicio de SQL Server con este comando:

   ```bash
   sudo systemctl status mssql-server
   ```

Puede detener, iniciar o reiniciar el servicio de SQL Server según sea necesario mediante los siguientes comandos:

   ```bash
   sudo systemctl stop mssql-server
   sudo systemctl start mssql-server
   sudo systemctl restart mssql-server
   ```

### <a name="manage-the-execution-of-the-mssql-docker-container"></a>Administrar la ejecución del contenedor de Docker mssql

Puede obtener el identificador de estado y el contenedor del contenedor de Docker de SQL Server más reciente creado ejecutando el comando siguiente (identificador estarán en la columna "Id. de contenedor"):

   ```bash
   sudo docker ps -l
   ```
   
Puede detener o reiniciar el servicio SQL Server según sea necesario mediante los siguientes comandos:
   
   ```bash
   sudo docker stop <container ID>
   sudo docker restart <container ID>
   ```

> [!TIP]
> Para más sugerencias para solucionar problemas de Docker, consulte [contenedores de solución de problemas de SQL Server Docker](sql-server-linux-configure-docker.md#troubleshooting).

## <a name="access-the-log-files"></a>Obtener acceso a los archivos de registro
   
Los registros del motor de SQL Server en el archivo /var/opt/mssql/log/errorlog en las instalaciones de Linux y Docker. Debe estar en modo de 'superusuario' para buscar este directorio.

El programa de instalación se registra aquí: / var/opt/mssql/setup-< marca de tiempo que representa el tiempo de instalación > puede examinar los archivos de registro de errores con cualquier herramienta compatible de UTF-16 como 'vim' o 'cat' similar a la siguiente: 

   ```bash
   sudo cat errorlog
   ```

Si lo prefiere, también puede convertir los archivos a UTF-8 para leerlos con 'más' o 'menos' con el siguiente comando:
   
   ```bash
   sudo iconv –f UTF-16LE –t UTF-8 <errorlog> -o <output errorlog file>
   ```
## <a name="extended-events"></a>Eventos extendidos

Eventos extendidos se pueden consultar a través de un comando SQL.  Puede encontrar más información sobre los eventos extendidos [aquí](https://technet.microsoft.com/en-us/library/bb630282.aspx):

## <a name="crash-dumps"></a>Volcados de memoria 

Busque los archivos de volcado en el directorio de registro en Linux. Busque en el directorio /var/opt/mssql/log de volcados de memoria de núcleo de Linux (. tar.gz2 extensión) o minivolcados SQL (extensión .mdmp)

Para los volcados del núcleo 
   ```bash
   sudo ls /var/opt/mssql/log | grep .tar.gz2 
   ```

Para archivos de volcado SQL 
   ```bash
   sudo ls /var/opt/mssql/log | grep .mdmp 
   ```

## <a name="common-issues"></a>Problemas comunes

1. No se puede conectar a la instancia remota de SQL Server.

   Vea la sección Solución de problemas del tema, [conectar con SQL Server en Linux](#connection).

2. ERROR: El nombre de host debe ser de 15 caracteres o menos.

   Se trata de un problema conocido que ocurre siempre que el nombre de la máquina que está intentando instalar el paquete de Debian de SQL Server tiene más de 15 caracteres. No hay ningún soluciones alternativas que no sea de cambiar el nombre de la máquina. Una manera de conseguirlo es modificando el archivo de nombre de host y reiniciar el equipo. El siguiente [Guía del sitio Web](http://www.cyberciti.biz/faq/ubuntu-change-hostname-command/) Esto se explica en detalle.

3. Restablecer la contraseña del sistema (SA) de administración.

   Si ha olvidado la contraseña de administrador (SA) del sistema o si necesita restablecer por algún otro motivo, siga estos pasos.

   > [!NOTE]
   > Siga estos pasos se detendrá temporalmente el servicio SQL Server.

   Inicie sesión en el terminal de host, ejecute los siguientes comandos y siga las indicaciones para restablecer la contraseña del administrador:

   ```bash
   sudo systemctl stop mssql-server
   sudo /opt/mssql/bin/mssql-conf setup
   ```

4. Uso de caracteres especiales en la contraseña.

   Si usas algunos caracteres de la contraseña de inicio de sesión de SQL Server debe ponerlos cuando se usen en el terminal de Linux. Necesitará el $ de escape en cualquier momento mediante el carácter de barra diagonal inversa se usa en un script de shell de comandos/terminal:

   No funciona:

   ```bash
   sudo sqlcmd -S myserver -U sa -P Test$$
   ```

   Funciona:

   ```bash
   sqlcmd -S myserver -U sa -P Test\$\$
   ```

   Recursos: [caracteres especiales](http://tldp.org/LDP/abs/html/special-chars.html)
   [Escaping](http://tldp.org/LDP/abs/html/escapingsection.html)

## <a name="support"></a>Soporte técnico

Soporte técnico está disponible a través de la Comunidad y supervisado por el equipo de ingeniería. Para preguntas específicas, use los siguientes recursos:

- [Cambio de la pila de DBA](https://dba.stackexchange.com/questions/tagged/sql-server): formular preguntas de administración de base de datos
- [Desbordamiento de pila](http://stackoverflow.com/questions/tagged/sql-server): formular preguntas de desarrollo
- [Foros de MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?category=sqlserver): hacer preguntas técnicas
- [Microsoft Connect](https://connect.microsoft.com/SQLServer/Feedback): informe de errores y la característica de solicitud
- [Reddit](https://www.reddit.com/r/SQLServer/): analizar SQL Server
