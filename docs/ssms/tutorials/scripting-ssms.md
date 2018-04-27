---
Title: 'Tutorial: Script Objects in SQL Server Management Studio'
description: Tutorial para crear scripts de objetos en SSMS.
keywords: SQL Server, SSMS, SQL Server Management Studio, scripts, scripting
author: MashaMSFT
ms.author: mathoma
ms.date: 03/13/2018
ms.topic: Tutorial
ms.suite: sql
ms.prod_service: sql-tools
ms.reviewer: sstein
manager: craigg
helpviewer_keywords:
- projects [SQL Server Management Studio], tutorials
- source controls [SQL Server Management Studio], tutorials
- Help [SQL Server], SQL Server Management Studio
- tutorials [SQL Server Management Studio]
- Transact-SQL tutorials
- solutions [SQL Server Management Studio], tutorials
- SQL Server Management Studio [SQL Server], tutorials
- scripts [SQL Server], SQL Server Management Studio
ms.openlocfilehash: a931ddb3cf3229970de4b301e18002484acbaf53
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="tutorial-script-objects-in-sql-server-management-studio"></a>Tutorial: Crear scripts de objetos en SQL Server Management Studio
En este tutorial aprenderá a generar scripts de Transact-SQL (T-SQL) para distintos objetos de SQL Server Management Studio.  En este tutorial encontrará ejemplos de cómo crear scripts de los siguientes objetos: 

> [!div class="checklist"]
> * Consultas al llevar a cabo acciones en la GUI
> * Bases de datos de dos formas diferentes ("Script As" [Generar script como] y "Generar script")
> * Tablas
> * Procedimientos almacenados
> * Eventos extendidos

El resumen de este tutorial es que se pueden crear scripts de todos los objetos del **Explorador de objetos**. Para ello, se debe hacer clic con el botón derecho en un objeto y seleccionar la opción **Generar script de objeto como**. 


## <a name="prerequisites"></a>Prerequisites
Para llevar a cabo este tutorial necesita tener SQL Server Management Studio, acceso a un servidor SQL Server y una base de datos de AdventureWorks. 

