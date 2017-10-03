---
title: Extraer, transformar y cargar datos en Linux con SSIS | Documentos de Microsoft
description: 
author: leolimsft
ms.author: lle
ms.reviewer: douglasl
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 9dab69c7-73af-4340-aef0-de057356b791
ms.translationtype: MT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: aa4ac0cca739ea57a28beb399325d55b38502217
ms.contentlocale: es-es
ms.lasthandoff: 10/02/2017

---
# <a name="extract-transform-and-load-data-on-linux-with-ssis"></a>Extraer, transformar y cargar datos en Linux con SSIS

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

En este tema se describe cómo ejecutar paquetes de SQL Server Integration Services (SSIS) en Linux. SSIS permite solucionar problemas de integración de datos complejos, extraer datos de varios orígenes y formatos, transformar y limpiar los datos y cargar los datos en varios destinos. 

Paquetes SSIS que se ejecutan en Linux pueden conectarse a Microsoft SQL Server que se ejecutan en Windows local o en la nube, en Linux o en Docker. También pueden conectarse a la base de datos de SQL Azure, almacenamiento de datos de SQL Azure, orígenes de datos ODBC, archivos sin formato y otros orígenes de datos, incluidos los orígenes ADO.NET, archivos XML y los servicios OData.

Para obtener más información acerca de las capacidades de SSIS, vea [SQL Server Integration Services](../integration-services/sql-server-integration-services.md).

## <a name="prerequisites"></a>Requisitos previos

Para ejecutar paquetes SSIS en un equipo Linux, primero tiene que instalar SQL Server Integration Services. SSIS no se incluye en la instalación de SQL Server para los equipos de Linux. Para obtener instrucciones de instalación, consulte [instalar SQL Server Integration Services](sql-server-linux-setup-ssis.md).

También deben tener un equipo de Windows para crear y mantener paquetes. Las herramientas de administración y diseño SSIS son aplicaciones de Windows que no están disponibles actualmente para equipos Linux. 

## <a name="run-an-ssis-package"></a>Ejecutar un paquete SSIS

Para ejecutar un paquete SSIS en un equipo Linux, haga lo siguiente:

1.  Copie el paquete SSIS en el equipo Linux.
2.  Ejecute el siguiente comando:
    ```
    $ dtexec /F \<package name \> /DE <protection password>
    ```

## <a name="other-common-ssis-tasks"></a>Otras tareas habituales de SSIS

-   **Diseñar paquetes**.

    -   **Conectarse a orígenes de datos ODBC**. Con SSIS al actualizar los Linux CTP 2.1 y versiones posteriores, paquetes SSIS pueden usar conexiones de ODBC en Linux. Esta funcionalidad se ha probado con el servidor SQL Server y los controladores ODBC de MySQL, pero también se espera que funcione con cualquier controlador de ODBC Unicode que se ajusta a la especificación de ODBC. En tiempo de diseño, puede proporcionar un DSN o una cadena de conexión para conectarse a los datos ODBC; También puede utilizar la autenticación de Windows. Para obtener más información, consulte el [entrada del blog del anuncio de compatibilidad con ODBC en Linux](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/).

    -   **Las rutas de acceso**. Proporcionar las rutas de acceso de estilo de Windows en los paquetes SSIS. SSIS en Linux no es compatible con las rutas de acceso basado en Linux, pero las rutas de acceso de estilo de Windows asigna a las rutas de acceso de estilo de Linux en tiempo de ejecución. A continuación, por ejemplo, SSIS en Linux asigna la ruta de acceso de estilo de Windows `C:\test` a la ruta de acceso basado en Linux `/test`.

-   **Implementar paquetes**. Solo puede almacenar paquetes en el sistema de archivos en Linux en esta versión. La base de datos de catálogo de SSIS y el servicio SSIS heredado no están disponibles en Linux para el almacenamiento y la implementación del paquete.

-   **Programar paquetes**. Puede utilizar el sistema de Linux, como las herramientas de programación `cron` para programar paquetes. No se puede usar el Agente SQL en Linux para programar la ejecución de paquetes en esta versión. Para obtener más información, consulte [paquetes SSIS de programación en Linux con cron](sql-server-linux-schedule-ssis-packages.md).

## <a name="limitations-and-known-issues"></a>Limitaciones y problemas conocidos

### <a name="general-limitations-and-known-issues"></a>Tiene las limitaciones y problemas conocidos

Las siguientes características no se admiten en esta versión de SSIS en Linux:
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

### <a name="components"></a>Componentes admitidos y no admitidos

Se admiten los siguientes componentes de Integration Services integrados en Linux. Algunos de ellos tienen limitaciones en la plataforma de Linux, tal como se describe en las tablas siguientes.

Componentes integrados que no se muestran aquí no se admiten en Linux.

#### <a name="supported-control-flow-tasks"></a>Admite tareas de flujo de control
- Inserción masiva, tarea
- Tarea Flujo de datos
- Tarea de generación de perfiles de datos
- Tarea Ejecutar SQL
- Tarea Ejecutar instrucción T-SQL
- Texto Expresión
- Tarea FTP
- Tarea Servicio web
- Tarea XML

#### <a name="control-flow-tasks-supported-with-limitations"></a>Tareas de flujo de control compatibles con limitaciones

| Tarea | Limitaciones |
|------------|---|
| Tarea Ejecutar proceso | Solo es compatible con el modo en proceso. |
| Tarea sistema de archivos | El *mover directorio* y *establecer atributos de archivo* no se admiten las acciones. |
| tarea Script | Solo es compatible con API estándar de .NET Framework. |
| Enviar correo, tarea | Solo admite el modo de usuario anónimo. |
| Tarea de transferencia de base de datos | No se admiten las rutas de acceso UNC. |
| | |

