---
title: Comentarios de los clientes de SQL Server en Linux | Documentos de Microsoft
description: Describe cómo se recopilan y se configura en Linux comentarios del cliente de SQL Server.
author: annashres
ms.author: anshrest
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql
ms.prod_service: database-engine
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.openlocfilehash: 278b53003fd04ccc8692b205124c85ca366f96f7
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="customer-feedback-for-sql-server-on-linux"></a>Comentarios de los clientes de SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

De forma predeterminada, Microsoft SQL Server recopila información sobre cómo sus clientes usan la aplicación. En concreto, SQL Server recopila información sobre la experiencia de instalación, el uso y el rendimiento. Esta información ayuda a Microsoft a mejorar el producto para satisfacer mejor las necesidades del cliente. Por ejemplo, Microsoft recopila información sobre los tipos de códigos de error que encuentran los clientes para que podamos corregir errores relacionados, mejorar nuestra documentación sobre cómo usar SQL Server y determinar si deben agregarse características al producto para ofrecer un mejor servicio a los clientes.

Este documento proporciona información detallada sobre qué tipos de información se recopilan y sobre cómo configurar Microsoft SQL Server en Linux para enviar que recopilan información a Microsoft. SQL Server 2017 incluye una declaración de privacidad que explica qué información y no se recopilan de los usuarios. Lea la declaración de privacidad.

En concreto, Microsoft no envía ninguno de los tipos de información siguientes a través de este mecanismo:

- Valores de dentro de las tablas de usuario
- Credenciales de inicio de sesión u otra información de autenticación
- Información de identificación personal (PII)

SQL Server 2017 siempre recopila y envía información sobre la experiencia de instalación del proceso de configuración para que podamos encontrar y corregir con rapidez cualquier problema de instalación que experimente el cliente. SQL Server 2017 puede configurarse para que no envíe información (en forma de instancia por servidor) a Microsoft a través de **mssql-conf**. MSSQL-conf es un script de configuración que se instala con SQL Server 2017 para Red Hat Enterprise Linux, SUSE Linux Enterprise Server y Ubuntu.

> [!NOTE]
> Puede deshabilitar el envío de información a Microsoft solo en versiones de pago de SQL Server.

## <a name="disable-customer-feedback"></a>Deshabilitar los comentarios de clientes

Esta opción permite cambiar si SQL Server envía comentarios a Microsoft o no. De forma predeterminada, este valor se establece en true. Para cambiar el valor, ejecute los siguientes comandos:

### <a name="on-red-hat-suse-and-ubuntu"></a>En Red Hat, SUSE y Ubuntu

1. Ejecute el script mssql-conf como raíz con el **establecer** comando para **telemetry.customerfeedback**. En el ejemplo siguiente se desactiva los comentarios de clientes mediante la especificación de **false**.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.customerfeedback false
   ```

1. Reinicie el servicio de SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```
   
### <a name="on-docker"></a>En Docker
Para deshabilitar los comentarios de clientes en docker, debe tener Docker [conservar los datos](sql-server-linux-configure-docker.md). 

1. Agregar un `mssql.conf` archivo con las líneas `[telemetry]` y `customerfeedback = false` en el directorio de host:
 
   ```bash
   echo '[telemetry]' >> <host directory>/mssql.conf
   ```

   ```bash
   echo 'customerfeedback = false' >> <host directory>/mssql.conf
   ```
2. Ejecutar la imagen de contenedor
   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux:2017-latest
   ```
   
## <a name="local-audit-for-sql-server-on-linux-usage-feedback-collection"></a>Auditoría local de SQL Server en la recopilación de comentarios de uso de Linux

Microsoft SQL Server 2017 contiene características habilitadas para Internet que pueden recopilar y enviar a Microsoft información sobre el equipo o dispositivo ("información estándar del equipo"). El componente de auditoría Local de la recopilación de comentarios de uso de SQL Server puede escribir los datos recopilados por el servicio en una carpeta designada, que representa los datos (registros) que se enviará a Microsoft. El propósito de la Auditoría local es permitir que los clientes vean todos los datos que Microsoft recopila con esta característica, por motivos de cumplimiento, reglamentarios o por validación de privacidad.

En SQL Server en Linux, auditoría Local es configurable en el nivel de instancia para el motor de base de datos de SQL Server. Otros componentes de SQL Server y las herramientas de SQL Server no tiene capacidad de auditoría Local para la recopilación de comentarios de uso.

### <a name="enable-local-audit"></a>Habilitar la auditoría Local

Esta opción habilita la auditoría Local y le permite establecer el directorio donde se crean los registros de auditoría Local.

1. Cree un directorio de destino para los nuevos registros de auditoría Local. En el ejemplo siguiente se crea un nuevo **/tmp/auditoría** directorio:

   ```bash
   sudo mkdir /tmp/audit
   ```

1. Cambiar el propietario y el grupo del directorio para la **mssql** usuario:

   ```bash
   sudo chown mssql /tmp/audit
   sudo chgrp mssql /tmp/audit
   ```

1. Ejecute el script mssql-conf como raíz con el **establecer** comando para **telemetry.userrequestedlocalauditdirectory**:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.userrequestedlocalauditdirectory /tmp/audit
   ```

1. Reinicie el servicio de SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```
   
### <a name="on-docker"></a>En Docker
Para habilitar la auditoría Local en docker, debe tener Docker [conservar los datos](sql-server-linux-configure-docker.md). 

1. El directorio de destino para los nuevos registros de auditoría Local estará en el contenedor. Cree un directorio de destino para los nuevos registros de auditoría Local en el directorio de host en su equipo. En el ejemplo siguiente se crea un nuevo **/auditoría** directorio:

   ```bash
   sudo mkdir <host directory>/audit
   ```

   
1. Agregar un `mssql.conf` archivo con las líneas `[telemetry]` y `userrequestedlocalauditdirectory = <host directory>/audit` en el directorio de host:
 
   ```bash
   echo '[telemetry]' >> <host directory>/mssql.conf
   ```

   ```bash
   echo 'userrequestedlocalauditdirectory = <host directory>/audit' >> <host directory>/mssql.conf
   ```
2. Ejecutar la imagen de contenedor
   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d microsoft/mssql-server-linux:2017-latest
   ```
   
## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de SQL Server en Linux, consulte la [información general de SQL Server en Linux](sql-server-linux-overview.md).
