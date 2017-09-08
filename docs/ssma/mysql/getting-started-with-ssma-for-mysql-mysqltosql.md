---
title: "Introducción a SSMA para MySQL (MySQLToSQL) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.custom: 
ms.date: 01/19/2017
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
- Getting started, MySQL metadata explorer
- Getting started, SQL Server or SQL Azure metadata explorer
- Getting started,Installing and licensing
ms.assetid: 8ebfa061-be6f-4a07-923f-8dc832a82f70
caps.latest.revision: 19
author: Shamikg
ms.author: Shamikg
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 0b832a9306244210e693bde7c476269455e9b6d8
ms.openlocfilehash: 38ce5c0e27703094e4d7ff2415d0bc91d501d1b4
ms.contentlocale: es-es
ms.lasthandoff: 09/07/2017

---
# <a name="getting-started-with-ssma-for-mysql-mysqltosql"></a>Introducción a SSMA para MySQL (MySQLToSQL)
SQL Server Migration Assistant (SSMA) para MySQL le permite convertir esquemas de base de datos de MySQL a esquemas de SQL Server o base de datos de SQL Azure, cargar los esquemas resultantes en SQL Server o base de datos de SQL Azure y migrar datos de MySQL a SQL Server o base de datos de SQL Azure rápidamente.  
  
En este tema se presenta el proceso de instalación y, a continuación, le ayuda a familiarizarse con la interfaz de usuario SSMA.  
  