#### <a name="supported-control-flow-containers"></a>Admite contenedores de flujo de control
- contenedor de secuencias
- Contenedor de bucles For
- Contenedor Foreach Loop

#### <a name="supported-data-flow-sources-and-destinations"></a>Orígenes de flujo de datos admitidos y los destinos
- Destino y origen de archivo sin formato
- Origen XML

#### <a name="data-flow-sources-and-destinations-supported-with-limitations"></a>Orígenes de flujo de datos y destinos compatibles con limitaciones

| Componente | Limitaciones |
|------------|---|
| ADO.NET, origen y destino | Solo se admite el proveedor de datos SQLClient. |
| Destino y origen de archivo plano | Solo se admiten rutas de acceso de archivo de estilo de Windows, al que se aplica la regla de asignación de ruta de acceso predeterminada. Por ejemplo `D:\home\ssis\travel.csv` se convierte en `/home/ssis/travel.csv`. |
| Origen OData | Solo se admite la autenticación básica. |
| Destino y origen de ODBC | Es compatible con controladores de 64 bits Unicode ODBC en Linux. Depende del Administrador de controladores UnixODBC en Linux. |
| Destino y origen de OLE DB | Solo se admiten SQL Server Native Client 11.0 y proveedor Microsoft OLE DB para SQL Server. |
| | |

#### <a name="supported-data-flow-transformations"></a>Admite las transformaciones de flujo de datos
- Agregado
- Auditar
- Balanced Data Distributor
- Mapa de caracteres
- División condicional
- Copiar columna
- Conversión de datos
- Columna derivada
- Exportar columna
- agrupación aproximada
- Búsqueda aproximada
- Importar columna
- Lookup
- Mezcla
- Merge Join
- Multidifusión
- Dinamización
- Recuento de filas
- Dimensión de variación lenta
- Sort
- Búsqueda de términos
- Unión de todo
- Anulación de dinamización

#### <a name="data-flow-transformations-supported-with-limitations"></a>Transformaciones de flujo de datos compatibles con limitaciones

| Componente | Limitaciones |
|------------|---|
| transformación Comando de OLE DB | Mismas limitaciones que el origen de OLE DB y el destino. |
| componente de script | Solo es compatible con API estándar de .NET Framework. |
| | |

### <a name="supported-and-unsupported-log-providers"></a>Proveedores de registro compatibles y no compatibles
Todos los proveedores de registro SSIS integrados se admiten en Linux excepto el proveedor de registro de eventos de Windows.

El proveedor de registro de SQL Server admite únicamente la autenticación de SQL; no admite la autenticación de Windows.

Los proveedores de registro SSIS para archivos de texto, para los archivos XML y de SQL Server Profiler escriben sus resultados a un archivo que especifique. Las consideraciones siguientes se aplican a la ruta de acceso de archivo:
-   Si no proporciona una ruta de acceso, el proveedor de registro se escribe en el directorio actual del host. Si el usuario actual no tiene permiso para escribir en el directorio actual del host, el proveedor de registro genera un error.
-   No se puede usar una variable de entorno en una ruta de acceso de archivo. Si especifica una variable de entorno, aparece el texto literal que se especifique en la ruta de acceso de archivo. Por ejemplo, si especifica `%TMP%/log.txt`, el proveedor de registro anexa el texto literal `/%TMP%/log.txt` en el directorio actual del host.

## <a name="more-info-about-ssis-on-linux"></a>Para obtener más información acerca de SSIS en Linux

Para obtener más información sobre SSIS en Linux, consulte las siguientes entradas de blog:

-   [SSIS en Linux está disponible en SQL Server de 2017 CTP2.1](https://blogs.msdn.microsoft.com/ssis/2017/05/17/ssis-helsinki-is-available-in-sql-server-vnext-ctp2-1/)
-   [ODBC es compatible con SSIS en Linux (actualización de CTP de SQL Server de 2017 2.1)](https://blogs.msdn.microsoft.com/ssis/2017/06/16/odbc-is-supported-in-ssis-on-linux-ssis-helsinki-ctp2-1-refresh/)

## <a name="more-info-about-ssis"></a>Para obtener más información acerca de SSIS

Microsoft SQL Server Integration Services (SSIS) es una plataforma para compilar soluciones de integración de datos de alto rendimiento, incluidos los paquetes de extracción, transformación y carga (ETL) para almacenamiento de datos. Para obtener más información sobre SSIS, vea [SQL Server Integration Services](/sql/integration-services/sql-server-integration-services.md).

SSIS incluye las siguientes características:
- las herramientas gráficas y asistentes para generar y depurar paquetes en Windows
- una serie de tareas para realizar funciones de flujo de trabajo, como las operaciones de FTP, ejecutar instrucciones SQL y enviar mensajes de correo electrónico
- una variedad de orígenes de datos y destinos para extraer y cargar datos
- una gama de transformaciones para limpiar, agregar, combinar y copiar datos
- interfaces de programación de aplicaciones (API) para ampliar SSIS con sus propios scripts personalizados y componentes

Para empezar a trabajar con SSIS, descargue la versión más reciente de [SQL Server Data Tools (SSDT)](../integration-services/ssis-how-to-create-an-etl-package.md).

## <a name="see-also"></a>Vea también
- [Obtener más información sobre SQL Server Integration Services](../integration-services/sql-server-integration-services.md)
- [Herramientas de administración y desarrollo de SQL Server Integration Services (SSIS)](../integration-services/integration-services-ssis-development-and-management-tools.md)
- [Tutoriales de SQL Server Integration Services](../integration-services/integration-services-tutorials.md)

