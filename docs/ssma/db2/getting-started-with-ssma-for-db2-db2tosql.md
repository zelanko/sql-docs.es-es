---
title: "Introducción a SSMA para DB2 (DB2ToSQL) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: ssma-db2
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.technology: sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 48ca32fc-1830-4d1f-add7-480ba5ad02e8
caps.latest.revision: "6"
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e22ba8791b1905e49a9ce9bb87cee68e69af9e43
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="getting-started-with-ssma-for-db2-db2tosql"></a>Introducción a SSMA para DB2 (DB2ToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Migration Assistant (SSMA) para DB2 permite rápidamente convertir esquemas de base de datos de DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] esquemas, cargar los esquemas resultantes a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] y migrar datos de DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
En este tema se presenta el proceso de instalación y, a continuación, le ayuda a familiarizarse con la interfaz de usuario SSMA.  
  
## <a name="installing-ssma"></a>Instalación de SSMA  
Para usar SSMA, primero debe instalar el programa de cliente SSMA en un equipo que puede tener acceso a la base de datos de origen DB2 y la instancia de destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Proveedores de OLE DB DB2 en el equipo que está ejecutando [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Estos componentes admiten la migración de datos y la emulación de funciones del sistema DB2. Para obtener instrucciones de instalación, consulte [instalar SSMA para DB2 &#40; DB2ToSQL &#41;](../../ssma/db2/installing-ssma-for-db2-db2tosql.md).  
  
Para iniciar SSMA, haga clic en **iniciar**, seleccione **todos los programas**, seleccione  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant para DB2**y, a continuación, haga clic en  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant para DB2**.  
  
## <a name="ssma-for-db2-user-interface"></a>SSMA para la interfaz de usuario de DB2  
Después de instala SSMA, puede usar SSMA para migrar bases de datos de DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Ayuda para familiarizarse con la interfaz de usuario SSMA antes de empezar. El siguiente diagrama muestra la interfaz de usuario de SSMA, incluidos los exploradores de metadatos, metadatos, las barras de herramientas, panel de salida y panel de lista de error:  
  
![Interfaz de usuario SSMA](../../ssma/db2/media/ssma_db2_ui.png "interfaz de usuario SSMA")  
  
Para iniciar una migración, primero debe crear un nuevo proyecto. A continuación, se conecta a una base de datos DB2. Después de una conexión correcta, los esquemas de DB2 aparecerá en el Explorador de metadatos de DB2. También puede, a continuación, objetos de menú contextual en el Explorador de metadatos de DB2 para realizar tareas como crean informes que evalúa las conversiones a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. También puede realizar estas tareas mediante el uso de las barras de herramientas y menús.  
  
También debe conectarse a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Después de una conexión correcta, una jerarquía de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] bases de datos aparecerá en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Explorador de metadatos. Después de convertir esquemas de DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] esquemas, seleccione dichos esquemas convertidos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] el Explorador de metadatos y, a continuación, sincronizar los esquemas con [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
Después de sincronizar esquemas convertidos con [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], puede volver al explorador de metadatos de DB2 y migrar datos de esquemas de DB2 en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] bases de datos.  
  
Para obtener más información sobre estas tareas y cómo realizarlas, vea [migrar bases de datos DB2 a SQL Server &#40; DB2ToSQL &#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md).  
  
Las secciones siguientes describen las características de la interfaz de usuario SSMA.  
  
### <a name="metadata-explorers"></a>Exploradores de metadatos  
SSMA contiene dos exploradores de metadatos para examinar y realizar acciones en DB2 y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] las bases de datos.  
  
#### <a name="db2-metadata-explorer"></a>DB2 Explorador de metadatos  
Explorador de metadatos de DB2 muestra información acerca de los esquemas de DB2. Mediante el Explorador de metadatos de DB2, puede realizar las siguientes tareas:  
  
-   Examinar los objetos de cada esquema.  
  
