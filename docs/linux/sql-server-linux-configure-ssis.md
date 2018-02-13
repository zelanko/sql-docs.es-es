---
title: Configurar SSIS en Linux con ssis-conf | Documentos de Microsoft
description: "En este artículo se describe cómo configurar SQL Server Integration Services (SSIS) en Linux con la utilidad de ssis-conf."
author: leolimsft
ms.author: lle
ms.reviewer: douglasl
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.workload: Inactive
ms.openlocfilehash: ee15f5b5124d96b2f8033515f95f03c3aab89ae3
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/13/2018
---
# <a name="configure-sql-server-integration-services-on-linux-with-ssis-conf"></a>Configurar SQL Server Integration Services en Linux con ssis-conf

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Ejecutar el `ssis-conf` script de configuración al instalar SQL Server Integration Services (SSIS) para Red Hat Enterprise Linux y Ubuntu. Para obtener más información acerca de cómo instalar SSIS, vea [instalar SQL Server Integration Services (SSIS) en Linux](sql-server-linux-setup-ssis.md).

También puede usar el `ssis-conf` utilidad para configurar las propiedades siguientes:

| Command | Description |
|-------------|---------------------------------------------------------------------|
| edición de conjunto | Establecer la edición de SQL Server                                       |
| Telemetría   | Habilitar o deshabilitar el servicio de telemetría de SQL Server Integration Services |
| instalar       | Inicializar y configurar Microsoft SQL Server Integration Services      |
|||

## <a name="run-ssis-conf"></a>Ejecutar conf de ssis

Los ejemplos de este artículo ejecutar `ssis-conf` especificando la ruta de acceso completa: `/opt/ssis/bin/ssis-conf`. Si se desplaza a esa ubicación antes de ejecutar `ssis-conf`, puede ejecutar la utilidad en el contexto del directorio actual: `./ssis-conf`.

Asegúrese de ejecutar los comandos que se describen en este artículo con privilegios de raíz. Por ejemplo, ejecutar `sudo /opt/ssis/bin/ssis-conf setup` y no `/opt/ssis/bin/ssis-conf setup`.

Para ejecutar estos comandos con los mensajes en el idioma que prefiera, puede especificar una configuración regional. Por ejemplo, para recibir mensajes en chino, ejecute el siguiente comando: `sudo LC_ALL=zh_CN.UTF-8 /opt/ssis/bin/ssis-conf setup`.

## <a name="use-set-edition-to-set-the-edition-of-sql-server-integration-services"></a>Utilice Edición de conjunto para establecer la edición de SQL Server Integration Services

La edición de SSIS se alinea con la edición de SQL Server.

Escriba el siguiente comando: `$ sudo /opt/ssis/bin/ssis-conf set-edition`.

Después de escribir el comando, recibirá el mensaje siguiente:

```
Choose an edition of SQL Server:

1) Evaluation (free, no production use rights, 180-day limit)

2) Developer (free, no production use rights)

3) Express (free)

4) Web (PAID)

5) Standard (PAID)

6) Enterprise (PAID)

7) Enterprise Core (PAID)

8) I bought a license through a retail sales channel and have a product key to enter.

Details about editions can be found at https://go.microsoft.com/fwlink/?LinkId=852748&clcid=0x409.

Use of PAID editions of this software requires separate licensing through a Microsoft Volume Licensing program.

By choosing a PAID edition, you are verifying that you have the appropriate number of licenses in place to install and run this software.

Enter your edition (1-8):
```

Si escribe un valor de 1 a 7, el sistema configura una edición gratuita o de pago. Si escribe 8, la utilidad le pide que escriba la clave de producto que se compraron:

```
Enter the 25-character product key:
```

## <a name="use-telemetry-to-configure-customer-feedback"></a>Use la telemetría para configurar los comentarios de clientes

El `telemetry` comando determina si SSIS envía comentarios a Microsoft.

Para las ediciones gratuitas (es decir, las ediciones Express, Developer y Evaluation), el servicio de telemetría siempre está habilitado. Si tiene una edición gratuita, no se puede usar el `telemetry` comando para deshabilitar la telemetría.

Escriba el siguiente comando: `$ sudo /opt/ssis/bin/ssis-conf telemetry`.

Para las ediciones de pago, después de escribir el comando, recibirá el mensaje siguiente:

```
Send feature usage data to Microsoft. Feature usage data includes information about your hardware configuration and how you use SQL Server Integration Services.

[Yes/No]:
```

Si selecciona **Sí**, el servicio de telemetría está habilitado y empieza a ejecutarse. El servicio se inicia automáticamente después de cada arranque. Si selecciona **n**, detiene el servicio de telemetría y está deshabilitado.

## <a name="use-setup-to-initialize-and-set-up-microsoft-sql-server-integration-services"></a>Utilice el programa de instalación para inicializar y configurar Microsoft SQL Server Integration Services

Use la `setup` comando cada vez que se instala SSIS.

Escriba el siguiente comando: `sudo /opt/ssis/bin/ssis-conf setup`.

La utilidad le pedirá que confirme o proporcionar valores para los siguientes elementos:
-   Licencia del producto
-   Acuerdo de términos de licencia
-   Servicio de telemetría
-   El idioma utilizado por Integration Services

Para ejecutar el `setup` comando con mensajes en el idioma que prefiera, puede especificar una configuración regional. Por ejemplo, para recibir mensajes en chino, ejecute el siguiente comando: `sudo LC_ALL=zh_CN.UTF-8 /opt/ssis/bin/ssis-conf setup`.

## <a name="ssisconf-format"></a>formato de SSIS.conf

El siguiente `/var/opt/ssis/ssis.conf` archivo proporciona un ejemplo para cada configuración.

Para SQL Server, puede cambiar la configuración del sistema cambiando los valores en el `mssql.conf` archivo. Para SSIS, se *no* cambiar la configuración del sistema cambiando los valores en el `ssis.conf` archivo. El `ssis.conf` archivo muestra solo los resultados de la instalación. Si desea cambiar la configuración de SSIS, puede eliminar el `ssis.conf` de archivos y ejecutar el `setup` comando nuevo.

Este es un ejemplo `ssis.conf` archivo. Cada campo corresponde al resultado de un paso de instalación.

```
[LICENSE]
                       
registered = Y        
                       
pid = enterprisecore  
                       
[EULA]
                       
accepteula = Y        
                       
[TELEMETRY]
                       
enabled = Y           
                       
[language]
                       
lcid = 2052
```