- Instale [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms).
- Instale [SQL Server 2017 Developer Edition](https://www.microsoft.com/en-us/sql-server/sql-server-downloads).
- Descargue [bases de datos de ejemplo de AdventureWorks2016](https://github.com/Microsoft/sql-server-samples/releases). Aquí encontrará instrucciones para restaurar bases de datos en SSMS: [Restaurar una base de datos](https://docs.microsoft.com/en-us/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms). 


## <a name="script-queries-from-gui"></a>Crear scripts de consultas desde la interfaz gráfica de usuario
Siempre que lleve a cabo una tarea con la interfaz gráfica de usuario (GUI) en SSMS, también puede generar el código de T-SQL asociado a esa tarea. En los siguientes ejemplos se muestra cómo hacerlo al hacer una copia de seguridad de una base de datos y al reducir el registro de transacciones.  Estos mismos pasos se pueden aplicar a cualquier acción que se lleve a cabo con la GUI. 

### <a name="script-t-sql-when-backing-up-a-database"></a>Creación de un script de T-SQL al hacer una copia de seguridad de una base de datos
1. Conéctese a su servidor SQL Server.
2. Expanda el nodo **Bases de datos** .
3. Haga clic con el botón derecho en la base de datos **Adventureworks2016** > **Tareas** > **Hacer una copia de seguridad**:

    ![Hacer una copia de seguridad de una base de datos](media/scripting-ssms/backupdb.png)

4. Configure la copia de seguridad del modo que quiera. Para este tutorial, se ha dejado todo en los valores predeterminados, aunque todos los cambios efectuados en la ventana también se verán reflejados en el script. 
5. Seleccione la opción **Generar script** > **Generar script de acción en la ventana de consulta**:
 
    ![Crear un script de la copia de seguridad de la base de datos](media/scripting-ssms/scriptdbbackup.PNG)
6. Revise el código T-SQL rellenado en la ventana de consulta: 

    ![Script para la copia de seguridad de la base de datos](media/scripting-ssms/dbbackupscript.PNG)
7. Seleccione **Ejecutar** para ejecutar la consulta para hacer una copia de seguridad de la base de datos mediante T-SQL. 


### <a name="script-t-sql-when-shrinking-the-transaction-log"></a>Crear un script de T-SQL al reducir el registro de transacciones
1. Haga clic con el botón derecho en la base de datos **AdventureWorks2016** > **Tareas** > **Reducir** > **Archivos**:

     ![Reducir archivos](media/scripting-ssms/shrinkfiles.png)

2. Seleccione **Registro** en la lista desplegable **Tipo de archivo**:

    ![Reducir el registro de transacciones](media/scripting-ssms/shrinktlog.png)

3. Seleccione las opciones **Generar script** y **Generar script de acción en Portapapeles**:

    ![Generar script en Portapapeles](media/scripting-ssms/scriptactiontoclipboard.png)

4. Abra una ventana de **nueva consulta** y seleccione Pegar (haga clic con el botón derecho en la ventana > **Pegar**):

    ![Pegar el script](media/scripting-ssms/paste.png)
5. Seleccione **Ejecutar** para ejecutar la consulta y reducir el registro de transacciones. 


## <a name="script-databases"></a>Creación un script de bases de datos
En la siguiente sección se describe cómo crear un script de la base de datos con la opción **Script As** (Generar script como) y con la opción **Generar scripts**.  Con la opción **Script As** (Generar script como) se volverán a crear las opciones de base de datos y de configuración para este. La opción **Generar scripts** le permitirá generar un script para el esquema y los datos. En esta sección, creará dos bases de datos: *AdventureWorks2016a*, que se creará usando la opción **Generar script como**, y *AdventureWorks2016b*, que se creará usando la opción **Generar scripts**. 


### <a name="script-database-using-script-option"></a>Crear un script de base de datos con la opción Script
1. Conéctese a su servidor SQL Server.
2. Expanda el nodo **Bases de datos** .
3. Haga clic con el botón derecho en la base de datos **AdventureWorks2016** > **Generar script de base de datos como** > **Crear en** > **Nueva ventana de consulta**:

    ![Crear un script de base de datos](media/scripting-ssms/scriptdb.png)

4. Revise la consulta de creación de la base de datos en la ventana: 

    ![Base de datos con script generado](media/scripting-ssms/scriptedoutdb.png)
    - Esta opción solo creará un script de las opciones de configuración de la base de datos.
5. En el teclado, presione **Ctrl+F** para abrir el cuadro de diálogo **Buscar** y seleccione la flecha abajo para abrir la opción **Reemplazar**. En la línea superior de **Buscar**, escriba *AdventureWorks2016*; en la línea inferior de **Reemplazar**, escriba *AdventureWorks2016a*. 
6. Seleccione **Reemplazar todo** para reemplazar todas las instancias de *AdventureWorks2016* por *AdventureWorks2016a*. 

    ![Buscar y reemplazar](media/scripting-ssms/findandreplace.png)

1. Seleccione **Ejecutar** para ejecutar la consulta y crear la nueva base de datos *AdventureWorks2016a*. 

### <a name="script-database-using-generate-scripts-option"></a>Crear un script de base de datos con la opción Generar scripts
1. Conéctese a su servidor SQL Server.
2. Expanda el nodo **Bases de datos** .
3. Haga clic con el botón derecho en la base de datos **AdventureWorks2016** > **Tareas** > **Generar scripts**:

    ![Generar scripts para una base de datos](media/scripting-ssms/generatescriptsfordb.png)

4. Se abrirá la página **Introducción**. Seleccione **Siguiente** para abrir la página **Elegir objetos**. Puede seleccionar toda la base de datos o determinados objetos. Seleccione la opción **Generar script de toda la base de datos y todos sus objetos** 
 
    ![Generar scripts para objetos](media/scripting-ssms/scriptobjects.png)
 
5. Seleccione **Siguiente** para abrir la página **Establecer opciones de scripting**, que le permitirá configurar la ubicación de guardado del script, así como otras opciones avanzadas adicionales. 

    A. Seleccione la opción **Guardar en nueva ventana de consulta**. 

    B. Seleccione **Opciones avanzadas** y compruebe que estas opciones estén establecidas de la siguiente manera: 

      - **Generar script de estadísticas** en *Generar script de estadísticas*
      - **Tipos de datos que se deben incluir en el script** en *Solo esquema*
      - **Generar script de índices** en *true*

   ![Generar script de objetos](media/scripting-ssms/advancedscripts.png)

   > [!NOTE]
   > Puede generar un script de los datos para la base de datos seleccionando *Esquema y datos* para la opción **Tipos de datos que se deben incluir en el script**. Sin embargo, esta opción no es la recomendada para bases de datos grandes, ya que puede ocupar más memoria de la que SSMS es capaz de asignar. Esta opción es válida para bases de datos pequeñas. Sim embargo, si quiere mover datos para una base de datos de mayor tamaño, le recomendamos que use el [Asistente para importación y exportación](https://docs.microsoft.com/en-us/sql/integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard).



1. Seleccione **Aceptar** y **Siguiente**. 
2. Seleccione **Siguiente** en **Resumen** y, después, vuelva a seleccionar **Siguiente** para generar el script en una ventana de **consulta nueva**.  
3. En el teclado, presione **Ctrl+F** para abrir el cuadro de diálogo **Buscar** y seleccione la flecha abajo para abrir la opción **Reemplazar**. En la línea superior de **Buscar**, escriba *AdventureWorks2016*; en la línea inferior de **Reemplazar**, escriba *AdventureWorks2016b*. 
    A. Seleccione **Reemplazar todo** para reemplazar todas las instancias de *AdventureWorks2016* por *AdventureWorks2016b*. 

    ![AdventureWorks2016b](media/scripting-ssms/adventureworks2016b.png)
7. Seleccione **Ejecutar** para ejecutar la consulta y crear la nueva base de datos *AdventureWorks2016b*. 
 
## <a name="script-tables"></a>Crear scripts de tablas
En esta sección se explica cómo crear scripts de tablas de la base de datos. Esta opción le permite crear la tabla, o bien anularla y volver a crearla. También puede usar esta opción para generar un script T-SQL asociado a la modificación de la tabla para, por ejemplo, insertar o actualizar contenido en esta. En esta sección, anulará una tabla y volverá a crearla. 

1. Conéctese a su servidor SQL Server.
2. Expanda el nodo **Bases de datos**.
3. Expanda el nodo de la base de datos **AdventureWorks**. 
4. Expanda el nodo **Tablas**.
5. Haga clic con el botón derecho en **dbo.ErrorLog** >  **Generar script de la tabla como** > **Anular y crear en** > **Nueva ventana del Editor de consultas**:
    
    ![Incluir tabla](media/scripting-ssms/scripttable.png)

6. Seleccione **Ejecutar** para ejecutar una consulta; se anulará la tabla *Errorlog* y se volverá a crear. 

    >[!NOTE]
    > De forma predeterminada, la tabla *Errorlog* está vacía en la base de datos AdventureWorks2016, de modo que no perderá ningún dato al anularla. Sin embargo, seguir estos pasos para una tabla que contenga datos provocará la pérdida de estos. 
 
## <a name="script-stored-procedures"></a>Crear scripts de procedimientos almacenados
En esta sección, obtendrá información sobre cómo anular y crear un procedimiento almacenado.  

1. Conéctese a su servidor SQL Server.
2. Expanda el nodo **Bases de datos**.
3. Expanda el nodo **Programación**. 
4. Expanda el nodo **Procedimiento almacenado**.
5. Haga clic con el botón derecho en el procedimiento almacenado **dbo.uspGetBillOfMaterials**> **Generar script de procedimiento almacenado como** > **Anular y crear en** > **Nueva ventana de consulta**:
    
    ![Crear scripts de procedimientos almacenados](media/scripting-ssms/scriptstoredprocedure.PNG)

## <a name="script-extended-events"></a>Crear scripts de eventos extendidos
En esta sección se explica cómo crear scripts de [eventos extendidos](https://docs.microsoft.com/en-us/sql/relational-databases/extended-events/extended-events). 

1. Conéctese a su servidor SQL Server.
2. Expanda el nodo **Administración**.
3. Expanda el nodo **Eventos extendidos**.
4. Expanda el nodo **Sesiones**.
5. Haga clic con el botón derecho en la sesión extendida que le interese > **Generar script de sesión como** > **Nueva ventana del Editor de consultas**:

    ![Crear scripts de XEvents](media/scripting-ssms/scriptxevents.png) 
6. En la **nueva ventana de consulta**, cambie el nuevo nombre de la sesión (*system_health*) por *system_health2* y seleccione **Ejecutar** para ejecutar la consulta. 

    A. Haga clic con el botón derecho en **Sesiones** en el **Explorador de objetos** y seleccione **Actualizar** para ver la nueva sesión de eventos extendidos. El icono verde situado junto a la sesión indica que la sesión se está ejecutando, mientras que el icono rojo indica que se ha detenido. 

    ![Nuevo valor xEvent](media/scripting-ssms/newxevent.png)

    >[!NOTE]
    > Puede iniciar sesión haciendo clic en la sesión y seleccionando **Iniciar**. Sin embargo, puesto que se trata de una copia de la sesión *system_health* en ejecución, puede omitir este paso. Puede eliminar la copia de la sesión de eventos extendidos haciendo clic en esta y seleccionando **Eliminar**. 

## <a name="next-steps"></a>Pasos siguientes
En el siguiente artículo se presentan las plantillas T-SQL predefinidas de SSMS. 

Vaya al siguiente artículo para obtener más información:
> [!div class="nextstepaction"]
> [Pasos siguientes](templates-ssms.md)


