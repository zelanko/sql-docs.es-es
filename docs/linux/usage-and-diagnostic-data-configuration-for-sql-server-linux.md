---
title: Configurar el uso y recopilación de datos de diagnóstico para SQL Server en Linux | Microsoft Docs
description: Describe cómo el uso del cliente de SQL Server y datos de diagnóstico se recopilan y configurado en Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 03/27/2019
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: c94023e89dbdfb784f2b1bc8db8c9842c4455fb1
ms.sourcegitcommit: aa4f594ec6d3e85d0a1da6e69fa0c2070d42e1d8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59243609"
---
# <a name="configure-usage-and-diagnostic-data-collection-for-sql-server-on-linux"></a>Configurar el uso y recopilación de datos de diagnóstico para SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

De forma predeterminada, Microsoft SQL Server recopila información sobre cómo sus clientes usan la aplicación. En concreto, SQL Server recopila información sobre la experiencia de instalación, el uso y el rendimiento. Esta información ayuda a Microsoft a mejorar el producto para satisfacer mejor las necesidades del cliente. Por ejemplo, Microsoft recopila información sobre los tipos de códigos de error que encuentran los clientes para que podamos corregir errores relacionados, mejorar nuestra documentación sobre cómo usar SQL Server y determinar si deben agregarse características al producto para ofrecer un mejor servicio a los clientes.

