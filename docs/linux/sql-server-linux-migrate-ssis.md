---
title: Extraer, transformar y cargar datos en Linux con SSIS | Documentos de Microsoft
description: 
author: sanagama
ms.author: sanagama
manager: jhubbard
ms.date: 07/17/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 9dab69c7-73af-4340-aef0-de057356b791
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: d7317cad5aa1e77653431c128ce1549bc4349e18
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="extract-transform-and-load-data-on-linux-with-ssis"></a>Extraer, transformar y cargar datos en Linux con SSIS

[!INCLUDE[tsql-appliesto-sslinux-only](../../docs/includes/tsql-appliesto-sslinux-only.md)]

En este tema se describe cómo ejecutar paquetes de SQL Server Integration Services (SSIS) en Linux. SSIS resuelve los problemas de integración de datos complejos, cargar datos desde varios orígenes y formatos, transformar y limpiar los datos y actualizar varios destinos. 

Paquetes SSIS que se ejecutan en Linux pueden conectarse a Microsoft SQL Server que se ejecutan en Windows local o en la nube, en Linux o en Docker. También pueden conectarse a la base de datos de SQL Azure, almacenamiento de datos de SQL Azure y orígenes de datos ODBC.

Puede usar SSIS para ejecutar paquetes en Linux si también tiene un equipo de Windows para crear y mantener paquetes. Las herramientas de administración y diseño SSIS son aplicaciones de Windows. 

## <a name="prerequisites"></a>Requisitos previos

Para ejecutar paquetes SSIS en un equipo Linux, primero tiene que instalar SQL Server Integration Services. Para obtener instrucciones de instalación, consulte [instalar SQL Server Integration Services](sql-server-linux-setup-ssis.md).

## <a name="run-an-ssis-package"></a>Ejecutar un paquete SSIS

Para ejecutar un paquete SSIS en un equipo Linux, haga lo siguiente:

1.  Copie el paquete SSIS en el equipo Linux.
2.  Ejecute el siguiente comando:
    ```
    $ dtexec /F \<package name \> /DE <protection password>
    ```

## <a name="more-about-ssis-on-linux"></a>Más información acerca de SSIS en Linux

**Conexiones ODBC**. Con SSIS al actualizar los Linux CTP 2.1 y versiones posteriores, paquetes SSIS pueden usar conexiones de ODBC en Linux. Esta funcionalidad se ha probado con el servidor SQL Server y los controladores ODBC de MySQL, pero también se espera que funcione con cualquier controlador de ODBC Unicode que se ajusta a la especificación de ODBC. En tiempo de diseño, puede proporcionar un DSN o una cadena de conexión para conectarse a los datos ODBC; También puede utilizar la autenticación de Windows. Para obtener más información, consulte el [entrada del blog del anuncio de compatibilidad con ODBC en Linux](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/).

**Las rutas de acceso**. SSIS en Linux no es compatible con las rutas de acceso basado en Linux, pero las rutas de acceso de estilo de Windows asigna a las rutas de acceso de estilo de Linux en tiempo de ejecución. Proporcionar las rutas de acceso de estilo de Windows en los paquetes SSIS. A continuación, por ejemplo, SSIS en Linux asigna la ruta de acceso de estilo de Windows `C:\test` a la ruta de acceso basado en Linux `/test`.

**Implementar paquetes**. Solo puede almacenar paquetes en el sistema de archivos en Linux en esta versión. La base de datos de catálogo de SSIS y el servicio SSIS heredado no están disponibles en Linux para el almacenamiento y la implementación del paquete.

**Programar paquetes**. No se puede usar el Agente SQL en Linux para programar la ejecución de paquetes en esta versión.

**Otras limitaciones y problemas conocidos**. Las siguientes características no se admiten en esta versión, al ejecutar paquetes SSIS en Linux:
  - Base de datos de catálogo de SSIS
  - Ejecución del paquete programado por el Agente SQL
  - Autenticación de Windows
  - Componentes de terceros
  - Captura de datos modificados (CDC)
  - Ampliación SSIS
  - Feature Pack de Azure para SSIS
  - Compatibilidad con Hadoop y HDFS
  - Microsoft Connector for SAP BW

Para conocer otras limitaciones y problemas conocidos de SSIS en Linux, consulte la [notas de la versión](sql-server-linux-release-notes.md#ssis).

Para obtener más información sobre SSIS en Linux, consulte las siguientes entradas de blog:

-   [SSIS en Linux está disponible en SQL Server de 2017 CTP2.1](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/)
-   [ODBC es compatible con SSIS en Linux (actualización de CTP de SQL Server de 2017 2.1)](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)

## <a name="more-about-ssis"></a>Más información acerca de SSIS

Microsoft SQL Server Integration Services (SSIS) es una plataforma para compilar soluciones de integración de datos de alto rendimiento, incluidos los paquetes de extracción, transformación y carga (ETL) para almacenamiento de datos. Para obtener más información sobre SSIS, vea [SQL Server Integration Services](/sql/integration-services/sql-server-integration-services.md).

SSIS incluye las siguientes características:
- las herramientas gráficas y asistentes para generar y depurar paquetes en Windows
- una serie de tareas para realizar funciones de flujo de trabajo, como las operaciones de FTP, ejecutar instrucciones SQL y enviar mensajes de correo electrónico
- una variedad de orígenes de datos y destinos para extraer y cargar datos
- una gama de transformaciones para limpiar, agregar, combinar y copiar datos
- interfaces de programación de aplicaciones (API) para ampliar SSIS con sus propios scripts personalizados y componentes

Para empezar a trabajar con SSIS, descargue la versión más reciente de [SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md). A continuación, siga el tutorial [cómo SSIS para crear un paquete ETL](https://msdn.microsoft.com/en-us/library/ms169917.aspx).

## <a name="see-also"></a>Vea también
- [Obtener más información sobre SQL Server Integration Services](https://msdn.microsoft.com/en-us/library/ms141026.aspx)
- [Herramientas de administración y desarrollo de SQL Server Integration Services (SSIS)](https://msdn.microsoft.com/en-us/library/ms140028.aspx)
- [Tutoriales de SQL Server Integration Services](https://msdn.microsoft.com/en-us/library/jj720568.aspx)

