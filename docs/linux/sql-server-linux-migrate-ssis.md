---
title: Extraer, transformar y cargar datos en Linux con SSIS | Microsoft Docs
description: Este artículo se describe SQL Server Integration Services (SSIS) para equipos Linux
author: leolimsft
ms.author: lle
ms.reviewer: douglasl
manager: craigg
ms.date: 01/09/2018
ms.topic: conceptual
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: d01a53524bf03e0ea8318c41b05b9cc59499de33
ms.sourcegitcommit: b7fd118a70a5da9bff25719a3d520ce993ea9def
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/24/2018
ms.locfileid: "46713227"
---
# <a name="extract-transform-and-load-data-on-linux-with-ssis"></a>Extraer, transformar y cargar datos en Linux con SSIS

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

En este artículo se describe cómo ejecutar paquetes de SQL Server Integration Services (SSIS) en Linux. SSIS soluciona los problemas de integración de datos complejos mediante la extracción de datos de varios orígenes y formatos, transformación y limpieza de los datos y cargar los datos en varios destinos. 

Paquetes SSIS que se ejecutan en Linux pueden conectarse a Microsoft SQL Server en ejecución en Windows local o en la nube, en Linux o en Docker. También pueden conectarse a Azure SQL Database, Azure SQL Data Warehouse, orígenes de datos ODBC, archivos sin formato y otros orígenes de datos, incluidos los orígenes ADO.NET, los archivos XML y servicios de OData.

Para obtener más información acerca de las capacidades de SSIS, vea [SQL Server Integration Services](../integration-services/sql-server-integration-services.md).

## <a name="prerequisites"></a>Requisitos previos

Para ejecutar paquetes SSIS en un equipo Linux, primero tiene que instalar SQL Server Integration Services. SSIS no se incluye en la instalación de SQL Server para equipos Linux. Para obtener instrucciones de instalación, consulte [instalar SQL Server Integration Services](sql-server-linux-setup-ssis.md).

También debe tener un equipo de Windows para crear y mantener paquetes. Las herramientas de administración y diseño SSIS son aplicaciones de Windows que no están disponibles actualmente para equipos Linux. 

## <a name="run-an-ssis-package"></a>Ejecutar un paquete SSIS

Para ejecutar un paquete SSIS en un equipo Linux, realice lo siguiente:

1.  Copie el paquete SSIS en el equipo Linux.
2.  Ejecute el siguiente comando:
    ```
    $ dtexec /F \<package name \> /DE <protection password>
    ```

## <a name="run-an-encrypted-password-protected-package"></a>Ejecutar un paquete cifrado (protegido con contraseña)
Hay tres maneras de ejecutar un paquete SSIS que se cifra con una contraseña:

1.  Establezca el valor de la variable de entorno `SSIS_PACKAGE_DECRYPT`, como se muestra en el ejemplo siguiente:

    ```
    SSIS_PACKAGE_DECRYPT=test /opt/ssis/bin/dtexec /f package.dtsx
    ```

2.  Especifique el `/de[crypt]` opción para escribir la contraseña de forma interactiva, tal como se muestra en el ejemplo siguiente:

    ```
    /opt/ssis/bin/dtexec /f package.dtsx /de
    
    Enter decryption password:
    ```

3.  Especifique el `/de` opción para proporcionar la contraseña en la línea de comandos, tal como se muestra en el ejemplo siguiente. Este método no se recomienda ya que almacena la contraseña de descifrado con el comando del historial de comandos.

    ```
    opt/ssis/bin/dtexec /f package.dtsx /de test
    
    Warning: Using /De[crypt] <password> may store decryption password in command history.
    
    You can use /De[crypt] instead to enter interactive mode,
    or use environment variable SSIS_PACKAGE_DECRYPT to set decryption password.
    ```

## <a name="design-packages"></a>Diseñar paquetes

**Conectarse a orígenes de datos ODBC**. Con SSIS en la actualización de Linux CTP 2.1 y versiones posteriores, los paquetes SSIS pueden usar conexiones de ODBC en Linux. Esta funcionalidad se ha probado con el servidor SQL Server y los controladores ODBC de MySQL, pero también se espera que funcione con cualquier controlador ODBC Unicode que cumple la especificación de ODBC. En tiempo de diseño, puede proporcionar un DSN o una cadena de conexión para conectarse a los datos ODBC; También puede usar la autenticación de Windows. Para obtener más información, consulte el [entrada de blog de anuncio de compatibilidad con ODBC en Linux](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/).

