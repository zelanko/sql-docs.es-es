---
title: "Introducción a SSMA para Oracle (OracleToSQL) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SSMA for Oracle, Metadata Explorers
- SSMA for Oracle, Toolbars
ms.assetid: df79664c-972e-4bef-865a-ce609789fee7
caps.latest.revision: 9
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 2ad25369dc4a9d9cc7a26795320050dcb583e92b
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="getting-started-with-ssma-for-oracle-oracletosql"></a>Introducción a SSMA para Oracle (OracleToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Migration Assistant (SSMA) para Oracle permite rápidamente convertir esquemas de base de datos de Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] esquemas, cargar los esquemas resultantes a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] y migrar datos de Oracle en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
En este tema se presenta el proceso de instalación y, a continuación, le ayuda a familiarizarse con la interfaz de usuario SSMA.  
  
## <a name="installing-ssma"></a>Instalación de SSMA  
Para usar SSMA, primero debe instalar el programa de cliente SSMA en un equipo que puede tener acceso a la base de datos de Oracle de origen y la instancia de destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. A continuación, debe instalar un paquete de extensión y al menos uno de los proveedores de Oracle (OLE DB o [!INCLUDE[vstecado](../../includes/vstecado_md.md)]) en el equipo que está ejecutando [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Estos componentes admiten la migración de datos y la emulación de funciones del sistema de Oracle. Para obtener instrucciones de instalación, consulte [instalar SSMA para Oracle &#40; OracleToSQL &#41;](../../ssma/oracle/installing-ssma-for-oracle-oracletosql.md).  
  
Para iniciar SSMA, haga clic en **iniciar**, seleccione **todos los programas**, seleccione  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant para Oracle**y, a continuación, haga clic en  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Migration Assistant para Oracle**.  
  
## <a name="ssma-for-oracle-user-interface"></a>SSMA para la interfaz de usuario de Oracle  
Después de instala SSMA, puede usar SSMA para migrar bases de datos de Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Ayuda para familiarizarse con la interfaz de usuario SSMA antes de empezar. El siguiente diagrama muestra la interfaz de usuario de SSMA, incluidos los exploradores de metadatos, metadatos, las barras de herramientas, panel de salida y panel de lista de error:  
  
![SSMA para la interfaz de usuario de Oracle](../../ssma/oracle/media/ssma_oracle_ui.jpg "SSMA para la interfaz de usuario de Oracle")  
  
Para iniciar una migración, primero debe crear un nuevo proyecto. A continuación, se conecta a una base de datos de Oracle. Después de una conexión correcta, los esquemas de Oracle aparecerá en el Explorador de metadatos de Oracle. También puede, a continuación, objetos de menú contextual en el Explorador de metadatos de Oracle para realizar tareas como crean informes que evalúa las conversiones a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. También puede realizar estas tareas mediante el uso de las barras de herramientas y menús.  
  
También debe conectarse a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Después de una conexión correcta, una jerarquía de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] bases de datos aparecerá en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Explorador de metadatos. Después de convertir esquemas de Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] esquemas, seleccione dichos esquemas convertidos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] el Explorador de metadatos y, a continuación, sincronizar los esquemas con [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
Después de sincronizar esquemas convertidos con [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], puede volver al explorador de metadatos de Oracle y migrar datos de esquemas de Oracle en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] bases de datos.  
  
Para obtener más información sobre estas tareas y cómo realizarlas, vea [migrar bases de datos de Oracle a SQL Server &#40; OracleToSQL &#41;](../../ssma/oracle/migrating-oracle-databases-to-sql-server-oracletosql.md).  
  
Las secciones siguientes describen las características de la interfaz de usuario SSMA.  
  
### <a name="metadata-explorers"></a>Exploradores de metadatos  
SSMA contiene dos exploradores de metadatos para examinar y realizar acciones en Oracle y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] las bases de datos.  
  
#### <a name="oracle-metadata-explorer"></a>Explorador de metadatos de Oracle  
Explorador de metadatos de Oracle, se muestra información acerca de los esquemas de Oracle. Mediante el Explorador de metadatos de Oracle, puede realizar las siguientes tareas:  
  
-   Examinar los objetos de cada esquema.  
  