## <a name="installing-ssma"></a>Instalación de SSMA  
Para usar SSMA, primero debe instalar el programa de cliente SSMA en un equipo que puede tener acceso a la base de datos de MySQL de origen y la instancia de destino de SQL Server o base de datos de SQL Azure. A continuación, instale a los proveedores de MySQL (MySQL 5.1 el controlador ODBC (de confianza)) en el equipo que está ejecutando el programa de cliente de SSMA. Para obtener instrucciones de instalación, consulte [instalar SSMA para MySQL &#40; MySqlToSql &#41;](../../ssma/mysql/installing-ssma-for-mysql-mysqltosql.md)  
  
Para iniciar SSMA, haga clic en **iniciar**, seleccione **todos los programas**, seleccione **SQL Server Migration Assistant para MySQL**y, a continuación, haga clic en **SQL Server Migration Assistant para MySQL**.  
  
## <a name="ssma-for-mysql-user-interface"></a>SSMA para la interfaz de usuario de MySQL  
Después de SSMA se instala y se autoriza el uso de, puede usar SSMA para migrar bases de datos de MySQL a SQL Server o base de datos de SQL Azure. Ayuda para familiarizarse con la interfaz de usuario SSMA antes de empezar. El siguiente diagrama muestra la interfaz de usuario de SSMA, incluidos los exploradores de metadatos, metadatos, las barras de herramientas, panel de salida y panel de lista de error:  
  
![SSMA para la interfaz gráfica de usuario de MySql](../../ssma/mysql/media/ssmaformysqlgui.gif "SSMA para la interfaz gráfica de usuario de MySql")  
  
Para iniciar una migración, debe:  
  
1.  Cree un nuevo proyecto.  
  
2.  Conectarse a una base de datos de MySQL.  
  
3.  Después de una conexión correcta, los esquemas de MySQL aparecerá en el Explorador de metadatos de MySQL. Objetos de menú contextual en el Explorador de metadatos de MySQL para realizar tareas como crean informes que evalúa las conversiones a la base de datos de SQL de SQL Server o SQL Azure.  
  
También puede realizar estas tareas mediante el uso de las barras de herramientas y menús.  
  
También debe conectarse a una instancia de SQL Server. Después de una conexión correcta, aparecerá una jerarquía de bases de datos de SQL Server en el Explorador de metadatos de SQL Server. Después de convertir esquemas de MySQL a esquemas de SQL Server, seleccione dichos esquemas convertidos en el Explorador de metadatos de SQL Server y, a continuación, sincronizar los esquemas con SQL Server.  
  
Debe conectarse a la base de datos de SQL Azure si ha seleccionado la base de datos de SQL Azure de la migración a la lista desplegable en el cuadro de diálogo nuevo proyecto. Después de una conexión correcta, aparecerá una jerarquía de las bases de datos de la base de datos de SQL Azure en el Explorador de metadatos de base de datos de SQL Azure. Después de convertir esquemas de MySQL a esquemas de base de datos de SQL Azure, seleccione dichos esquemas convertidos en el Explorador de metadatos de base de datos de SQL Azure y, a continuación, sincronizar los esquemas con la base de datos de SQL Azure.  
  
Después de sincronizar esquemas convertidos con SQL Server o base de datos de SQL Azure, puede volver al explorador de metadatos de MySQL y migrar datos de esquemas de MySQL a las bases de datos de SQL Server o base de datos de SQL Azure.  
  
Para obtener más información sobre estas tareas y cómo realizarlas, vea [migrar bases de datos MySQL a SQL Server: base de datos de SQL de Azure &#40; MySQLToSql &#41; ](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md).  
  
Las secciones siguientes describen las características de la interfaz de usuario SSMA.  
  
### <a name="metadata-explorers"></a>Exploradores de metadatos  
SSMA contiene dos exploradores de metadatos para examinar y realizar acciones en las bases de datos de SQL Server y MySQL.  
  
### <a name="mysql-metadata-explorer"></a>Explorador de metadatos de MySQL  
Explorador de metadatos de MySQL muestra información acerca de los esquemas de MySQL. Mediante el Explorador de metadatos de MySQL, puede realizar las siguientes tareas:  
  
-   Examinar los objetos de cada esquema.  
  
-   Seleccionar objetos para la conversión y, a continuación, convertir los objetos a la sintaxis de SQL Server. Para obtener más información, vea [convertir bases de datos de MySQL &#40; MySQLToSQL &#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
-   Seleccionar tablas para la migración de datos y, a continuación, migrar los datos de esas tablas a SQL Server. Para obtener más información, vea [migrar datos de MySQL a SQL Server: base de datos de SQL de Azure &#40; MySQLToSQL &#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  
### <a name="sql-server-or-azure-sql-db-metadata-explorer"></a>SQL Server o el Explorador de metadatos de base de datos de SQL Azure  
SQL Server o el Explorador de metadatos de base de datos de SQL Azure muestra información sobre una instancia de SQL Server o base de datos de SQL Azure. Cuando se conecta a una instancia de SQL Server o base de datos de SQL Azure, SSMA recupera metadatos acerca de esa instancia y lo almacena en el archivo de proyecto.  
  
Puede usar el Explorador de metadatos para seleccionar objetos de base de datos de MySQL convertidos y, a continuación, sincroniza esos objetos con la instancia de SQL Server o base de datos de SQL Azure.  
  
Para obtener más información, vea [sincronización (MySQL a SQL Server / base de datos de SQL Azure)](http://msdn.microsoft.com/en-us/ac993a6d-0283-4823-8793-6b217677dfa3)  
  
### <a name="metadata"></a>Metadatos  
A la derecha de cada explorador de metadatos son las pestañas que describen el objeto seleccionado. Por ejemplo, si selecciona una tabla en el Explorador de metadatos de MySQL, nueve aparecerán fichas: **tabla**, **SQL**, **Type Mapping**, **datos**, **configuración**, **Charset asignación**, **modos de SQL**, **propiedades**, y **informe**. El **informe** pestaña contiene información únicamente después de crear un informe que contiene el objeto seleccionado. Si selecciona una tabla en el Explorador de metadatos de SQL Server, aparecerán tres fichas: **tabla**, **SQL** y **datos**.  
  
Mayoría de los valores de metadatos es de solo lectura. Sin embargo, puede modificar los metadatos siguientes:  
  
-   En el Explorador de metadatos de MySQL, puede modificar las asignaciones de tipos, asignación de conjunto de caracteres, modos de SQL. Para convertir las asignaciones de tipos modificada o asignación de conjunto de caracteres o modos de SQL, realizar cambios antes de convertir esquemas.  
  
-   En el Explorador de metadatos de SQL Server, puede modificar las propiedades de tabla e índice en la pestaña de tabla. Para ver estos cambios en SQL Server, realice estos cambios antes de cargar los esquemas en SQL Server.  
  
Los cambios realizados en el Explorador de metadatos se reflejan en los metadatos del proyecto, no en las bases de datos de origen o de destino.  
  
### <a name="toolbars"></a>Barras de herramientas  
SSMA tiene dos barras de herramientas: una barra de herramientas de proyecto y una barra de herramientas de migración.  
  
### <a name="the-project-toolbar"></a>La barra de herramientas de proyecto  
La barra de herramientas de proyecto contiene botones para trabajar con proyectos, conectar con MySQL y conectarse a SQL Server o base de datos de SQL Azure. Estos botones son similares a los comandos en el **archivo** menú.  
  
### <a name="migration-toolbar"></a>Barra de herramientas de migración  
La siguiente tabla muestra los comandos de barra de herramientas de la migración:  
  
|||  
|-|-|  
|**Botón**|**Función**|  
|**Crear informe**|Convierte los objetos seleccionados de MySQL a SQL Server o base de datos de SQL Azure objetos y, a continuación, crea un informe que muestra cómo se realiza correctamente la conversión.<br /><br />Este comando está deshabilitado a menos que se seleccionan objetos en el Explorador de metadatos de MySQL.|  
|**Convertir esquema**|Convierte los objetos seleccionados de MySQL a los objetos de SQL Server o base de datos de SQL Azure.<br /><br />Este comando está deshabilitado a menos que se seleccionan objetos en el Explorador de metadatos de MySQL.|  
|**Migrar datos**|Migra los datos de la base de datos de MySQL a SQL Server o base de datos de SQL Azure. Antes de ejecutar este comando, debe convertir los esquemas de MySQL a esquemas de SQL Server o base de datos de SQL Azure y, a continuación, cargar los objetos en SQL Server o base de datos de SQL Azure.<br /><br />Este comando está deshabilitado a menos que se seleccionan objetos en el Explorador de metadatos de MySQL.|  
|**Detener**|Detiene el proceso actual.|  
  
### <a name="menus"></a>Menús  
La siguiente tabla muestra los menús SSMA.  
  
|||  
|-|-|  
|**Menú**|**Description**|  
|**Archivo**|Contiene comandos para trabajar con proyectos, conectar con MySQL y conectarse a SQL Server o base de datos de SQL Azure.|  
|**Editar**|Contiene comandos para buscar y trabajar con texto en las páginas de detalles. Para abrir **administrar marcadores** cuadro de diálogo, en el menú Edición, haga clic en Administrar marcadores. En el cuadro de diálogo verá una lista de los marcadores existentes. Puede usar los botones en el lado derecho del cuadro de diálogo para administrar los marcadores.|  
|**Ver**|Contiene el **sincronizar metadatos exploradores** comando. Sincroniza los objetos entre el Explorador de metadatos de MySQL y SQL Server o el Explorador de metadatos de base de datos de SQL Azure. También contiene comandos para mostrar y ocultar el **salida** y **lista de errores** paneles y una opción **diseños** para administrar con los diseños.|  
|**Herramientas**|Contiene comandos para crear informes, convertir el esquema, actualizar desde la base de datos, migrar objetos y los datos y guardar como secuencia de comandos. También proporciona acceso a la **configuración Global, la configuración predeterminada del proyecto** y **configuración del proyecto** cuadros de diálogo.|  
|**Ayuda**|Proporciona acceso a la Ayuda de SSMA y a la **sobre** cuadro de diálogo.|  
  
### <a name="output-pane-and-error-list-pane"></a>Panel de resultados y el panel de lista de errores  
El **vista** menú proporciona comandos para alternar la visibilidad de los paneles de salida y la lista de errores:  
  
-   El panel de resultados muestra los mensajes de estado de SSMA durante la conversión de objetos, la sincronización de objetos y la migración de datos.  
  
-   El panel de lista de errores muestra mensajes informativos, de advertencia y de error en una lista que se puede ordenar.  
  
## <a name="see-also"></a>Vea también  
[Referencia de la interfaz de usuario &#40; MySQLToSQL &#41;](../../ssma/mysql/user-interface-reference-mysqltosql.md)  
[Migrar datos de MySQL a SQL Server: base de datos de SQL Azure &#40; MySQLToSQL &#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  

