---
title: Configurar SSIS en Linux con ssis-conf
description: En este artículo se describe cómo configurar SQL Server Integration Services (SSIS) en Linux con la utilidad de ssis-conf.
author: lrtoyou1223
ms.author: lle
ms.reviewer: maghan
manager: jroth
ms.date: 10/02/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 0a6fc4a73d8991626c53d9caa8671673c0164a10
ms.sourcegitcommit: 93d1566b9fe0c092c9f0f8c84435b0eede07019f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2019
ms.locfileid: "67833992"
---
# <a name="configure-sql-server-integration-services-on-linux-with-ssis-conf"></a>Configurar SQL Server Integration Services en Linux con ssis-conf

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Ejecutar el `ssis-conf` script de configuración al instalar SQL Server Integration Services (SSIS) para Red Hat Enterprise Linux y Ubuntu. Para obtener más información acerca de cómo instalar SSIS, vea [instalar SQL Server Integration Services (SSIS) en Linux](sql-server-linux-setup-ssis.md).

También puede usar el `ssis-conf` utilidad para configurar las propiedades siguientes:

| Comando | Descripción |
|-------------|---------------------------------------------------------------------|
| set-edition | Establezca la edición de SQL Server                                       |
| datos de telemetría   | Habilitar o deshabilitar el servicio de telemetría de SQL Server Integration Services |
| instalar       | Inicializar y configurar Microsoft SQL Server Integration Services      |
|||

## <a name="run-ssis-conf"></a>Ejecución de ssis-conf

Los ejemplos de este artículo ejecutar `ssis-conf` especificando la ruta de acceso completa: `/opt/ssis/bin/ssis-conf`. Si se desplaza a esa ubicación antes de ejecutar `ssis-conf`, puede ejecutar la utilidad en el contexto del directorio actual: `./ssis-conf`.

Asegúrese de ejecutar los comandos que se describen en este artículo con privilegios raíz. Por ejemplo, ejecute `sudo /opt/ssis/bin/ssis-conf setup` y no `/opt/ssis/bin/ssis-conf setup`.

Para ejecutar estos comandos con mensajes en el idioma que prefiera, puede especificar una configuración regional. Por ejemplo, para recibir mensajes en chino, ejecute el siguiente comando: `sudo LC_ALL=zh_CN.UTF-8 /opt/ssis/bin/ssis-conf setup`.

## <a name="use-set-edition-to-set-the-edition-of-sql-server-integration-services"></a>Use set-edition para establecer la edición de SQL Server Integration Services

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

Si escribe un valor de 1 a 7, el sistema configura una edición gratuita o de pago. Si escribe 8, la utilidad le pedirá que escriba la clave de producto que ha comprado:

```
Enter the 25-character product key:
```

## <a name="use-telemetry-to-configure-customer-feedback"></a>Usar la telemetría para configurar los comentarios de clientes

El `telemetry` comando determina si SSIS envía comentarios a Microsoft.

Para las ediciones gratuita (es decir, las ediciones Evaluation, Developer y Express), siempre está habilitado el servicio de telemetría. Si tiene una edición gratuita, no puede usar el `telemetry` comando para deshabilitar la telemetría.

Escriba el siguiente comando: `$ sudo /opt/ssis/bin/ssis-conf telemetry`.

Para las ediciones de pago después de escribir el comando, recibirá el mensaje siguiente:

```
Send feature usage data to Microsoft. Feature usage data includes information about your hardware configuration and how you use SQL Server Integration Services.

[Yes/No]:
```

Si selecciona **Sí**, el servicio de telemetría se habilita y comienza a ejecutarse. El servicio se inicia automáticamente después de cada arranque. Si selecciona **No**, detiene el servicio de telemetría y está deshabilitado.

## <a name="use-setup-to-initialize-and-set-up-microsoft-sql-server-integration-services"></a>Utilice el programa de instalación para inicializar y configurar Microsoft SQL Server Integration Services

Use el `setup` comando cada vez que se instala SSIS.

Escriba el siguiente comando: `sudo /opt/ssis/bin/ssis-conf setup`.

La utilidad le pedirá que confirme o proporcionar valores para los siguientes elementos:
-   Licencia de producto
-   Contrato de licencia
-   Servicio de telemetría
-   El idioma utilizado por Integration Services

Para ejecutar el `setup` comando con mensajes en el idioma que prefiere, puede especificar una configuración regional. Por ejemplo, para recibir mensajes en chino, ejecute el siguiente comando: `sudo LC_ALL=zh_CN.UTF-8 /opt/ssis/bin/ssis-conf setup`.

## <a name="ssisconf-format"></a>formato SSIS.conf

La siguiente `/var/opt/ssis/ssis.conf` archivo proporciona un ejemplo para cada configuración.

Para SQL Server, puede cambiar la configuración del sistema cambiando los valores en el `mssql.conf` archivo. Para SSIS, le *no* cambiar la configuración del sistema cambiando los valores en el `ssis.conf` archivo. El `ssis.conf` archivo muestra solamente los resultados de la instalación. Si desea cambiar la configuración de SSIS, puede eliminar el `ssis.conf` de archivos y ejecutar el `setup` nuevo comando.

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

## <a name="related-content-about-ssis-on-linux"></a>Contenido relacionado sobre SSIS en Linux
-   [Extraer, transformar y cargar datos en Linux con SSIS](sql-server-linux-migrate-ssis.md)
-   [Instalar SQL Server Integration Services (SSIS) en Linux](sql-server-linux-setup-ssis.md)
-   [Limitaciones y problemas conocidos de SSIS en Linux](sql-server-linux-ssis-known-issues.md)
-   [Ejecución en Linux con cron de paquetes de programación de SQL Server Integration Services](sql-server-linux-schedule-ssis-packages.md)
