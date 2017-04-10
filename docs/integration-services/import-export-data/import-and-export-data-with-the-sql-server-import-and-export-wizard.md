---
title: "Importar y exportar datos con el Asistente para importaci&#243;n y exportaci&#243;n de SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "exportar datos"
  - "asignar archivos [Integration Services]"
  - "Asistente para importación y exportación de SQL Server"
  - "paquetes SSIS, creación"
  - "paquetes [Integration Services], copia"
  - "paquetes de Integration Services, creación"
  - "paquetes [Integration Services], creación"
  - "paquetes de SQL Server Integration Services, creación"
  - "Asistente para importación y exportación"
  - "copiar datos [Integration Services]"
  - "importar datos, paquetes SSIS"
  - "orígenes [Integration Services], copia de datos"
ms.assetid: c0e4d867-b2a9-4b2a-844b-2fe45be88f81
caps.latest.revision: 160
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 134
---
# Importar y exportar datos con el Asistente para importaci&#243;n y exportaci&#243;n de SQL Server
 El Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ofrece una manera sencilla de copiar datos de un origen a un destino. No es necesario tener SQL Server instalado para ejecutar el asistente. En esta visión general se describen los orígenes de datos que admiten la importación o exportación de datos mediante el auxiliar, así como los permisos necesarios para ejecutarlo.

En este tema se proporciona solo una **introducción** al asistente.
-   Si está listo para ejecutar el asistente y simplemente quiere saber cómo iniciarlo, consulte [Iniciar el Asistente para importación y exportación de SQL Server](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md).
-   Si quiere obtener información acerca de los pasos del asistente, seleccione la página correspondiente en el menú de navegación de contenido. Hay una página independiente de documentación para cada página del asistente. O pulse la tecla F1 en cualquier página o cuadro de diálogo del asistente para ver la documentación de la página actual.

