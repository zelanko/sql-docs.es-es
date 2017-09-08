---
title: "Importar y exportar datos con el Asistente de exportación y la importación de SQL Server | Documentos de Microsoft"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- exporting data
- mapping files [Integration Services]
- SQL Server Import and Export Wizard
- SSIS packages, creating
- packages [Integration Services], copying
- Integration Services packages, creating
- packages [Integration Services], creating
- SQL Server Integration Services packages, creating
- Import and Export Wizard
- copying data [Integration Services]
- importing data, SSIS packages
- sources [Integration Services], copying data
ms.assetid: c0e4d867-b2a9-4b2a-844b-2fe45be88f81
caps.latest.revision: 160
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2800075091835b2d6f2b07ee34e9b897fe86634e
ms.openlocfilehash: 22419ce21476588f4ff2859185c8b833306fa896
ms.contentlocale: es-es
ms.lasthandoff: 08/17/2017

---
# <a name="import-and-export-data-with-the-sql-server-import-and-export-wizard"></a>Importar y exportar datos con el Asistente para importación y exportación de SQL Server

 > Para el contenido relacionado con las versiones anteriores de SQL Server, vea [ejecutar la importación de SQL Server y el Asistente para exportación de](https://msdn.microsoft.com/en-US/library/ms140052(SQL.120).aspx).

 El Asistente para importación y exportación de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ofrece una manera sencilla de copiar datos de un origen a un destino. Esta introducción describe los orígenes de datos que el asistente pueda utilizar como orígenes y destinos, así como los permisos que necesita para ejecutar al asistente.

## <a name="get-the-wizard"></a>Obtener el Asistente
Si desea ejecutar el asistente, pero no tiene [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalado en el equipo, puede instalar el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante la instalación de SQL Server Data Tools (SSDT). Para obtener más información, vea [Descargar SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).

## <a name="what-happens-when-i-run-the-wizard"></a>¿Qué ocurre cuando ejecuta el Asistente?
-    **Ver la lista de pasos.** Para obtener una descripción de los pasos del asistente, consulte [los pasos de la importación de SQL Server y el Asistente para exportación de](../../integration-services/import-export-data/steps-in-the-sql-server-import-and-export-wizard.md). También hay una página independiente de la documentación de cada página del asistente.  
    \-o\-
-   **Ver un ejemplo sencillo.** Para obtener una visión rápida de las varias pantallas que ve en una sesión típica, eche un vistazo en este sencillo ejemplo de extremo a extremo en una sola página - [empezar a trabajar con este ejemplo sencillo de la importación y el Asistente para exportación de](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md).  

##  <a name="wizardSources"></a>¿Qué orígenes y destinos puedo usar?  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Import and Export Wizard pueden copiar datos a y desde los orígenes de datos que se muestran en la tabla siguiente. Para conectarse a algunos de estos orígenes de datos, tendrá que descargar e instalar archivos adicionales.
 
| Origen de datos | ¿Es necesario descargar archivos adicionales? |
|-------------|-----------------------------------------|
|**Bases de datos empresariales**<br/>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Oracle, DB2 y otros usuarios.|SQL Server o SQL Server Data Tools (SSDT) instala los archivos que necesita para conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Pero SSDT no lo instala todos los archivos que necesita para conectarse a otras bases de datos empresariales, como Oracle o IBM DB2.<br/><br/>Para conectarse a una base de datos de empresa, normalmente deberá tener dos cosas:<br/><br/>1. **Software de cliente**. Si ya tiene el software cliente instalado en el sistema de base de datos empresarial, por lo general ya dispone de lo necesario para establecer una conexión. Si no tiene instalado el software cliente, consulte al administrador de base de datos cómo instalar una copia con licencia.<br/><br/>2. **Controladores o proveedores**. Microsoft instala controladores y proveedores para conectar con Oracle. Para conectarse a IBM DB2, obtener el proveedor Microsoft® OLE DB para DB2 v5.0 para Microsoft SQL Server desde el [Microsoft SQL Server 2016 Feature Pack](https://www.microsoft.com/download/details.aspx?id=52676).|
|**Archivos de texto** (archivos planos)|No se necesitan archivos adicionales.|
|**Archivos de Microsoft Excel y Microsoft Access**|Microsoft Office no instala todos los archivos que necesita para conectarse a archivos de Excel y Access como orígenes de datos. Obtenga la descarga siguiente - [redistribuible de 2016 de motor de base de datos Microsoft acceso](https://www.microsoft.com/download/details.aspx?id=54920).<br/><br/>Para obtener más información, consulte [conectar a un origen de datos de Excel](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md) o [conectarse a un origen de datos de Access](../../integration-services/import-export-data/connect-to-an-access-data-source-sql-server-import-and-export-wizard.md).|
|**Orígenes de datos de Azure**<br/>Actualmente, solo Almacenamiento de blobs de Azure.|SQL Server Data Tools no instalar los archivos que necesita para conectarse al almacenamiento de blobs de Azure como un origen de datos. Obtenga la descarga siguiente: [Microsoft SQL Server 2016 Integration Services Feature Pack for Azure](https://www.microsoft.com/download/details.aspx?id=49492)(Feature Pack de Microsoft SQL Server 2016 Integration Services para Azure).<br/><br/>Para obtener más información, consulte [conectar al almacenamiento de blobs de Azure](../../integration-services/import-export-data/connect-to-azure-blob-storage-sql-server-import-and-export-wizard.md).|
|**Bases de datos de código abierto**<br/>PostgreSQL, MySql u otros datos.|Tiene que descargar archivos adicionales para conectarse a estos orígenes de datos.<br/><br/>-Para **PostgreSQL**, consulte [conectarse a un origen de datos de PostgreSQL](../../integration-services/import-export-data/connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard.md).<br/>-Para **MySql**, consulte [conectarse a un origen de datos de MySQL](../../integration-services/import-export-data/connect-to-a-mysql-data-source-sql-server-import-and-export-wizard.md).|
|**Cualquier otro origen de datos para el que un proveedor o controlador está disponible**|Normalmente tiene que descargar archivos adicionales para conectarse a los siguientes tipos de orígenes de datos.<br/><br/>- Cualquier origen para el que esté disponible un **controlador ODBC** . Para obtener más información, consulte [conectar a un origen de datos ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md).<br/>- Cualquier origen para el que esté disponible un **proveedor de datos .NET Framework** .<br/>- Cualquier origen para el que esté disponible un **proveedor OLE DB** .<br/><br/>Componentes de terceros que proporcionan capacidades de origen y destino para otros orígenes de datos a veces se comercializan como productos complementarios para SQL Server Integration Services (SSIS).|

## <a name="how-do-i-connect-to-my-data"></a>¿Cómo conecto a Mis datos?
Para obtener información sobre cómo conectarse a un origen de datos de uso frecuente, consulte una de las páginas siguientes.
-   [Conectarse a SQL Server](../../integration-services/import-export-data/connect-to-a-sql-server-data-source-sql-server-import-and-export-wizard.md)
-   [Conectar con Oracle](../../integration-services/import-export-data/connect-to-an-oracle-data-source-sql-server-import-and-export-wizard.md)
-   [Conectarse a los archivos sin formato (archivos de texto)](../../integration-services/import-export-data/connect-to-a-flat-file-data-source-sql-server-import-and-export-wizard.md)
-   [Conectarse a Excel](../../integration-services/import-export-data/connect-to-an-excel-data-source-sql-server-import-and-export-wizard.md)
-   [Conectar con Access](../../integration-services/import-export-data/connect-to-an-access-data-source-sql-server-import-and-export-wizard.md)
-   [Conectarse al almacenamiento de blobs de Azure](../../integration-services/import-export-data/connect-to-azure-blob-storage-sql-server-import-and-export-wizard.md)
-   [Conectar con ODBC](../../integration-services/import-export-data/connect-to-an-odbc-data-source-sql-server-import-and-export-wizard.md)
-   [Conectarse a PostgreSQL](../../integration-services/import-export-data/connect-to-a-postgresql-data-source-sql-server-import-and-export-wizard.md)
-   [Conectarse a MySQL](../../integration-services/import-export-data/connect-to-a-mysql-data-source-sql-server-import-and-export-wizard.md)


Para obtener información sobre cómo conectarse a un origen de datos que no aparece aquí, consulte [la referencia de las cadenas de conexión](https://www.connectionstrings.com/). Este sitio de terceros contiene las cadenas de conexión de ejemplo y obtener más información acerca de los proveedores de datos y la información de conexión que se necesiten.

## <a name="what-permissions-do-i-need"></a>¿Qué permisos necesito?  
 Para ejecutar correctamente el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , debe disponer como mínimo de los siguientes permisos. Si ya trabaja con el origen y el destino de datos, probablemente cuente con los permisos necesarios.
  
|Necesita permisos para estas acciones|Si se está conectando a SQL Server, necesita estos permisos específicos |  
|-------------------------|----------------------------------------------------|  
|Conectarse a las bases de datos o recursos compartidos de archivos de origen y de destino.|Derechos de inicio de sesión del servidor y de la base de datos.|  
|Exportar o leer datos desde la base de datos o el archivo de origen.|Permisos SELECT en las tablas y vistas de origen.|  
|Importar o escribir datos en la base de datos o el archivo de destino.|Permisos INSERT en las tablas de destino.|  
|Crear la base de datos o el archivo de destino, si procede.|Permisos CREATE DATABASE o CREATE TABLE.|  
|Guardar el paquete SSIS creado por el asistente, si procede.|Si quiere guardar el paquete en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], permisos suficientes para guardar el paquete en la base de datos **msdb** .|  
  
## <a name="get-help-while-the-wizard-is-running"></a>Obtener ayuda mientras se ejecuta el Asistente
> [!TIP]
> Pulse la tecla F1 en cualquier página o cuadro de diálogo del Asistente para ver la documentación de la página actual.   
  
##  <a name="wizardSSIS"></a> El asistente usa SQL Server Integration Services (SSIS)  
 El asistente usa SQL Server Integration Services (SSIS) para copiar datos. SSIS es una herramienta para la extracción, transformación y carga (ETL) de datos. Las páginas del asistente usan parte del idioma de SSIS.
  
 En SSIS, la unidad básica es el **paquete**. El asistente crea un paquete SSIS en la memoria a medida que se desplaza por las páginas del asistente y especifica las opciones.    
  
Al final del asistente, si tiene instalado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard Edition o una versión superior, puede guardar el paquete de SSIS. Después podrá volver a usar el paquete o ampliarlo usando el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] para agregar tareas, transformaciones y lógica controlada por eventos. El Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ofrece la manera más simple para crear un paquete básico de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que copia datos de un origen en un destino.

Para obtener más información sobre SSIS, vea [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md).

## <a name="whats-next"></a>Siguientes pasos  
 Inicie el asistente. Para obtener más información, vea [Start the SQL Server Import and Export Wizard](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md)(Iniciar el Asistente para importación y exportación de SQL Server).  

## <a name="see-also"></a>Vea también
[Comenzar con este sencillo ejemplo del Asistente para importar y exportar](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)  
[Asignación de tipos de datos en el Asistente para importación y exportación de SQL Server](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)



