---
title: Introducción a SSMA para MySQL (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
helpviewer_keywords:
- Getting started, MySQL metadata explorer
- Getting started, SQL Server or SQL Azure metadata explorer
- Getting started,Installing and licensing
ms.assetid: 8ebfa061-be6f-4a07-923f-8dc832a82f70
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 1ae91f90bf601e4ef17ae2f363260dbb47a2822e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63187152"
---
# <a name="getting-started-with-ssma-for-mysql-mysqltosql"></a>Introducción a SSMA para MySQL (MySQLToSQL)
SQL Server Migration Assistant (SSMA) para MySQL le permite convertir los esquemas de base de datos MySQL a esquemas de SQL Server o Azure SQL DB, cargar los esquemas resultantes en SQL Server o Azure SQL DB y migrar datos desde MySQL a SQL Server o Azure SQL DB rápidamente.  
  
En este tema presenta el proceso de instalación y, a continuación, le ayuda a familiarizarse con la interfaz de usuario SSMA.  
  
## <a name="installing-ssma"></a>Instalación de SSMA  
Para usar SSMA, primero debe instalar el programa de cliente SSMA en un equipo que puede tener acceso a la base de datos de MySQL de origen y la instancia de destino de SQL Server o Azure SQL DB. A continuación, instale a los proveedores de MySQL (controlador ODBC de MySQL 5.1 (de confianza)) en el equipo que ejecuta el programa de cliente de SSMA. Para obtener instrucciones de instalación, consulte [instalar SSMA para MySQL &#40;MySqlToSql&#41;](../../ssma/mysql/installing-ssma-for-mysql-mysqltosql.md)  
  
Para iniciar SSMA, haga clic en **iniciar**, apunte a **todos los programas**, apunte a **SQL Server Migration Assistant para MySQL**y, a continuación, haga clic en **migración a SQL Server El Asistente para MySQL**.  
  
## <a name="ssma-for-mysql-user-interface"></a>SSMA para la interfaz de usuario de MySQL  
Después de instalar SSMA y con licencia, puede usar SSMA para migrar bases de datos MySQL a SQL Server o Azure SQL DB. Ayuda a familiarizarse con la interfaz de usuario SSMA antes de empezar. El siguiente diagrama muestra la interfaz de usuario de SSMA, incluidos los exploradores de los metadatos, metadatos, las barras de herramientas, panel de salida y panel de lista de errores:  
  
![SSMA para la interfaz gráfica de usuario de MySql](../../ssma/mysql/media/ssmaformysqlgui.gif "SSMA para la interfaz gráfica de usuario de MySql")  
  
Para iniciar una migración, debe:  
  
1.  Cree un nuevo proyecto.  
  
2.  Conectarse a una base de datos MySQL.  
  
3.  Después de una conexión correcta, los esquemas de MySQL aparecerá en el Explorador de metadatos de MySQL. Objetos de botón derecho en el Explorador de metadatos de MySQL para realizar tareas como crean informes que evaluación las conversiones a SQL Server, Azure SQL DB.  
  
También puede realizar estas tareas mediante el uso de los menús y barras de herramientas.  
  
También debe conectarse a una instancia de SQL Server. Después de una conexión correcta, aparece una jerarquía de bases de datos de SQL Server en el Explorador de metadatos de SQL Server. Después de convertir los esquemas de MySQL a esquemas de SQL Server, seleccione esos esquemas convertidos en el Explorador de metadatos de SQL Server y, a continuación, sincronizar los esquemas con SQL Server.  
  
Si ha seleccionado la base de datos de SQL Azure de la migración en la lista desplegable en el cuadro de diálogo nuevo proyecto debe conectarse a Azure SQL DB. Después de una conexión correcta, una jerarquía de bases de datos de Azure SQL DB aparecerá en el Explorador de metadatos de Azure SQL DB. Después de convertir los esquemas de MySQL a esquemas de base de datos de SQL Azure, seleccione esos esquemas convertidos en el Explorador de metadatos de Azure SQL DB y, a continuación, sincronizar los esquemas con Azure SQL DB.  
  
Después de sincronizar esquemas convertidos con SQL Server o Azure SQL DB, puede volver al explorador de metadatos de MySQL y migrar datos de esquemas de MySQL a las bases de datos de SQL Server o Azure SQL DB.  
  
Para obtener más información sobre estas tareas y cómo realizarlas, vea [migrar bases de datos MySQL a SQL Server: Azure SQL DB &#40;MySQLToSql&#41;](../../ssma/mysql/migrating-mysql-databases-to-sql-server-azure-sql-db-mysqltosql.md).  
  
Las siguientes secciones describen las características de la interfaz de usuario SSMA.  
  
### <a name="metadata-explorers"></a>Exploradores de metadatos  
SSMA contiene dos exploradores de los metadatos para examinar y realizar acciones en las bases de datos MySQL y SQL Server.  
  
### <a name="mysql-metadata-explorer"></a>Explorador de metadatos de MySQL  
Explorador de metadatos de MySQL muestra información acerca de los esquemas de MySQL. Mediante el Explorador de metadatos de MySQL, puede realizar las siguientes tareas:  
  
-   Examinar los objetos de cada esquema.  
  
-   Seleccionar objetos para la conversión y, a continuación, convertir los objetos en la sintaxis de SQL Server. Para obtener más información, consulte [convertir las bases de datos de MySQL &#40;MySQLToSQL&#41;](../../ssma/mysql/converting-mysql-databases-mysqltosql.md)  
  
-   Seleccionar tablas para la migración de datos y, a continuación, migrar los datos de esas tablas en SQL Server. Para obtener más información, consulte [migrar datos de MySQL a SQL Server: Azure SQL DB &#40;MySQLToSQL&#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  
### <a name="sql-server-or-azure-sql-db-metadata-explorer"></a>SQL Server o el Explorador de metadatos de base de datos de SQL Azure  
SQL Server o el Explorador de metadatos de base de datos SQL de Azure muestra información sobre una instancia de SQL Server o Azure SQL DB. Cuando se conecta a una instancia de SQL Server o Azure SQL DB, SSMA recupera los metadatos sobre esa instancia y lo almacena en el archivo de proyecto.  
  
Puede usar el Explorador de metadatos para seleccionar los objetos de base de datos MySQL convertidos y, a continuación, sincroniza esos objetos con la instancia de SQL Server o Azure SQL DB.  
  
Para obtener más información, consulte [sincronización (MySQL a SQL Server / base de datos de SQL Azure)](https://msdn.microsoft.com/ac993a6d-0283-4823-8793-6b217677dfa3)  
  
### <a name="metadata"></a>Metadatos  
A la derecha de cada explorador de metadatos son las pestañas que describen el objeto seleccionado. Por ejemplo, si selecciona una tabla en el Explorador de metadatos de MySQL, aparecerán las pestañas de nueve: **Tabla**, **SQL**, **asignación de tipos de**, **datos**, **configuración**, **Charset asignación**, **Modos SQL**, **propiedades**, y **informe**. El **informe** pestaña contiene información únicamente después de crear un informe que contiene el objeto seleccionado. Si selecciona una tabla en el Explorador de metadatos de SQL Server, aparecerán tres fichas: **Tabla**, **SQL** y **datos**.  
  
La mayoría de los metadatos configuración es de solo lectura. Sin embargo, puede modificar los metadatos siguientes:  
  
-   En el Explorador de metadatos de MySQL, puede modificar asignaciones de tipos, asignación de juego de caracteres, los modos de SQL. Para convertir las asignaciones de tipos modificados o asignación de juego de caracteres o modos de SQL, realice los cambios antes de convertir los esquemas.  
  
-   En el Explorador de metadatos de SQL Server, puede modificar las propiedades de tabla e índice en la pestaña de tabla. Para ver estos cambios en SQL Server, realice estos cambios antes de cargar los esquemas en SQL Server.  
  
Los cambios realizados en el Explorador de metadatos se reflejan en los metadatos del proyecto, no en las bases de datos de origen o destino.  
  
### <a name="toolbars"></a>Barras de herramientas  
SSMA tiene dos barras de herramientas: una barra de herramientas de proyecto y una barra de herramientas de migración.  
  
### <a name="the-project-toolbar"></a>La barra de herramientas de proyecto  
La barra de herramientas de proyecto contiene botones para trabajar con proyectos, conectar con MySQL y conectarse a SQL Server o Azure SQL DB. Estos botones son similares a los comandos en el **archivo** menú.  
  
### <a name="migration-toolbar"></a>Barra de herramientas de migración  
La siguiente tabla muestra los comandos de la barra de herramientas de la migración:  
  
|||  
|-|-|  
|**Button**|**Función**|  
|**Crear informe**|Convierte los objetos seleccionados de MySQL a SQL Server o Azure SQL DB objetos y, a continuación, crea un informe que muestra cómo se realiza correctamente la conversión.<br /><br />Este comando está deshabilitado a menos que los objetos seleccionados en el Explorador de metadatos de MySQL.|  
|**Convertir esquema**|Convierte los objetos seleccionados de MySQL a SQL Server o Azure SQL DB objetos.<br /><br />Este comando está deshabilitado a menos que los objetos seleccionados en el Explorador de metadatos de MySQL.|  
|**Migración de datos**|Migra los datos de la base de datos MySQL a SQL Server o Azure SQL DB. Antes de ejecutar este comando, debe convertir los esquemas de MySQL a esquemas de SQL Server o Azure SQL DB y, a continuación, cargar los objetos en SQL Server o Azure SQL DB.<br /><br />Este comando está deshabilitado a menos que los objetos seleccionados en el Explorador de metadatos de MySQL.|  
|**Detener**|Detiene el proceso actual.|  
  
### <a name="menus"></a>Menús  
La siguiente tabla muestra los menús SSMA.  
  
|||  
|-|-|  
|**Menú**|**Descripción**|  
|**Archivo**|Contiene comandos para trabajar con proyectos, conectar con MySQL y conectarse a SQL Server o Azure SQL DB.|  
|**Editar**|Contiene comandos para buscar y trabajar con texto en las páginas de detalles. Para abrir **administrar marcadores** cuadro de diálogo, en el menú Edición, haga clic en Administrar marcadores. En el cuadro de diálogo, verá una lista de los marcadores existentes. Puede usar los botones en el lado derecho del cuadro de diálogo para administrar los marcadores.|  
|**Vista**|Contiene el **sincronizar metadatos Explorers** comando. Sincroniza los objetos entre el Explorador de metadatos de MySQL y SQL Server o el Explorador de metadatos de Azure SQL DB. También contiene comandos para mostrar y ocultar el **salida** y **lista de errores** paneles y una opción **diseños** para administrar con los diseños.|  
|**Herramientas**|Contiene comandos para crear informes, convertir el esquema, actualizar desde la base de datos, migrar objetos y los datos y guardar como secuencia de comandos. También proporciona acceso a la **configuración Global, la configuración predeterminada del proyecto** y **configuración del proyecto** cuadros de diálogo.|  
|**Ayuda**|Proporciona acceso para ayudar a SSMA y a la **sobre** cuadro de diálogo.|  
  
### <a name="output-pane-and-error-list-pane"></a>Panel de salida y el panel de lista de errores  
El **vista** menú proporciona comandos para alternar la visibilidad de los paneles de salida y el panel de lista de errores:  
  
-   El panel de resultados muestra los mensajes de estado de SSMA durante la conversión de objetos, la sincronización del objeto y migración de datos.  
  
-   El panel de lista de errores, muestra un error, advertencia y mensajes informativos en una lista clasificable.  
  
## <a name="see-also"></a>Vea también  
[Referencia de la interfaz de usuario &#40;MySQLToSQL&#41;](../../ssma/mysql/user-interface-reference-mysqltosql.md)  
[Migrar datos de MySQL a SQL Server: base de datos SQL Azure &#40;MySQLToSQL&#41;](../../ssma/mysql/migrating-mysql-data-into-sql-server-azure-sql-db-mysqltosql.md)  
  
