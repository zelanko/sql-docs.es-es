---
title: Introducción a SQL Server Migration Assistant para Access | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 08/15/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- error list pane
- getting started
- menus
- metadata explorers
- output pane
- toolbars
- user interface
- user interface overview
ms.assetid: 462a731f-08f1-44e1-9eeb-4deac6d2f6c5
author: Shamikg
ms.author: Shamikg
manager: murato
ms.openlocfilehash: 1168609d35a266f2ac5fe6641aee7ca131bc9d89
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62759924"
---
# <a name="getting-started-with-sql-server-migration-assistant-for-access-accesstosql"></a>Introducción a SQL Server Migration Assistant para Access (AccessToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Migration Assistant (SSMA) para el acceso, podrá convertir rápidamente objetos de base de datos de Access a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o los objetos de base de datos de SQL Azure, cargue los objetos resultantes en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL DB, y migrar datos de Access a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL DB. Si es necesario, también puede vincular las tablas de Access a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o en las tablas de base de datos de SQL Azure para que pueda continuar usar las aplicaciones de front-end de Access existentes con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL DB.  
  
En este tema se presenta el proceso de instalación y ayuda a familiarizarse con la interfaz de usuario SSMA.  
  
## <a name="installing-ssma"></a>Instalación de SSMA  
Para usar SSMA, primero debe instalar el programa de cliente SSMA en un equipo que puede tener acceso a las bases de datos que desea migrar y la instancia de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL DB. Para obtener instrucciones de instalación, consulte [instalar SQL Server Migration Assistant para Access &#40;AccessToSQL&#41;](../../ssma/access/installing-sql-server-migration-assistant-for-access-accesstosql.md).  
  
Para iniciar SSMA, haga clic en **iniciar**, apunte a **todos los programas**, apunte a **SQL Server Migration Assistant para Access**y, a continuación, seleccione **migración a SQL Server El Asistente para acceso**.  
  
## <a name="using-ssma"></a>Uso de SSMA  
Después de instalar SSMA, ayuda a familiarizarse con la interfaz de usuario SSMA antes de usar la herramienta para migrar bases de datos de Access a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL DB. La interfaz de usuario SSMA, incluidos los exploradores de los metadatos, metadatos, las barras de herramientas, panel de salida y panel de lista de errores se muestran en el diagrama siguiente:  
  
![SSMA para la interfaz gráfica de usuario de Access](../../ssma/access/media/ssmaforaccessgui.gif "SSMA para la interfaz gráfica de usuario de Access")  
  
Para iniciar una migración, cree un nuevo proyecto y, a continuación, agregue las bases de datos de acceso al explorador de metadatos de acceso. A continuación, puede hacer clic en objetos en el Explorador de metadatos de acceso para realizar tareas tales como:
- Exportación de un inventario de los objetos de base de datos de Access a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL DB.
- Creación de informes que evaluación las conversiones a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL DB.
- Conversión de esquemas de acceso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o esquemas de base de datos de SQL Azure.

También puede realizar estas tareas mediante el uso de los menús y barras de herramientas.  
  
También se debe conectar a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Después de una conexión correcta, una jerarquía de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bases de datos aparece en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Explorador de metadatos. Después de convertir los esquemas de acceso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] esquemas, puede seleccionar esos esquemas convertidos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el Explorador de metadatos y, a continuación, cargar los esquemas a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Si ha seleccionado Azure SQL DB desde la migración en la lista desplegable en el cuadro de diálogo nuevo proyecto, debe conectarse a Azure SQL DB. Después de una conexión correcta, una jerarquía de bases de datos de Azure SQL DB aparece en el Explorador de metadatos de Azure SQL DB. Después de convertir los esquemas de acceso a los esquemas de base de datos de SQL Azure, puede seleccionar esos esquemas convertidos en el Explorador de metadatos de Azure SQL DB y, a continuación, cargar los esquemas a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Después de cargar esquemas convertidos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL DB, puede volver al explorador de metadatos de acceso y migrar datos desde bases de datos de Access en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o bases de datos de SQL Azure. Si es necesario, también puede vincular las tablas de Access a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o tablas de base de datos de SQL Azure.  
  