**Las rutas de acceso**. Proporcionar las rutas de acceso de estilo de Windows en los paquetes SSIS. SSIS en Linux no admite rutas de acceso basado en Linux, pero las rutas de acceso de estilo de Windows asigna a las rutas de acceso basado en Linux en tiempo de ejecución. A continuación, por ejemplo, SSIS en Linux asigna la ruta de acceso de estilo Windows `C:\test` a la ruta de acceso basado en Linux `/test`.

## <a name="deploy-packages"></a>Implementar paquetes
Solo puede almacenar paquetes en el sistema de archivos en Linux en esta versión. La base de datos del catálogo de SSIS y el servicio SSIS heredado no están disponibles en Linux para el almacenamiento y la implementación del paquete.

## <a name="schedule-packages"></a>Programar paquetes
Puede usar las herramientas de programación, como el sistema de Linux `cron` para programar paquetes. No puede usar para programar la ejecución del paquete en esta versión del Agente SQL en Linux. Para obtener más información, consulte [paquetes de SSIS de programación en Linux con cron](sql-server-linux-schedule-ssis-packages.md).

## <a name="limitations-and-known-issues"></a>Limitaciones y problemas conocidos

Para obtener información detallada sobre las limitaciones y problemas conocidos de SSIS en Linux, consulte [limitaciones y problemas conocidos de SSIS en Linux](sql-server-linux-ssis-known-issues.md).

## <a name="more-info-about-ssis-on-linux"></a>Obtener más información sobre SSIS en Linux

Para obtener más información acerca de SSIS en Linux, consulte las siguientes entradas de blog:

-   [SSIS en Linux está disponible en SQL Server CTP2.1](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/)
-   [SSIS en Linux (actualización de SQL Server CTP 2.1) es compatible con ODBC](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)

## <a name="more-info-about-ssis"></a>Obtener más información sobre SSIS

Microsoft SQL Server Integration Services (SSIS) es una plataforma para compilar soluciones de integración de datos de alto rendimiento, incluidos los paquetes de extracción, transformación y carga (ETL) para el almacenamiento de datos. Para obtener más información sobre SSIS, vea [SQL Server Integration Services](/sql/integration-services/sql-server-integration-services).

SSIS incluye las siguientes características:
- Las herramientas gráficas y asistentes para generar y depurar paquetes en Windows
- Una serie de tareas para realizar funciones de flujo de trabajo, como operaciones de FTP, ejecutar instrucciones SQL y enviar mensajes de correo electrónico
- Una variedad de orígenes de datos y destinos para extraer y cargar datos
- Una variedad de transformaciones para limpiar, agregar, combinar y copiar datos
- (API) de interfaces de programación de aplicaciones para ampliar SSIS con sus propios scripts personalizados y componentes

Para empezar a trabajar con SSIS, descargue la versión más reciente de [SQL Server Data Tools (SSDT)](../integration-services/ssis-how-to-create-an-etl-package.md).

Para obtener más información sobre SSIS, consulte los artículos siguientes:
- [Más información sobre SQL Server Integration Services](../integration-services/sql-server-integration-services.md)
- [Herramientas de administración y desarrollo de SQL Server Integration Services (SSIS)](../integration-services/integration-services-ssis-development-and-management-tools.md)
- [Tutoriales de SQL Server Integration Services](../integration-services/integration-services-tutorials.md)

## <a name="related-content-about-ssis-on-linux"></a>Contenido relacionado sobre SSIS en Linux
-   [Instalar SQL Server Integration Services (SSIS) en Linux](sql-server-linux-setup-ssis.md)
-   [Configurar SQL Server Integration Services en Linux con ssis-conf](sql-server-linux-configure-ssis.md)
-   [Limitaciones y problemas conocidos de SSIS en Linux](sql-server-linux-ssis-known-issues.md)
-   [Ejecución en Linux con cron de paquetes de programación de SQL Server Integration Services](sql-server-linux-schedule-ssis-packages.md)