-   Seleccionar objetos para la conversión y, a continuación, convertir los objetos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] sintaxis. Para obtener más información, consulte [convertir esquemas de Oracle &#40; OracleToSQL &#41;](../../ssma/oracle/converting-oracle-schemas-oracletosql.md).  
  
-   Seleccionar tablas para la migración de datos y, a continuación, migrar los datos de esas tablas en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Para obtener más información, consulte [migrar datos de Oracle en SQL Server &#40; OracleToSQL &#41;](../../ssma/oracle/migrating-oracle-data-into-sql-server-oracletosql.md).  
  
#### <a name="sql-server-metadata-explorer"></a>Explorador de metadatos SQL Server  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Explorador de metadatos muestra información sobre una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Cuando se conecta a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], SSMA recupera metadatos acerca de esa instancia y lo almacena en el archivo de proyecto.  
  
Puede usar [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Explorador de metadatos para seleccionar objetos de base de datos de Oracle convertidos y, a continuación, sincroniza esos objetos con la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
Para obtener más información, consulte [cargar objetos de base de datos para convertir a SQL Server &#40; OracleToSQL &#41;](../../ssma/oracle/loading-converted-database-objects-into-sql-server-oracletosql.md).  
  
### <a name="metadata"></a>Metadatos  
A la derecha de cada explorador de metadatos son las pestañas que describen el objeto seleccionado. Por ejemplo, si selecciona una tabla en el Explorador de metadatos de Oracle, seis pestañas aparecerán: **tabla**, **SQL**, **asignación de tipo, el informe**, **propiedades**, y **datos**. El **informe** pestaña contiene información únicamente después de crear un informe que contiene el objeto seleccionado. Si selecciona una tabla en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] el Explorador de metadatos, aparecerán tres fichas: **tabla**, **SQL**, y **datos**.  
  
Mayoría de los valores de metadatos es de solo lectura. Sin embargo, puede modificar los metadatos siguientes:  
  
-   En el Explorador de metadatos de Oracle, puede modificar los procedimientos y las asignaciones de tipos. Para convertir los procedimientos modificados y asignaciones de tipos, realizar cambios antes de convertir esquemas.  
  
-   En [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] el Explorador de metadatos, puede modificar el [!INCLUDE[tsql](../../includes/tsql_md.md)] para los procedimientos almacenados. Para ver estos cambios en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)], realice estos cambios antes de cargar los esquemas en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
Los cambios realizados en el Explorador de metadatos se reflejan en los metadatos del proyecto, no en las bases de datos de origen o de destino.  
  
### <a name="toolbars"></a>Barras de herramientas  
SSMA tiene dos barras de herramientas: una barra de herramientas de proyecto y una barra de herramientas de migración.  
  
#### <a name="the-project-toolbar"></a>La barra de herramientas de proyecto  
La barra de herramientas de proyecto contiene botones para trabajar con proyectos, conectarse a Oracle y conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Estos botones son similares a los comandos en el **archivo** menú.  
  
#### <a name="migration-toolbar"></a>Barra de herramientas de migración  
La siguiente tabla muestra los comandos de barra de herramientas de la migración:  
  
|Botón|Función|  
|------|--------|  
|**Crear informe**|Convierte los objetos seleccionados de Oracle a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] sintaxis y, a continuación, crea un informe que muestra cómo se realiza correctamente la conversión.<br /><br />Este comando está deshabilitado a menos que se seleccionan objetos en el Explorador de metadatos de Oracle.|  
|**Convertir esquema**|Convierte los objetos seleccionados de Oracle a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] objetos.<br /><br />Este comando está deshabilitado a menos que se seleccionan objetos en el Explorador de metadatos de Oracle.|  
|**Migrar datos**|Migra los datos de la base de datos Oracle [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Antes de ejecutar este comando, debe convertir los esquemas de Oracle para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] esquemas y, a continuación, cargar los objetos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].<br /><br />Este comando está deshabilitado a menos que se seleccionan objetos en el Explorador de metadatos de Oracle.|  
|**Detener**|Detiene el proceso actual.|  
  
### <a name="menus"></a>Menús  
La siguiente tabla muestra los menús SSMA.  
  
|Menú|Description|  
|----|-----------|  
|**Archivo**|Contiene comandos para trabajar con proyectos, conectarse a Oracle y conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].|  
|**Editar**|Contiene comandos para buscar y trabajar con texto en las páginas de detalles, como copiar [!INCLUDE[tsql](../../includes/tsql_md.md)] desde el panel de detalles SQL. También contiene el **administrar marcadores** opción, donde podrá ver una lista de los marcadores existentes. Puede usar los botones en el lado derecho del cuadro de diálogo para administrar los marcadores.|  
|**Ver**|Contiene el **sincronizar metadatos exploradores** comando. Que sincroniza los objetos entre el Explorador de metadatos de Oracle y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Explorador de metadatos. También contiene comandos para mostrar y ocultar el **salida** y **lista de errores** paneles y una opción **diseños** para administrar los diseños.|  
|**Herramientas**|Contiene comandos para crear informes y migra los datos y objetos. También proporciona acceso a la **configuración Global** y **configuración del proyecto** cuadros de diálogo.|  
|**Herramienta de comprobación**|Contiene comandos para crear y trabajar con casos de prueba, el repositorio y el sistema de administración de copia de seguridad.|  
|**Ayuda**|Proporciona acceso a la Ayuda de SSMA y a la **sobre** cuadro de diálogo.|  
  
### <a name="output-pane-and-error-list-pane"></a>Panel de resultados y el panel de lista de errores  
El **vista** menú proporciona comandos para alternar la visibilidad de los paneles de salida y la lista de errores:  
  
-   El panel de resultados muestra los mensajes de estado de SSMA durante la conversión de objetos, la sincronización de objetos y la migración de datos.  
  
-   El panel de lista de errores muestra mensajes informativos, de advertencia y de error en una lista que se puede ordenar.  
  
## <a name="see-also"></a>Vea también  
[Migrar datos de Oracle en SQL Server &#40; OracleToSQL &#41;](../../ssma/oracle/migrating-oracle-data-into-sql-server-oracletosql.md)  
[Referencia de la interfaz de usuario &#40; OracleToSQL &#41;](../../ssma/oracle/user-interface-reference-oracletosql.md)  
  

