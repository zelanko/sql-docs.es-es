---
title: Configurar SSIS en Linux con ssis-conf | Documentos de Microsoft
description: "Este artículo muestra cómo configurar SQL Server Integration Services en Linux con la utilidad de ssis-conf."
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.date: 09/26/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 46327772e8c22f76770bc51f72817ceedffae469
ms.contentlocale: es-es
ms.lasthandoff: 09/27/2017

---
# <a name="configure-sql-server-integration-services-on-linux-with-ssis-conf"></a>Configurar SQL Server Integration Services en Linux con ssis-conf

`ssis-conf`es un script de configuración que es cuando instale SQL Server Integration Services (SSIS) para Red Hat Enterprise Linux y Ubuntu. Puede usar esta utilidad para configurar las siguientes propiedades:

| Command | Description |
|-------------|---------------------------------------------------------------------|
| edición de conjunto | Establecer la edición de SQL Server                                       |
| Telemetría   | Habilitar o deshabilitar el servicio de telemetría de SQL Server Integration Services |
| instalar       | Inicializar y configurar Microsoft SQL Server Integration Services      |
|||

## <a name="how-to-run-ssis-conf"></a>Cómo ejecutar conf de ssis

Los ejemplos de este artículo ejecutar `ssis-conf` al especificar la ruta de acceso completa: `/opt/ssis/bin/ssis-conf`. Si se desplaza a esa ruta de acceso antes de ejecutar `ssis-conf`, puede ejecutar la utilidad en el contexto del directorio actual: `./ssis-conf`.

Asegúrese de que ejecutar los comandos descritos en este artículo con privilegios de raíz. Por ejemplo, ejecutar `sudo /opt/ssis/bin/ssis-conf setup` y no `/opt/ssis/bin/ssis-conf setup`.

Para ejecutar estos comandos con los mensajes en el idioma que prefiera, puede especificar una configuración regional. Por ejemplo, para ver los mensajes en chino, ejecute el siguiente comando:

`sudo LC_ALL=zh_CN.UTF-8 /opt/ssis/bin/ssis-conf setup`.

## <a name="use-set-edition-to-set-the-edition-of-sql-server-integration-services"></a>Utilice Edición de conjunto para establecer la edición de SQL Server Integration Services

La edición de SSIS se alinea con la edición de SQL Server.

Escriba el comando siguiente:

`$ sudo /opt/ssis/bin/ssis-conf set-edition`

Después de escribir el comando, verá el mensaje siguiente:

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

Details about editions can be found at

https://go.microsoft.com/fwlink/?LinkId=852748&clcid=0x409

Use of PAID editions of this software requires separate licensing through a

Microsoft Volume Licensing program.

By choosing a PAID edition, you are verifying that you have the appropriate

number of licenses in place to install and run this software.

Enter your edition(1-8):
```

Si especifica un valor entre 1 y 7, el sistema configura una edición gratuita o de pagada. Si escribe 8, la utilidad le pide que escriba la clave de producto que se compraron:

```
Enter the 25-character product key:
```

## <a name="use-telemetry-to-configure-customer-feedback"></a>Use la telemetría para configurar los comentarios de clientes

El `telemetry` comando determina si SSIS envía comentarios a Microsoft.

Para las ediciones gratuitas (es decir, las ediciones Express, Developer y Evaluation), el servicio de telemetría siempre está habilitado. Si tiene una edición gratuita, no se puede usar el `telemetry` comando para deshabilitar la telemetría.

Escriba el comando siguiente:

`$ sudo /opt/ssis/bin/ssis-conf telemetry`

Las ediciones de pago, después de escribir el comando, verá el mensaje siguiente:

```
Send feature usage data to Microsoft. Feature usage data includes information
about your hardware configuration and how you use SQL Server Integration Services.

[Yes/No]:
```

Si elige **Sí**, el servicio de telemetría está habilitado y empieza a ejecutarse. El servicio automático-comienza después de cada arranque. Si elige **n**, detiene el servicio de telemetría y está deshabilitado.

## <a name="use-setup-to-initialize-and-set-up-microsoft-sql-server-integration-services"></a>Utilice el programa de instalación para inicializar y configurar Microsoft SQL Server Integration Services

Use la `setup` comando cada vez que se instala SSIS.

Escriba el comando siguiente:

`sudo /opt/ssis/bin/ssis-conf setup`

La utilidad le pedirá que confirme o para proporcionar valores para los siguientes elementos:
-   Licencia del producto
-   Acuerdo de términos de licencia
-   Servicio de telemetría
-   El idioma utilizado por Integration Services

Para ejecutar el `setup` comando con mensajes en el idioma que prefiera, puede especificar una configuración regional. Por ejemplo, para ver los mensajes en chino, ejecute el siguiente comando: `sudo LC_ALL=zh_CN.UTF-8 /opt/ssis/bin/ssis-conf setup`.

## <a name="ssisconf-format"></a>formato de SSIS.conf

El siguiente `/var/opt/ssis/ssis.conf` archivo proporciona un ejemplo para cada configuración.

Para SQL Server, puede cambiar la configuración del sistema cambiando los valores en el `mssql.conf` archivo. Para SSIS, se **no** cambiar la configuración del sistema cambiando los valores en el `ssis.conf` archivo. El `ssis.conf` archivo solo muestra los resultados del programa de instalación. Si desea cambiar la configuración de SSIS, puede eliminar el `ssis.conf` de archivos y ejecutar el `setup` comando nuevo.

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
