---
title: "Introducción a SSMA para SAP ASE (SybaseToSQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 09/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: c4098516-f0fc-4690-97bb-3766dfd43156
caps.latest.revision: "10"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a4cc7553ec5936efeafdde72f87b19c9656a699e
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="getting-started-with-ssma-for-sap-ase-sybasetosql"></a>Introducción a SSMA para SAP ASE (SybaseToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Migration Assistant (SSMA) para SAP ASE le permite rápidamente convertir esquemas de base de datos de SAP Adaptive Server Enterprise (ASE) a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o esquemas de base de datos de SQL Azure, cargue los esquemas resultantes a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure, y migrar datos desde SAP ASE a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos SQL Azure.  
  
En este tema se presenta el proceso de instalación y, a continuación, le ayuda a familiarizarse con la interfaz de usuario SSMA.  
  
## <a name="installing-and-licensing-ssma"></a>Instalación y licencias de SSMA  
Para usar SSMA, primero debe instalar el programa de cliente SSMA en un equipo que puede tener acceso a la instancia de origen de SAP ASE tanto la instancia de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure. Para usar la migración de datos en el servidor, debe instalar el paquete de extensión y al menos uno de los proveedores de SAP ASE (OLE DB o ADO.NET) en el equipo que está ejecutando [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Estos componentes admiten la emulación de funciones del sistema SAP ASE y migración de datos. Para obtener instrucciones de instalación, consulte [instalar SSMA para SAP ASE &#40; SybaseToSQL &#41; ](../../ssma/sybase/installing-ssma-for-sybase-sybasetosql.md).  
  
Para iniciar SSMA, haga clic en **iniciar**, seleccione **todos los programas**, seleccione  **[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant para Sybase**y, a continuación, seleccione  **[!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant para Sybase**. La primera vez que inicie SSMA, que aparece un cuadro de diálogo de licencia. Debe licencias SSMA mediante el uso de un Windows Live ID para poder usar SSMA. Instrucciones de licencia se incluyen con las instrucciones de instalación de la [instalar SSMA para Sybase cliente &#40; SybaseToSQL &#41; ](../../ssma/sybase/installing-ssma-for-sybase-client-sybasetosql.md) tema.  
  
## <a name="ssma-for-sap-ase-user-interface"></a>SSMA para la interfaz de usuario de SAP ASE  
Después de SSMA se instala y se autoriza el uso de, puede usar SSMA para migrar bases de datos de SAP ASE a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure. Ayuda para familiarizarse con la interfaz de usuario SSMA antes de empezar. El siguiente diagrama muestra la interfaz de usuario de SSMA, incluidos los exploradores de metadatos, metadatos, las barras de herramientas, panel de salida y panel de lista de error:  
  
![SSMA para la interfaz de usuario de ASE de SAP](../../ssma/sybase/media/ssmaforsybaseuserinterface.jpg "SSMA para la interfaz de usuario de ASE de SAP")  
  
Para iniciar una migración, primero debe crear un nuevo proyecto. A continuación, se conecta a SAP ASE. Después de una conexión correcta, una jerarquía de bases de datos de SAP ASE aparecerá en el Explorador de metadatos de Sybase. También puede, a continuación, objetos de menú contextual en el Explorador de metadatos de Sybase para realizar tareas como crean informes que evalúa las conversiones a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure. También puede realizar estas tareas mediante los menús y barras de herramientas.  
  
También debe conectarse a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure. Después de una conexión correcta, una jerarquía de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o bases de datos SQL de Azure se mostrarán en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o en el Explorador de metadatos de SQL Azure. Después de convertir esquemas de SAP ASE a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o esquemas de base de datos de SQL Azure, seleccione dichos esquemas convertidos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o el Explorador de metadatos de SQL Azure y, a continuación, cargar los esquemas en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure.  
  
Después de cargar los esquemas convertidos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure, puede volver al explorador de metadatos de Sybase y migrar datos desde bases de datos de SAP ASE en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o bases de datos de SQL Azure.  
  
Para obtener más información sobre estas tareas y cómo realizarlas, vea [migrando SAP ASE bases de datos a SQL Server: base de datos de SQL de Azure &#40; SybaseToSQL &#41; ](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md).  
  
Las secciones siguientes describen las características de la interfaz de usuario SSMA.  
  
### <a name="metadata-explorers"></a>Exploradores de metadatos  
SSMA contiene dos exploradores de metadatos para examinar y realizar acciones en SAP ASE y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o bases de datos de SQL Azure.  
  
#### <a name="sybase-metadata-explorer"></a>Explorador de metadatos de Sybase  
Explorador de metadatos de Sybase muestra información acerca de las bases de datos en la instancia de origen de SAP ASE.  
  
Mediante el Explorador de metadatos de Sybase, puede realizar las siguientes tareas:  
  
-   Examinar las tablas en cada base de datos.  
  
-   Seleccionar objetos para la conversión y, a continuación, convertir los objetos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o la sintaxis de la base de datos de SQL Azure. Para obtener más información, vea [convertir objetos de base de datos de SAP ASE &#40; SybaseToSQL &#41; ](../../ssma/sybase/converting-sybase-ase-database-objects-sybasetosql.md).  
  
-   Seleccionar objetos para la migración de datos y, a continuación, migrar los datos de dichos objetos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure. Para obtener más información, vea [migrar los datos de SAP ASE en SQL Server: base de datos de SQL de Azure &#40; SybaseToSQL &#41; ](../../ssma/sybase/migrating-sybase-ase-data-into-sql-server-azure-sql-db-sybasetosql.md).  
  
#### <a name="sql-server-or-sql-azure-metadata-explorer"></a>SQL Server o el Explorador de metadatos de Azure SQL  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]o el Explorador de metadatos de SQL Azure muestra información sobre una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure. Cuando se conecta a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure, SSMA recupera metadatos acerca de esa instancia y lo almacena en el archivo de proyecto.  
  
Puede usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o el Explorador de metadatos de SQL Azure para seleccionar objetos de base de datos de SAP ASE convertidos y, a continuación, cargar (synchronize) esos objetos en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure.  
  
Para obtener más información, vea [cargar objetos de base de datos para convertir a SQL Server &#40; SybaseToSQL &#41; ](../../ssma/sybase/loading-converted-database-objects-into-sql-server-sybasetosql.md).  
  
### <a name="metadata"></a>Metadatos  
A la derecha de cada explorador de metadatos son las pestañas que describen el objeto seleccionado. Por ejemplo, si selecciona una tabla en el Explorador de metadatos de Sybase, aparecen seis fichas: **tabla**, **SQL**, **Type Mapping**, **datos**,  **Propiedades**, y **informe**. El **informe** pestaña contiene información solo cuando se crea un informe que contiene el objeto seleccionado. Si selecciona una tabla en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o explorador de metadatos de SQL Azure, aparecen de tres pestañas: **tabla**, **SQL**, y **datos**.  
  
Mayoría de los valores de metadatos es de solo lectura. Sin embargo, puede modificar los metadatos siguientes:  
  
-   En el Explorador de metadatos de Sybase, puede modificar los procedimientos y las asignaciones de tipos. Realice estos cambios antes de convertir esquemas.  
  
-   En [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o explorador de metadatos de SQL Azure, puede modificar el [!INCLUDE[tsql](../../includes/tsql_md.md)] para los procedimientos almacenados. Realice estos cambios antes de cargar los esquemas en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
Los cambios realizados en el Explorador de metadatos se reflejan en los metadatos del proyecto, no en las bases de datos de origen o de destino.  
  
### <a name="toolbars"></a>Barras de herramientas  
SSMA tiene dos barras de herramientas: una barra de herramientas de proyecto y una barra de herramientas de migración.  
  
#### <a name="the-project-toolbar"></a>La barra de herramientas de proyecto  
La barra de herramientas de proyecto contiene botones para trabajar con proyectos, conéctese a SAP ASE y conéctese a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure. Estos botones son similares a los comandos en el **archivo** menú.  
  
#### <a name="the-migration-toolbar"></a>La barra de herramientas de migración  
La barra de herramientas de migración contiene los siguientes comandos:  
  
|Botón|Función|  
|----------|------------|  
|**Crear informe**|Convierte los objetos de SAP ASE seleccionados a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] sintaxis y, a continuación, crea un informe que muestra cómo se realiza correctamente la conversión.<br /><br />Este comando está disponible sólo cuando se seleccionan objetos en el Explorador de metadatos de Sybase.|  
|**Convertir esquema**|Convierte los objetos de SAP ASE seleccionados a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] u objetos de base de datos de SQL Azure.<br /><br />Este comando está disponible sólo cuando se seleccionan objetos en el Explorador de metadatos de Sybase.|  
|**Migrar datos**|Migra los datos de la base de datos SAP ASE [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure. Antes de ejecutar este comando, debe convertir los esquemas de SAP ASE a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o esquemas de base de datos de SQL Azure y, a continuación, cargar los objetos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure.<br /><br />Este comando está disponible sólo cuando se seleccionan objetos en el Explorador de metadatos de Sybase.|  
|**Detener**|Detiene el proceso actual, como convertir objetos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o la sintaxis de la base de datos de SQL Azure.|  
  
### <a name="menus"></a>Menús  
SSMA contiene los siguientes menús:  
  
|Menú|Description|  
|--------|---------------|  
|**Archivo**|Contiene comandos para trabajar con proyectos, conéctese a SAP ASE y conéctese a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure.|  
|**Editar**|Contiene comandos para buscar y trabajar con texto en las páginas de detalles, como copiar [!INCLUDE[tsql](../../includes/tsql_md.md)] desde el panel de detalles SQL. También contiene el **administrar marcadores** opción, donde puede ver una lista de los marcadores existentes. Puede usar los botones en el lado derecho del cuadro de diálogo para administrar los marcadores.|  
|**Ver**|Contiene el **sincronizar metadatos exploradores** comando. Esto sincroniza los objetos entre el Explorador de metadatos de Sybase y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o en el Explorador de metadatos de SQL Azure. También contiene comandos para mostrar y ocultar el **salida** y **lista de errores** paneles y una opción **diseños** para administrar los diseños.|  
|**Herramientas**|Contiene comandos para crear informes, exportar los datos y migrar objetos y los datos. También proporciona acceso a la **configuración Global** y **configuración del proyecto** cuadros de diálogo.|  
|**Herramienta de comprobación**|Contiene comandos para crear comandos para la administración de copia de seguridad de base de datos, ver los resultados de pruebas y casos de prueba.|  
|**Ayuda**|Proporciona acceso a la Ayuda de SSMA y a la **sobre** cuadro de diálogo.|  
  
### <a name="output-pane-and-error-list-pane"></a>Panel de resultados y el panel de lista de errores  
El **vista** menú proporciona comandos para alternar la visibilidad de los paneles de salida y la lista de errores:  
  
-   El panel de resultados muestra los mensajes de estado de SSMA durante la conversión de objetos, la sincronización de objetos y la migración de datos.  
  
-   El panel de lista de errores muestra mensajes informativos, de advertencia y de error en una lista que se puede ordenar.  
  
## <a name="see-also"></a>Vea también  
[Migrar SAP ASE bases de datos a SQL Server: base de datos SQL Azure &#40; SybaseToSQL &#41;](../../ssma/sybase/migrating-sybase-ase-databases-to-sql-server-azure-sql-db-sybasetosql.md)  
[Referencia de la interfaz de usuario &#40; SybaseToSQL &#41;](../../ssma/sybase/user-interface-reference-sybasetosql.md)  