**Obtenga el asistente**. Si desea ejecutar el asistente, pero no tiene [!INCLUDE[msCoName] (../Token/msCoName_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instalado en el equipo, puede instalar el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante la instalación de SQL Server Data Tools (SSDT). Para obtener más información, vea [Descargar SQL Server Data Tools (SSDT)](https://msdn.microsoft.com/library/mt204009.aspx).

> [!TIP] Si tiene que copiar más de una base de datos u objetos de base de datos que no sean tablas y vistas, use al Asistente para copiar bases de datos en lugar del Asistente para importación y exportación. Para más información, vea [Usar el Asistente para copiar bases de datos](../../relational-databases/databases/use-the-copy-database-wizard.md).

## <a name="example-of-a-common-use-case---exporting-data-to-excel-video"></a>Ejemplo de un caso de uso común: Exportar datos a Excel (vídeo)  
Un uso común del asistente es exportar datos a Excel. Aquí tiene un vídeo de cuatro minutos de YouTube en que se muestra el asistente y se explica cómo realizarlo, con instrucciones claras y sencillas: [Using the SQL Server Import and Export Wizard to Export to Excel](https://go.microsoft.com/fwlink/?linkid=829049) (Usar el Asistente para importación y exportación de SQL Server para exportar a Excel).

##  <a name="a-namewizardsourcesa-what-data-sources-and-destinations-can-i-use"></a><a name="wizardSources"></a> ¿Qué orígenes y destinos de datos puedo usar?  
 El Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede copiar datos en los orígenes de datos siguientes. Para usar algunos de estos orígenes de datos, quizá necesite descargar e instalar archivos adicionales.

| Origen de datos | ¿Es necesario descargar archivos adicionales? |
|-------------|-----------------------------------------|
|**Bases de datos empresariales**<br/>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Oracle y otros.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instala los archivos que necesita para conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y Oracle, pero no instala los archivos que necesita para conectarse a otras bases de datos empresariales, como IBM DB2 o Informix.<br/>- Si ya tiene el software cliente instalado en el sistema de base de datos empresarial, por lo general ya dispone de lo necesario para establecer una conexión.<br/>- Si no tiene instalado el software cliente, pregúntele al administrador de base de datos cómo instalar una copia con licencia.|
|**Bases de datos de código abierto**<br/>MySql, PostgreSQL, SQLite y otros.|Tiene que descargar archivos adicionales para conectarse a estos orígenes de datos.<br/><br/>- Para **MySql**, consulte [MySQL Connectors](http://dev.mysql.com/downloads/connector/) (Conectores MySQL).<br/>- Para **PostgreSQL**, consulte [psqlODBC - PostgreSQL ODBC driver](https://odbc.postgresql.org/) (psqlODBC: controlador ODBC de PostgreSQL) y productos de terceros como [Npgsql - .NET Data Provider for PostgreSQL](http://www.npgsql.org/) (Npgsql: proveedor de datos .NET para PostgreSQL).<br/>- Para **SQLite**, seleccione entre varios proveedores y controladores de código abierto disponibles en línea.|
|**Archivos de texto** (archivos planos)|No se necesitan archivos adicionales.|
|**Archivos de Microsoft Excel y Microsoft Access**|Microsoft Office no instala todos los archivos que necesita para conectarse a archivos de Excel y Access como orígenes de datos. Obtenga la descarga siguiente: [Microsoft Access 2016 Runtime](https://www.microsoft.com/download/details.aspx?id=50040).|
|**Orígenes de datos de Azure**<br/>Actualmente, solo Almacenamiento de blobs de Azure.|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no instala los archivos que necesita para conectarse a Almacenamiento de blobs de Azure como origen de datos. Obtenga la descarga siguiente: [Microsoft SQL Server 2016 Integration Services Feature Pack for Azure](https://www.microsoft.com/download/details.aspx?id=49492) (Feature Pack de Microsoft SQL Server 2016 Integration Services para Azure).|
|**Cualquier otro origen de datos para el que esté disponible un conector**|Normalmente tiene que descargar archivos adicionales para conectarse a los siguientes tipos de orígenes de datos.<br/><br/>- Cualquier origen para el que esté disponible un **controlador ODBC**. Establezca una conexión ODBC (Conectividad abierta de bases de datos). Para ello, seleccione el proveedor de .NET Framework para ODBC en la página del asistente **Seleccionar un origen de datos** o **Seleccionar un destino** y, después, proporcione una cadena de conexión o un DSN (nombre de origen de datos) existente que haga referencia al controlador ODBC.<br/>- Cualquier origen para el que esté disponible un **proveedor OLE DB**.<br/>- Cualquier origen para el que esté disponible un **proveedor de datos .NET Framework**.<br/>- Otros orígenes de datos para los que las funcionalidades de origen y de destino se proporcionen mediante **componentes de terceros**. Normalmente estos productos de terceros se comercializan como productos complementarios para SQL Server Integration Services (SSIS).|
  
> [!TIP] Si su origen de datos necesita una cadena de conexión, encontrará ejemplos en este sitio de terceros: [The Connection Strings Reference](https://www.connectionstrings.com/) (Referencia de Connection Strings).  
  
## <a name="what-permissions-do-i-need-to-run-the-wizard"></a>¿Qué permisos necesito para ejecutar el asistente?  
 Para ejecutar correctamente el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], debe disponer como mínimo de los siguientes permisos. Si ya trabaja con el origen y el destino de datos, probablemente cuente con los permisos necesarios.
  
|Necesita permisos para estas acciones|Si se conecta a SQL Server, necesita estos permisos: |  
|-------------------------|----------------------------------------------------|  
|Conectarse a las bases de datos o recursos compartidos de archivos de origen y de destino.|Derechos de inicio de sesión del servidor y de la base de datos.|  
|Exportar o leer datos desde la base de datos o el archivo de origen.|Permisos SELECT en las tablas y vistas de origen.|  
|Importar o escribir datos en la base de datos o el archivo de destino.|Permisos INSERT en las tablas de destino.|  
|Crear la base de datos o el archivo de destino, si procede.|Permisos CREATE DATABASE o CREATE TABLE.|  
|Guardar el paquete SSIS creado por el asistente, si procede.|Si quiere guardar el paquete en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], permisos suficientes para guardar el paquete en la base de datos **msdb**.|  
  
##  <a name="a-namewizardssisa-the-wizard-uses-sql-server-integration-services-ssis"></a><a name="wizardSSIS"></a> El asistente usa SQL Server Integration Services (SSIS)  
 El asistente usa SQL Server Integration Services (SSIS) para copiar datos. SSIS es una herramienta para la extracción, transformación y carga (ETL) de datos. Las páginas del asistente usan parte del idioma de SSIS.
  
 En SSIS, la unidad básica es el **paquete**. El asistente crea un paquete SSIS en la memoria a medida que se desplaza por las páginas del asistente y especifica las opciones.    
  
Al final del asistente, si tiene instalado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard Edition o una versión superior, puede guardar el paquete de SSIS. Después podrá volver a usar el paquete o ampliarlo usando el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] para agregar tareas, transformaciones y lógica controlada por eventos. El Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ofrece la manera más simple para crear un paquete básico de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que copia datos de un origen en un destino.

Para obtener más información sobre SSIS, vea [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md).

## <a name="get-help-while-the-wizard-is-running"></a>Obtener ayuda mientras se ejecuta el Asistente
> [!TIP] Pulse la tecla F1 en cualquier página o cuadro de diálogo del Asistente para ver la documentación de la página actual.   
  
## <a name="whats-next"></a>Siguientes pasos  
 Inicie el asistente. Para obtener más información, vea [Start the SQL Server Import and Export Wizard](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md) (Iniciar el Asistente para importación y exportación de SQL Server).  
  
## <a name="see-also"></a>Vea también
[Asignación de tipos de datos en el Asistente para importación y exportación de SQL Server](../../integration-services/import-export-data/data-type-mapping-in-the-sql-server-import-and-export-wizard.md)