Este documento proporciona detalles acerca de qué tipos de información se recopilan y cómo configurar Microsoft SQL Server en Linux para enviar ese recopilados a Microsoft. SQL Server 2017 incluye una declaración de privacidad que explica qué información y no se recopilan de los usuarios. Para obtener más información, consulte el [declaración de privacidad](https://go.microsoft.com/fwlink/?LinkID=868444).

En concreto, Microsoft no envía ninguno de los tipos de información siguientes a través de este mecanismo:

- Valores de dentro de las tablas de usuario
- Credenciales de inicio de sesión u otra información de autenticación
- Información de identificación personal (PII)

SQL Server 2017 siempre recopila y envía información sobre la experiencia de instalación del proceso de configuración para que podamos encontrar y corregir con rapidez cualquier problema de instalación que experimente el cliente. SQL Server 2017 puede configurarse para que no envíe información (en forma de instancia por servidor) a Microsoft a través de **mssql-conf**. MSSQL-conf es un script de configuración que se instala con SQL Server 2017 para Red Hat Enterprise Linux, SUSE Linux Enterprise Server y Ubuntu.

> [!NOTE]
> Puede deshabilitar el envío de información a Microsoft solo en versiones de pago de SQL Server.

## <a name="disable-usage-and-diagnostic-data-collection"></a>Deshabilitar la recopilación de datos de diagnóstico y uso

Esta opción le permite cambiar si SQL Server envía uso y recopilación de datos de diagnóstico a Microsoft o no. De forma predeterminada, este valor se establece en true. Para cambiar el valor, ejecute los siguientes comandos:

> [!IMPORTANT]
> Puede no desactivar uso y recopilación de datos de diagnóstico de forma gratuita las ediciones de SQL Server, Express y Developer.

### <a name="on-red-hat-suse-and-ubuntu"></a>En Red Hat, SUSE y Ubuntu

1. Ejecute el script mssql-conf como raíz con el **establecer** comando para **telemetry.customerfeedback**. El ejemplo siguiente se desactiva la recopilación de datos de diagnóstico y uso mediante la especificación de **false**.

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.customerfeedback false
   ```

1. Reinicie el servicio de SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```
   
### <a name="on-docker"></a>En Docker
Para deshabilitar el uso y recopilación de datos de diagnóstico en docker, debe tener Docker [conservar los datos](sql-server-linux-configure-docker.md). 

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

1. Agregar un `mssql.conf` archivo con las líneas `[telemetry]` y `customerfeedback = false` en el directorio de host:
 
   ```bash
   echo '[telemetry]' >> <host directory>/mssql.conf
   ```

   ```bash
   echo 'customerfeedback = false' >> <host directory>/mssql.conf
   ```

2. Ejecutar la imagen de contenedor

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
   ```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

1. Agregar un `mssql.conf` archivo con las líneas `[telemetry]` y `customerfeedback = false` en el directorio de host:

   ```bash
   echo '[telemetry]' >> <host directory>/mssql.conf
   ```

   ```bash
   echo 'customerfeedback = false' >> <host directory>/mssql.conf
   ```

2. Ejecutar la imagen de contenedor

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
   ```

::: moniker-end

## <a name="local-audit-for-sql-server-on-linux-usage-and-diagnostic-data-collection"></a>Auditoría local de SQL Server en Linux uso y recopilación de datos de diagnóstico

Microsoft SQL Server 2017 contiene características habilitadas para Internet que pueden recopilar y enviar a Microsoft información sobre el equipo o dispositivo ("información estándar del equipo"). El componente de auditoría Local de recopilación de datos de diagnóstico y uso de SQL Server puede escribir los datos recopilados por el servicio en una carpeta designada, que representa los datos (registros) que se enviará a Microsoft. El propósito de la Auditoría local es permitir que los clientes vean todos los datos que Microsoft recopila con esta característica, por motivos de cumplimiento, reglamentarios o por validación de privacidad.

En SQL Server en Linux, auditoría Local es configurable en el nivel de instancia para motor de base de datos de SQL Server. Otros componentes de SQL Server y las herramientas de SQL Server no tienen capacidad de auditoría Local para la recopilación de datos de diagnóstico y uso.

### <a name="enable-local-audit"></a>Habilitar auditoría Local

Esta opción habilita la auditoría Local y le permite establecer el directorio donde se crean los registros de auditoría Local.

1. Cree un directorio de destino para los nuevos registros de auditoría Local. En el ejemplo siguiente se crea un nuevo **/tmp/auditoría** directorio:

   ```bash
   sudo mkdir /tmp/audit
   ```

2. Cambiar el propietario y el grupo del directorio para el **mssql** usuario:

   ```bash
   sudo chown mssql /tmp/audit
   sudo chgrp mssql /tmp/audit
   ```

3. Ejecute el script mssql-conf como raíz con el **establecer** comando para **telemetry.userrequestedlocalauditdirectory**:

   ```bash
   sudo /opt/mssql/bin/mssql-conf set telemetry.userrequestedlocalauditdirectory /tmp/audit
   ```

4. Reinicie el servicio de SQL Server:

   ```bash
   sudo systemctl restart mssql-server
   ```
   
### <a name="on-docker"></a>En Docker
Para habilitar la auditoría Local de docker, debe tener Docker [conservar los datos](sql-server-linux-configure-docker.md). 

<!--SQL Server 2017 on Linux -->
::: moniker range="= sql-server-linux-2017 || = sql-server-2017"

1. El directorio de destino para los nuevos registros de auditoría Local estará en el contenedor. Cree un directorio de destino para los nuevos registros de auditoría Local en el directorio de host en el equipo. En el ejemplo siguiente se crea un nuevo **auditoría** directorio:

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

1. Ejecutar la imagen de contenedor

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2017-latest
   ```

::: moniker-end
<!--SQL Server 2019 on Linux-->
::: moniker range=">= sql-server-linux-ver15 || >= sql-server-ver15 || =sqlallproducts-allversions"

1. El directorio de destino para los nuevos registros de auditoría Local estará en el contenedor. Cree un directorio de destino para los nuevos registros de auditoría Local en el directorio de host en el equipo. En el ejemplo siguiente se crea un nuevo **auditoría** directorio:

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

1. Ejecutar la imagen de contenedor

   ```bash
   docker run -e 'ACCEPT_EULA=Y' -e 'MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>' -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
   ```

   ```PowerShell
   docker run -e "ACCEPT_EULA=Y" -e "MSSQL_SA_PASSWORD=<YourStrong!Passw0rd>" -p 1433:1433 -v <host directory>:/var/opt/mssql -d mcr.microsoft.com/mssql/server:2019-CTP2.4-ubuntu
   ```

::: moniker-end

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de SQL Server en Linux, consulte el [información general de SQL Server en Linux](sql-server-linux-overview.md).