Para obtener más información sobre estas tareas y cómo realizarlas, vea los temas siguientes:  
  
-   [Preparar las bases de datos de acceso para la migración](preparing-access-databases-for-migration-accesstosql.md)  
  
-   [Migrar bases de datos de Access a SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
-   [Vinculación de aplicaciones de acceso a SQL Server](linking-access-applications-to-sql-server-azure-sql-db-accesstosql.md)  
  
Las siguientes secciones describen las características de la interfaz de usuario SSMA.  
  
### <a name="metadata-explorers"></a>Exploradores de metadatos  
SSMA contiene dos exploradores de los metadatos que puede usar para explorar y realizar acciones en Access y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o bases de datos de SQL Azure.  
  
#### <a name="access-metadata-explorer"></a>Obtener acceso al explorador de metadatos  
Explorador de metadatos de acceso se muestra información acerca de las bases de datos de Access que se han agregado al proyecto. Al agregar una base de datos de Access, SSMA recupera los metadatos sobre esa base de datos, los metadatos que están disponibles en el Explorador de metadatos de acceso.  
  
Puede usar el Explorador de metadatos de acceso para realizar las tareas siguientes:  
  
-   Examinar las tablas en cada base de datos de Access.  
  
-   Seleccionar objetos para la conversión y convertir los objetos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sintaxis. Para obtener más información, consulte [convertir objetos de base de datos de Access](converting-access-database-objects-accesstosql.md).  
  
-   Seleccionar objetos para la migración de datos y migrar los datos de dichos objetos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, consulte [migrar datos de Access a SQL Server](migrating-access-data-into-sql-server-azure-sql-db-accesstosql.md).  
  
-   Vincular y desvincular de acceso y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tablas.  
  
#### <a name="sql-server-or-azure-sql-db-metadata-explorer"></a>SQL Server o el Explorador de metadatos de base de datos de SQL Azure  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o el Explorador de metadatos de base de datos SQL de Azure muestra información acerca de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL DB. Cuando se conecta a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL DB, SSMA recupera los metadatos sobre esa instancia y la almacena en el archivo de proyecto.  
  
Puede usar SQL Server o el Explorador de metadatos de base de datos de SQL Azure para seleccionar los objetos de base de datos convertidos de acceso y cargar (sincronizar) dichos objetos en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL DB.  
  
Para obtener más información, consulte [cargar objetos de base de datos para convertir a SQL Server](loading-converted-database-objects-into-sql-server-accesstosql.md).  
  
### <a name="metadata"></a>Metadatos  
A la derecha de cada explorador de metadatos son las pestañas que describen el objeto seleccionado. Por ejemplo, si selecciona una tabla en el Explorador de metadatos de acceso, aparecen cuatro pestañas: **Tabla**, **asignación de tipos de**, **propiedades**, y **datos**. Si selecciona una tabla en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aparecen tres pestañas de explorador de metadatos: **Tabla**, **SQL**, y **datos**.  
  
La mayoría de los metadatos configuración es de solo lectura. Sin embargo, puede modificar los metadatos siguientes:  
  
-   En el Explorador de metadatos de acceso, puede modificar las asignaciones de tipos. Asegúrese de realizar estos cambios antes de crear informes o convertir los esquemas.  
  
-   En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el Explorador de metadatos, puede modificar las propiedades de tabla e índice en el **tabla** ficha. Realice estos cambios antes de cargar los esquemas a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, consulte [convertir objetos de base de datos de Access](converting-access-database-objects-accesstosql.md).  
  
### <a name="toolbars"></a>Barras de herramientas  
SSMA tiene dos barras de herramientas: una barra de herramientas de proyecto y una barra de herramientas de migración.  
  
#### <a name="the-project-toolbar"></a>La barra de herramientas de proyecto  
La barra de herramientas de proyecto contiene botones para trabajar con proyectos, agregar archivos de base de datos de Access y conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL DB. Estos botones son similares a los comandos en el **archivo** menú.  
  
#### <a name="the-migration-toolbar"></a>La barra de herramientas de migración  
La barra de herramientas de migración contiene los siguientes comandos:  
  
|Botón|Función|  
|----------|------------|  
|**Convertir, cargar y migrar**|Convierte las bases de datos de Access, carga los objetos convertidos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL DB, y migra los datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL DB, todo en un paso.|  
|**Crear informe**|Convierte el esquema de acceso seleccionado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o sintaxis de la base de datos de SQL Azure y, a continuación, crea un informe que muestra cómo se realiza correctamente la conversión.<br /><br />Este comando está disponible solo cuando se seleccionan objetos en el Explorador de metadatos de acceso.|  
|**Convertir esquema**|Convierte el esquema de acceso seleccionado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o esquemas de base de datos de SQL Azure.<br /><br />Este comando está disponible solo cuando se seleccionan objetos en el Explorador de metadatos de acceso.|  
|**Migración de datos**|Migra los datos de la base de datos de Access a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL DB. Antes de ejecutar este comando, debe convertir los esquemas de acceso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o esquemas de base de datos de SQL Azure y, a continuación, cargar los objetos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL DB.<br /><br />Este comando está disponible solo cuando se seleccionan objetos en el Explorador de metadatos de acceso.|  
|**Detener**|Detiene el proceso actual, como convertir objetos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o la sintaxis de la base de datos de SQL Azure.|  
  
### <a name="menus"></a>Menús  
SSMA contiene los siguientes menús:  
  
|Menú|Descripción|  
|--------|---------------|  
|**Archivo**|Contiene comandos para el Asistente para migración, trabajar con proyectos, agregar y quitar el acceso a los archivos de base de datos y conectar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Azure SQL DB.|  
|**Editar**|Contiene comandos para buscar y trabajar con texto en las páginas de detalles, como copiar [!INCLUDE[tsql](../../includes/tsql-md.md)] desde el panel de detalles SQL. Para abrir el **administrar marcadores** cuadro de diálogo, en el menú Edición, haga clic en Administrar marcadores. En el cuadro de diálogo, verá una lista de los marcadores existentes. Puede usar los botones en el lado derecho del cuadro de diálogo para administrar los marcadores.|  
|**Vista**|Contiene el **sincronizar metadatos Explorers** comando. Esto sincroniza los objetos entre el Explorador de metadatos de acceso y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o el Explorador de metadatos de base de datos de SQL Azure. También contiene comandos para mostrar y ocultar el **salida** y **lista de errores** paneles y una opción **diseños** para administrar con los diseños.|  
|**Herramientas**|Contiene comandos para crear informes, exportar datos, migración de datos y objetos, vincular tablas y proporciona acceso global y la configuración del proyecto de cuadros de diálogo.|  
|**Ayuda**|Proporciona acceso para ayudar a SSMA y a la **sobre** cuadro de diálogo.|  
  
### <a name="output-pane-and-error-list-pane"></a>Panel de salida y el panel de lista de errores  
El **vista** menú proporciona comandos para alternar la visibilidad de los paneles de salida y el panel de lista de errores:  
  
-   El panel de resultados muestra los mensajes de estado de SSMA durante la conversión de objetos, la sincronización del objeto y migración de datos.  
  
-   El panel de lista de errores, muestra un error, advertencia y mensajes informativos en una lista que se puede ordenar.  
  
## <a name="see-also"></a>Vea también  
[Migrar bases de datos de Access a SQL Server](migrating-access-databases-to-sql-server-azure-sql-db-accesstosql.md)  
  
