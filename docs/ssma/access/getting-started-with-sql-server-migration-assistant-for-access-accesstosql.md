---
title: "Introducción a SQL Server Migration Assistant para Access | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 08/15/2017
ms.reviewer: 
ms.suite: 
ms.technology:
- sql-ssma
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
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
caps.latest.revision: 24
author: Shamikg
ms.author: Shamikg
manager: murato
ms.translationtype: MT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 846d08c9226e6a34e0d0b3bbd5efab8c2548a469
ms.contentlocale: es-es
ms.lasthandoff: 09/07/2017

---
# <a name="getting-started-with-sql-server-migration-assistant-for-access-accesstosql"></a>Introducción a SQL Server Migration Assistant para Access (AccessToSQL)
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Migration Assistant (SSMA) para acceso permite convertir rápidamente objetos de base de datos de Access a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] u objetos de base de datos de SQL Azure, cargue los objetos resultantes en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure, y migrar datos de acceso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure. Si es necesario, también puede vincular tablas de Access a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o en las tablas de base de datos de SQL Azure para que pueda continuar utilizando sus aplicaciones front-end de acceso existentes con [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure.  
  
En este tema se presenta el proceso de instalación y ayuda a familiarizarse con la interfaz de usuario SSMA.  
  
## <a name="installing-ssma"></a>Instalación de SSMA  
Para usar SSMA, primero debe instalar el programa de cliente SSMA en un equipo que puede tener acceso a las bases de datos que desea migrar y la instancia de destino [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure. Para obtener instrucciones de instalación, consulte [instalar SQL Server Migration Assistant para acceder al &#40; AccessToSQL &#41; ](../../ssma/access/installing-sql-server-migration-assistant-for-access-accesstosql.md).  
  
Para iniciar SSMA, haga clic en **iniciar**, seleccione **todos los programas**, seleccione **SQL Server Migration Assistant para Access**y, a continuación, seleccione **SQL Server Migration Assistant para Access**.  
  
## <a name="using-ssma"></a>Uso de SSMA  
Después de instalar SSMA, ayuda a familiarizarse con la interfaz de usuario SSMA antes de usar la herramienta para migrar bases de datos de Access a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure. La interfaz de usuario SSMA, incluidos los exploradores de metadatos, metadatos, las barras de herramientas, panel de salida y panel de lista de errores se muestran en el diagrama siguiente:  
  
![SSMA para la interfaz gráfica de usuario de Access](../../ssma/access/media/ssmaforaccessgui.gif "SSMA para la interfaz gráfica de usuario de Access")  
  
Para iniciar una migración, cree un nuevo proyecto y, a continuación, agregar las bases de datos de acceso al explorador de metadatos de acceso. Puede, a continuación, haga clic en objetos en el Explorador de metadatos de acceso para realizar tareas tales como:
- Exportar un inventario de los objetos de base de datos de Access a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure.
- Creación de informes que evalúa las conversiones a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure.
- Convertir esquemas de acceso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o esquemas de base de datos de SQL Azure.

También puede realizar estas tareas mediante el uso de las barras de herramientas y menús.  
  
También debe conectarse a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Después de una conexión correcta, una jerarquía de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] bases de datos aparece en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Explorador de metadatos. Después de convertir los esquemas de acceso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] esquemas, puede seleccionar los esquemas convertidos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] el Explorador de metadatos y, a continuación, cargar los esquemas en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
Si ha seleccionado la base de datos de SQL Azure de la migración a la lista desplegable en el cuadro de diálogo nuevo proyecto, debe conectarse a la base de datos de SQL Azure. Después de una conexión correcta, una jerarquía de las bases de datos de la base de datos de SQL Azure aparece en el Explorador de metadatos de base de datos de SQL Azure. Después de convertir los esquemas de acceso a los esquemas de base de datos de SQL Azure, puede seleccionar los esquemas convertidos en el Explorador de metadatos de base de datos de SQL Azure y, a continuación, cargar los esquemas en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)].  
  
