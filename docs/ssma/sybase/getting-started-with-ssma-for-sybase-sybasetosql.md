---
title: Introducción a SSMA para SAP ASE (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/30/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: c4098516-f0fc-4690-97bb-3766dfd43156
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 7e308589ab565b5702bbf2cba939835a50c08d8e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63126657"
---
# <a name="getting-started-with-ssma-for-sap-ase-sybasetosql"></a>Introducción a SSMA para SAP ASE (SybaseToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant (SSMA) para SAP ASE permite rápidamente convertir esquemas de base de datos de SAP Adaptive Server Enterprise (ASE) para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o esquemas de base de datos de SQL Azure, cargue los esquemas resultantes a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL Database, y migrar datos desde SAP ASE [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL Database.  
  
En este tema presenta el proceso de instalación y, a continuación, le ayuda a familiarizarse con la interfaz de usuario SSMA.  
  
## <a name="installing-and-licensing-ssma"></a>Instalación y la licencia de SSMA  
Para usar SSMA, primero debe instalar el programa de cliente SSMA en un equipo que puede tener acceso a la instancia de origen de SAP ASE tanto la instancia de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL Database. Para usar la migración de datos del servidor, debe instalar el paquete de extensión y al menos uno de los proveedores de SAP ASE (OLE DB o ADO.NET) en el equipo que ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Estos componentes admiten la emulación de funciones del sistema de SAP ASE y migración de datos. Para obtener instrucciones de instalación, consulte [instalar SSMA para SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md).  
  
Para iniciar SSMA, haga clic en **iniciar**, apunte a **todos los programas**, apunte a  **[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant para Sybase**y, a continuación, seleccione  **[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant para Sybase**. La primera vez que inicie SSMA, que aparece un cuadro de diálogo Administración de licencias. Debe licencias SSMA mediante el uso de un Windows Live ID para poder usar SSMA. Instrucciones de licencia se incluyen con las instrucciones de instalación en el [instalación de SSMA para Sybase cliente &#40;SybaseToSQL&#41; ](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md) tema.  
  
## <a name="ssma-for-sap-ase-user-interface"></a>SSMA para la interfaz de usuario de SAP ASE  
Después de instalar SSMA y con licencia, puede usar para migrar bases de datos de SAP ASE para SSMA [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL Database. Ayuda a familiarizarse con la interfaz de usuario SSMA antes de empezar. El siguiente diagrama muestra la interfaz de usuario de SSMA, incluidos los exploradores de los metadatos, metadatos, las barras de herramientas, panel de salida y panel de lista de errores:  
  
![SSMA para la interfaz de usuario de ASE de SAP](../../ssma/sybase/media/ssmaforsybaseuserinterface.jpg "SSMA para la interfaz de usuario de ASE de SAP")  
  
Para iniciar una migración, primero debe crear un nuevo proyecto. A continuación, se conecta a SAP ASE. Después de una conexión correcta, una jerarquía de bases de datos de SAP ASE aparecerá en el Explorador de metadatos de Sybase. Puede, a continuación, objetos de botón secundario en el Explorador de metadatos de Sybase para realizar tareas como crean informes que evaluación las conversiones a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL Database. También puede hacer estas tareas a través de los menús y barras de herramientas.  
  
También debe conectarse a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL Database. Después de una conexión correcta, una jerarquía de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o bases de datos SQL de Azure aparecerán en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o el Explorador de metadatos de SQL Azure. Después de convertir los esquemas de SAP ASE a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o esquemas de base de datos de SQL Azure, seleccione esos esquemas convertidos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o el Explorador de metadatos de SQL Azure y, a continuación, cargar los esquemas a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL Database.  
  
Después de cargar esquemas convertidos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL Database, puede volver al explorador de metadatos de Sybase y migrar datos desde bases de datos de SAP ASE en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o bases de datos SQL de Azure.  
  
Para obtener más información sobre estas tareas y cómo realizarlas, vea [migrar SAP ASE las bases de datos a SQL Server: base de datos de SQL Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md).  
  
Las siguientes secciones describen las características de la interfaz de usuario SSMA.  
  
### <a name="metadata-explorers"></a>Exploradores de metadatos  
SSMA contiene dos exploradores de los metadatos para examinar y realizar acciones en SAP ASE y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o bases de datos SQL de Azure.  
  
#### <a name="sybase-metadata-explorer"></a>Explorador de metadatos de Sybase  
Explorador de metadatos de Sybase, se muestra información acerca de las bases de datos en la instancia de origen de SAP ASE.  
  
Mediante el Explorador de metadatos de Sybase, puede realizar las siguientes tareas:  
  
-   Examinar las tablas en cada base de datos.  
  
-   Seleccionar objetos para la conversión y, a continuación, convertir los objetos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o la sintaxis de la base de datos de SQL Azure. Para obtener más información, consulte [convertir objetos de base de datos de SAP ASE &#40;SybaseToSQL&#41;](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md).  
  
-   Seleccionar objetos para la migración de datos y, a continuación, migrar los datos de dichos objetos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL Database. Para obtener más información, consulte [migrar los datos de SAP ASE en SQL Server: base de datos de SQL Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-data-into-sql-server-azure-sql-db-sybasetosql.md).  
  
#### <a name="sql-server-or-sql-azure-metadata-explorer"></a>SQL Server o el Explorador de metadatos de SQL Azure  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o el Explorador de metadatos de SQL Azure muestra información acerca de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL Database. Cuando se conecta a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL Database, SSMA recupera los metadatos sobre esa instancia y la almacena en el archivo de proyecto.  
  
Puede usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o el Explorador de metadatos de SQL Azure para seleccionar los objetos de base de datos convertidos de SAP ASE y, a continuación, cargar (sincronizar) dichos objetos en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL Database.  
  
Para obtener más información, consulte [cargar objetos de base de datos para convertir a SQL Server &#40;SybaseToSQL&#41;](../../ssma/sybase/loading-converted-database-objects-into-sql-server-sybasetosql.md).  
  
### <a name="metadata"></a>Metadatos  
A la derecha de cada explorador de metadatos son las pestañas que describen el objeto seleccionado. Por ejemplo, si selecciona una tabla en el Explorador de metadatos de Sybase, aparecen seis pestañas: **Tabla**, **SQL**, **asignación de tipos de**, **datos**, **propiedades**, y **informe**. El **informe** pestaña contiene información solo cuando se crea un informe que contiene el objeto seleccionado. Si selecciona una tabla en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o explorador de metadatos de SQL Azure, aparezcan como tres fichas: **Tabla**, **SQL**, y **datos**.  
  
La mayoría de los metadatos configuración es de solo lectura. Sin embargo, puede modificar los metadatos siguientes:  
  
-   En el Explorador de metadatos de Sybase, puede modificar los procedimientos y asignaciones de tipos. Realice estos cambios antes de convertir los esquemas.  
  
-   En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o explorador de metadatos de SQL Azure, puede modificar el [!INCLUDE[tsql](../../includes/tsql-md.md)] para los procedimientos almacenados. Realice estos cambios antes de cargar los esquemas a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Los cambios realizados en el Explorador de metadatos se reflejan en los metadatos del proyecto, no en las bases de datos de origen o destino.  
  
### <a name="toolbars"></a>Barras de herramientas  
SSMA tiene dos barras de herramientas: una barra de herramientas de proyecto y una barra de herramientas de migración.  
  
#### <a name="the-project-toolbar"></a>La barra de herramientas de proyecto  
La barra de herramientas de proyecto contiene botones para trabajar con proyectos, conectarse a SAP ASE y conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL Database. Estos botones son similares a los comandos en el **archivo** menú.  
  
#### <a name="the-migration-toolbar"></a>La barra de herramientas de migración  
La barra de herramientas de migración contiene los siguientes comandos:  
  
|Botón|Función|  
|----------|------------|  
|**Crear informe**|Convierte los objetos seleccionados de SAP ASE a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintaxis y, a continuación, crea un informe que muestra cómo se realiza correctamente la conversión.<br /><br />Este comando está disponible solo cuando se seleccionan objetos en el Explorador de metadatos de Sybase.|  
|**Convertir esquema**|Convierte los objetos seleccionados de SAP ASE a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] u objetos de base de datos de SQL Azure.<br /><br />Este comando está disponible solo cuando se seleccionan objetos en el Explorador de metadatos de Sybase.|  
|**Migración de datos**|Migra los datos de la base de datos SAP ASE [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL Database. Antes de ejecutar este comando, debe convertir los esquemas de SAP ASE en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o esquemas de base de datos de SQL Azure y, a continuación, cargar los objetos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL Database.<br /><br />Este comando está disponible solo cuando se seleccionan objetos en el Explorador de metadatos de Sybase.|  
|**Detener**|Detiene el proceso actual, como convertir objetos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o la sintaxis de la base de datos de SQL Azure.|  
  
### <a name="menus"></a>Menús  
SSMA contiene los siguientes menús:  
  
|Menú|Descripción|  
|--------|---------------|  
|**Archivo**|Contiene comandos para trabajar con proyectos, conectarse a SAP ASE y conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL Database.|  
|**Editar**|Contiene comandos para buscar y trabajar con texto en las páginas de detalles, como copiar [!INCLUDE[tsql](../../includes/tsql-md.md)] desde el panel de detalles SQL. También contiene el **administrar marcadores** opción, donde puede ver una lista de los marcadores existentes. Puede usar los botones en el lado derecho del cuadro de diálogo para administrar los marcadores.|  
|**Vista**|Contiene el **sincronizar metadatos Explorers** comando. Esto sincroniza los objetos entre el Explorador de metadatos de Sybase y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o el Explorador de metadatos de SQL Azure. También contiene comandos para mostrar y ocultar el **salida** y **lista de errores** paneles y una opción **diseños** para administrar los diseños.|  
|**Herramientas**|Contiene comandos para crear informes, exportar los datos y migrar objetos y datos. También proporciona acceso a la **configuración Global** y **configuración del proyecto** cuadros de diálogo.|  
|**Herramienta de comprobación**|Contiene comandos para crear casos de prueba, ver resultados de pruebas y comandos para la administración de copia de seguridad de base de datos.|  
|**Ayuda**|Proporciona acceso para ayudar a SSMA y a la **sobre** cuadro de diálogo.|  
  
### <a name="output-pane-and-error-list-pane"></a>Panel de salida y el panel de lista de errores  
El **vista** menú proporciona comandos para alternar la visibilidad de los paneles de salida y el panel de lista de errores:  
  
-   El panel de resultados muestra los mensajes de estado de SSMA durante la conversión de objetos, la sincronización del objeto y migración de datos.  
  
-   El panel de lista de errores, muestra un error, advertencia y mensajes informativos en una lista que se puede ordenar.  
  
## <a name="see-also"></a>Vea también  
[Migrar bases de datos de ASE de SAP a SQL Server: base de datos SQL Azure &#40;SybaseToSQL&#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
[User Interface Reference &#40;SybaseToSQL&#41;](../../ssma/sybase/user-interface-reference-sybasetosql.md)  