-   Seleccionar objetos para la conversión y, a continuación, convertir los objetos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] sintaxis. Para obtener más información, consulte [convertir esquemas de DB2 &#40; DB2ToSQL &#41;](../../ssma/db2/converting-db2-schemas-db2tosql.md).  
  
-   Seleccionar tablas para la migración de datos y, a continuación, migrar los datos de esas tablas en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Para obtener más información, consulte [migrar bases de datos DB2 a SQL Server &#40; DB2ToSQL &#41;](../../ssma/db2/migrating-db2-databases-to-sql-server-db2tosql.md).  
  
#### <a name="sql-server-metadata-explorer"></a>Explorador de metadatos SQL Server  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Explorador de metadatos muestra información sobre una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Cuando se conecta a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], SSMA recupera metadatos acerca de esa instancia y lo almacena en el archivo de proyecto.  
  
Puede usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Explorador de metadatos para seleccionar objetos de base de datos de DB2 convertidos y, a continuación, sincroniza esos objetos con la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
### <a name="metadata"></a>Metadatos  
A la derecha de cada explorador de metadatos son las pestañas que describen el objeto seleccionado. Por ejemplo, si selecciona una tabla en el Explorador de metadatos de DB2, seis pestañas aparecerán: **tabla**, **SQL**, **asignación de tipo, el informe**, **propiedades**, y **datos**. El **informe** pestaña contiene información únicamente después de crear un informe que contiene el objeto seleccionado. Si selecciona una tabla en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] el Explorador de metadatos, aparecerán tres fichas: **tabla**, **SQL**, y **datos**.  
  
Mayoría de los valores de metadatos es de solo lectura. Sin embargo, puede modificar los metadatos siguientes:  
  
-   En el Explorador de metadatos de DB2, puede modificar los procedimientos y las asignaciones de tipos. Para convertir los procedimientos modificados y asignaciones de tipos, realizar cambios antes de convertir esquemas.  
  
-   En [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] el Explorador de metadatos, puede modificar el [!INCLUDE[tsql](../../includes/tsql_md.md)] para los procedimientos almacenados. Para ver estos cambios en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], realice estos cambios antes de cargar los esquemas en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
Los cambios realizados en el Explorador de metadatos se reflejan en los metadatos del proyecto, no en las bases de datos de origen o de destino.  
  
### <a name="toolbars"></a>Barras de herramientas  
SSMA tiene dos barras de herramientas: una barra de herramientas de proyecto y una barra de herramientas de migración.  
  
#### <a name="the-project-toolbar"></a>La barra de herramientas de proyecto  
La barra de herramientas de proyecto contiene botones para trabajar con proyectos, conéctese a DB2 y conéctese a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Estos botones son similares a los comandos en el **archivo** menú.  
  
#### <a name="migration-toolbar"></a>Barra de herramientas de migración  
La siguiente tabla muestra los comandos de barra de herramientas de la migración:  
  
|Botón|Función|  
|------|--------|  
|**Crear informe**|Convierte los objetos de DB2 seleccionados a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] sintaxis y, a continuación, crea un informe que muestra cómo se realiza correctamente la conversión.<br /><br />Este comando está deshabilitado a menos que se seleccionan objetos en el Explorador de metadatos de DB2.|  
|**Convertir esquema**|Convierte los objetos de DB2 seleccionados a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] objetos.<br /><br />Este comando está deshabilitado a menos que se seleccionan objetos en el Explorador de metadatos de DB2.|  
|**Migrar datos**|Migra los datos de la base de datos DB2 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Antes de ejecutar este comando, debe convertir los esquemas de DB2 a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] esquemas y, a continuación, cargar los objetos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].<br /><br />Este comando está deshabilitado a menos que se seleccionan objetos en el Explorador de metadatos de DB2.|  
|**Detener**|Detiene el proceso actual.|  
  
### <a name="menus"></a>Menús  
La siguiente tabla muestra los menús SSMA.  
  
|Menú|Description|  
|----|-----------|  
|**Archivo**|Contiene comandos para trabajar con proyectos, conéctese a DB2 y conéctese a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].|  
|**Editar**|Contiene comandos para buscar y trabajar con texto en las páginas de detalles, como copiar [!INCLUDE[tsql](../../includes/tsql_md.md)] desde el panel de detalles SQL. También contiene el **administrar marcadores** opción, donde podrá ver una lista de los marcadores existentes. Puede usar los botones en el lado derecho del cuadro de diálogo para administrar los marcadores.|  
|**Ver**|Contiene el **sincronizar metadatos exploradores** comando. Que sincroniza los objetos entre el Explorador de metadatos de DB2 y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Explorador de metadatos. También contiene comandos para mostrar y ocultar el **salida** y **lista de errores** paneles y una opción **diseños** para administrar los diseños.|  
|**Herramientas**|Contiene comandos para crear informes y migra los datos y objetos. También proporciona acceso a la **configuración Global** y **configuración del proyecto** cuadros de diálogo.|  
|**Ayuda**|Proporciona acceso a la Ayuda de SSMA y a la **sobre** cuadro de diálogo.|  
  
### <a name="output-pane-and-error-list-pane"></a>Panel de resultados y el panel de lista de errores  
El **vista** menú proporciona comandos para alternar la visibilidad de los paneles de salida y la lista de errores:  
  
-   El panel de resultados muestra los mensajes de estado de SSMA durante la conversión de objetos, la sincronización de objetos y la migración de datos.  
  
-   El panel de lista de errores muestra mensajes informativos, de advertencia y de error en una lista que se puede ordenar.  
  
## <a name="see-also"></a>Vea también  
[Migrar datos de DB2 en SQL Server &#40; DB2ToSQL &#41;](../../ssma/db2/migrating-db2-data-into-sql-server-db2tosql.md)  
[Referencia de la interfaz de usuario &#40; DB2ToSQL &#41;](../../ssma/db2/user-interface-reference-db2tosql.md)  
  