Después de cargar los esquemas convertidos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure, puede volver al explorador de metadatos de acceso y migrar datos desde bases de datos de Access en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o las bases de datos de la base de datos de SQL Azure. Si es necesario, también puede vincular tablas de Access a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o tablas de base de datos de SQL Azure.  
  
Para obtener más información sobre estas tareas y cómo realizarlas, vea los temas siguientes:  
  
-   [Preparar las bases de datos de acceso para la migración](http://msdn.microsoft.com/9b80a9e0-08e7-4b4d-b5ec-cc998d3f5114)  
  
-   [Migrar bases de datos de Access a SQL Server](http://msdn.microsoft.com/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  
-   [Vincular las aplicaciones de Access a SQL Server](http://msdn.microsoft.com/82374ad2-7737-4164-a489-13261ba393d4)  
  
Las secciones siguientes describen las características de la interfaz de usuario SSMA.  
  
### <a name="metadata-explorers"></a>Exploradores de metadatos  
SSMA contiene dos exploradores de metadatos que puede usar para examinar y realizar acciones en Access y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o las bases de datos de la base de datos de SQL Azure.  
  
#### <a name="access-metadata-explorer"></a>Obtener acceso al explorador de metadatos  
Explorador de metadatos de acceso muestra información acerca de las bases de datos de Access que se han agregado al proyecto. Cuando se agrega una base de datos de Access, SSMA recupera metadatos acerca de esa base de datos, los metadatos que están disponibles en el Explorador de metadatos de acceso.  
  
Puede usar el Explorador de metadatos de acceso para realizar las siguientes tareas:  
  
-   Examinar las tablas en cada base de datos de Access.  
  
-   Seleccionar objetos para la conversión y convertir los objetos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] sintaxis. Para obtener más información, consulte [convertir objetos de base de datos de Access](http://msdn.microsoft.com/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c).  
  
-   Seleccionar objetos para la migración de datos y migrar los datos de dichos objetos a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Para obtener más información, consulte [migrar datos de Access a SQL Server](http://msdn.microsoft.com/f3b18af7-1af0-499d-a00d-a0af94895625).  
  
-   Vinculación y desvinculación de acceso y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] tablas.  
  
#### <a name="sql-server-or-azure-sql-db-metadata-explorer"></a>SQL Server o el Explorador de metadatos de base de datos de SQL Azure  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]o el Explorador de metadatos de base de datos de SQL Azure muestra información sobre una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure. Cuando se conecta a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure, SSMA recupera metadatos acerca de esa instancia y lo almacena en el archivo de proyecto.  
  
Puede usar el servidor de SQL o el Explorador de metadatos de base de datos de SQL Azure para seleccionar objetos de base de datos convertidos de acceso y cargar (synchronize) esos objetos en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure.  
  
Para obtener más información, consulte [cargar objetos de base de datos para convertir a SQL Server](http://msdn.microsoft.com/4e854eee-b10c-4f0b-9d9e-d92416e6f2ba).  
  
### <a name="metadata"></a>Metadatos  
A la derecha de cada explorador de metadatos son las pestañas que describen el objeto seleccionado. Por ejemplo, si selecciona una tabla en el Explorador de metadatos de acceso, aparecen cuatro pestañas: **tabla**, **Type Mapping**, **propiedades**, y **datos**. Si selecciona una tabla en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] aparecen de explorador de metadatos, tres pestañas: **tabla**, **SQL**, y **datos**.  
  
Mayoría de los valores de metadatos es de solo lectura. Sin embargo, puede modificar los metadatos siguientes:  
  
-   En el Explorador de metadatos de acceso, puede modificar las asignaciones de tipos. Asegúrese de realizar estos cambios antes de crear informes o convertir esquemas.  
  
-   En [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] el Explorador de metadatos, puede modificar las propiedades de tabla e índice en el **tabla** ficha. Realice estos cambios antes de cargar los esquemas en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. Para obtener más información, consulte [convertir objetos de base de datos de Access](http://msdn.microsoft.com/e0ef67bf-80a6-4e6c-a82d-5d46e0623c6c).  
  
### <a name="toolbars"></a>Barras de herramientas  
SSMA tiene dos barras de herramientas: una barra de herramientas de proyecto y una barra de herramientas de migración.  
  
#### <a name="the-project-toolbar"></a>La barra de herramientas de proyecto  
La barra de herramientas de proyecto contiene botones para trabajar con proyectos, agregar archivos de base de datos de Access y conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure. Estos botones son similares a los comandos en el **archivo** menú.  
  
#### <a name="the-migration-toolbar"></a>La barra de herramientas de migración  
La barra de herramientas de migración contiene los siguientes comandos:  
  
|Botón|Función|  
|----------|------------|  
|**Convertir, cargar y migrar**|Convierte las bases de datos de Access, carga los objetos convertidos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure, y migra los datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] u DB de SQL Azure, en un solo paso.|  
|**Crear informe**|Convierte el esquema de acceso seleccionado para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o la sintaxis de la base de datos de SQL Azure y, a continuación, crea un informe que muestra cómo se realiza correctamente la conversión.<br /><br />Este comando está disponible sólo cuando se seleccionan objetos en el Explorador de metadatos de acceso.|  
|**Convertir esquema**|Convierte el esquema de acceso seleccionado para [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o esquemas de base de datos de SQL Azure.<br /><br />Este comando está disponible sólo cuando se seleccionan objetos en el Explorador de metadatos de acceso.|  
|**Migrar datos**|Migra los datos de la base de datos de Access a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure. Antes de ejecutar este comando, debe convertir los esquemas de acceso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o esquemas de base de datos de SQL Azure y, a continuación, cargar los objetos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure.<br /><br />Este comando está disponible sólo cuando se seleccionan objetos en el Explorador de metadatos de acceso.|  
|**Detener**|Detiene el proceso actual, como convertir objetos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o la sintaxis de la base de datos de SQL Azure.|  
  
### <a name="menus"></a>Menús  
SSMA contiene los siguientes menús:  
  
|Menú|Description|  
|--------|---------------|  
|**Archivo**|Contiene comandos para el Asistente para migración, trabajar con proyectos, agregar y quitar archivos de base de datos de Access y conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o base de datos de SQL Azure.|  
|**Editar**|Contiene comandos para buscar y trabajar con texto en las páginas de detalles, como copiar [!INCLUDE[tsql](../../includes/tsql_md.md)] desde el panel de detalles SQL. Para abrir el **administrar marcadores** cuadro de diálogo, en el menú Edición, haga clic en Administrar marcadores. En el cuadro de diálogo, verá una lista de los marcadores existentes. Puede usar los botones en el lado derecho del cuadro de diálogo para administrar los marcadores.|  
|**Ver**|Contiene el **sincronizar metadatos exploradores** comando. Esto sincroniza los objetos entre el Explorador de metadatos de acceso y [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o en el Explorador de metadatos de base de datos de SQL Azure. También contiene comandos para mostrar y ocultar el **salida** y **lista de errores** paneles y una opción **diseños** para administrar con los diseños.|  
|**Herramientas**|Contiene comandos para crear informes, exportar datos, migrar los objetos y datos, vincular tablas y proporciona acceso a global y la configuración de proyecto cuadros de diálogo.|  
|**Ayuda**|Proporciona acceso a la Ayuda de SSMA y a la **sobre** cuadro de diálogo.|  
  
### <a name="output-pane-and-error-list-pane"></a>Panel de resultados y el panel de lista de errores  
El **vista** menú proporciona comandos para alternar la visibilidad de los paneles de salida y la lista de errores:  
  
-   El panel de resultados muestra los mensajes de estado de SSMA durante la conversión de objetos, la sincronización de objetos y la migración de datos.  
  
-   El panel de lista de errores muestra mensajes informativos, de advertencia y de error en una lista que se puede ordenar.  
  
## <a name="see-also"></a>Vea también  
[Migrar bases de datos de Access a SQL Server](http://msdn.microsoft.com/76a3abcf-2998-4712-9490-fe8d872c89ca)  
  

