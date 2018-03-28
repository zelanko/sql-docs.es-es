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
ms.openlocfilehash: 2ee56bc26c22f91af7bf156ea967c19b61eab881
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/21/2018
---
# <a name="tutorial-script-objects-in-sql-server-management-studio"></a>Tutorial: Crear scripts de objetos en SQL Server Management Studio
En este tutorial aprenderá a generar scripts de Transact-SQL (T-SQL) para distintos objetos de SQL Server Management Studio.  En este tutorial encontrará ejemplos de cómo crear scripts de los siguientes objetos: 
 - Consultas al llevar a cabo acciones en la GUI
 - Bases de datos de dos formas diferentes ("Script As" [Generar script como] y "Generar script")
 - Tablas
 - Procedimientos almacenados
 - Eventos extendidos

El resumen de este tutorial es que se pueden crear scripts de todos los objetos del **Explorador de objetos**. Para ello, se debe hacer clic con el botón derecho en un objeto y seleccionar la opción **Script Object As** (Crear script de objeto como). 


## <a name="prerequisites"></a>Prerequisites
Para llevar a cabo este tutorial necesita tener SQL Server Management Studio, acceso a un servidor SQL Server y una base de datos de AdventureWorks. 

- Instale [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms).
- Instale [SQL Server 2017 Developer Edition](https://www.microsoft.com/en-us/sql-server/sql-server-downloads).
- Descargar una [Base de datos de ejemplo AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases). 
    - Aquí encontrará instrucciones para restaurar bases de datos en SSMS: [Restaurar una base de datos](https://docs.microsoft.com/en-us/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms). 


## <a name="script-queries-from-gui"></a>Crear scripts de consultas desde la interfaz gráfica de usuario
Siempre que lleve a cabo una tarea con la interfaz gráfica de usuario (GUI) en SSMS, también puede generar el código de T-SQL asociado a esa tarea. En los siguientes ejemplos se muestra cómo hacerlo al hacer una copia de seguridad de una base de datos y al reducir el registro de transacciones.  Estos mismos pasos se pueden aplicar a cualquier acción que se lleve a cabo con la GUI. 

### <a name="scriptt-sql-when-backing-up-a-database"></a>Crear un script de T-SQL al hacer una copia de seguridad de una base de datos
1. Conéctese a su servidor SQL Server.
2. Expanda el nodo **Bases de datos** .
3. Haga clic con el botón derecho en la base de datos > **Tareas** > **Copia de seguridad**:

    ![Hacer una copia de seguridad de una base de datos](media/scripting-ssms/backupdb.png)

4. Configure la copia de seguridad del modo que quiera. Para este tutorial se ha dejado todo en los valores predeterminados, aunque todos los cambios efectuados en la ventana también se verán reflejados en el script. 
5. Haga clic en la opción **Script** > **Script Action to Query Window** (Generar script de acción en Nueva ventana de consulta):
 
    ![Crear un script de la copia de seguridad de la base de datos](media/scripting-ssms/scriptdbbackup.PNG)
6. Revise el código T-SQL rellenado en la ventana de consulta: 

    ![Script para la copia de seguridad de la base de datos](media/scripting-ssms/dbbackupscript.PNG)


### <a name="script-t-sql-when-shrinking-the-transaction-log"></a>Crear un script de T-SQL al reducir el registro de transacciones
1. Haga clic con el botón derecho en la base de datos > **Tareas** > **Reducir** > **Archivos**:

     ![Reducir archivos](media/scripting-ssms/shrinkfiles.png)

2. Seleccione **Registro** en la lista desplegable **Tipo de archivo**:

    ![Reducir el registro de transacciones](media/scripting-ssms/shrinktlog.png)

3. Haga clic en la opción **Script** y en **Generar script de acción en Portapapeles**:

    ![Generar script en Portapapeles](media/scripting-ssms/scriptactiontoclipboard.png)

4. Abra una ventana de **nueva consulta** y seleccione Pegar (haga clic con el botón derecho en la ventana > **Pegar**):

    ![Pegar el script](media/scripting-ssms/paste.png)


## <a name="script-databases"></a>Crear un script de bases de datos
En la siguiente sección se describe cómo crear un script de la base de datos con la opción **Script As** (Generar script como) y con la opción **Generar scripts**.  Con la opción **Script As** (Generar script como) se volverán a crear las opciones de base de datos y de configuración para este. Con la opción **Generar scripts** se crearán scripts de todos los objetos de la base de datos, pero no de los datos. Para incluir los datos en el script, deberá usar el [Asistente para importación y exportación](https://docs.microsoft.com/en-us/sql/integration-services/import-export-data/start-the-sql-server-import-and-export-wizard).  


### <a name="script-database-using-script-option"></a>Crear un script de base de datos con la opción Script
1. Conéctese a su servidor SQL Server.
2. Expanda el nodo **Bases de datos** .
3. Haga clic con el botón derecho en la base de datos > **Crear script de base de datos como**:

    ![Crear un script de base de datos](media/scripting-ssms/scriptdb.png)

4. Revise la consulta de creación de la base de datos en la ventana: 

    ![Base de datos con script generado](media/scripting-ssms/scriptedoutdb.png)
    - Esta opción solo creará un script de las opciones de configuración de la base de datos.  

### <a name="script-database-using-generate-scripts-option"></a>Crear un script de base de datos con la opción Generar scripts
1. Conéctese a su servidor SQL Server.
2. Expanda el nodo **Bases de datos** .
3. Haga clic con el botón derecho en la base de datos > **Tareas** > **Generar scripts**:

    ![Generar scripts para una base de datos](media/scripting-ssms/generatescriptsfordb.png)

4. Seleccione **Siguiente** y verá que puede elegir la opción de crear un script de toda la base de datos o bien de objetos específicos de la base de datos: 
 
    ![Generar scripts para objetos](media/scripting-ssms/scriptobjects.png)
 
5. Seleccione **Siguiente**. En esta pantalla puede configurar la ubicación en la que se guardará el script. 
    - También puede configurar opciones avanzadas seleccionando **Opciones avanzadas**:

    ![Opciones avanzadas de script](media/scripting-ssms/advancedscripts.png)

6. Cuando esté a punto para continuar, pulse **Siguiente** hasta que se generen los scripts y llegue a **Finalizar**. El script de base de datos estará en la ubicación guardada en el paso 5. 
    - Se creará un script del esquema y de distintos objetos de la base de datos, pero no de los datos. 
 
## <a name="script-tables"></a>Crear scripts de tablas
En esta sección se explica cómo crear scripts de tablas de la base de datos.

1. Conéctese a su servidor SQL Server.
2. Expanda el nodo **Bases de datos**.
3. Expanda el nodo de la base de datos **AdventureWorks**. 
4. Expanda el nodo **Tablas**.
5. Haga clic con el botón derecho en la tabla para la que quiere crear un script > **Script Table as** (Crear script de tabla como):
    - Aquí hay varias opciones, como la de crear la tabla o insertar datos en ella: 
    
    ![Incluir tabla](media/scripting-ssms/scripttable.png)
 
## <a name="script-stored-procedures"></a>Crear scripts de procedimientos almacenados
En esta sección se explica cómo crear scripts de procedimientos almacenados. 

1. Conéctese a su servidor SQL Server.
2. Expanda el nodo **Bases de datos**.
3. Expanda el nodo **Programación**. 
4. Expanda el nodo **Procedimiento almacenado**.
5. Haga clic con el botón derecho en el procedimiento almacenado que le interesa > **Script Stored Procedure As** (Crear script de procedimiento almacenado como):
    
    ![Crear scripts de procedimientos almacenados](media/scripting-ssms/scriptstoredprocedure.PNG)

## <a name="script-extended-events"></a>Crear scripts de eventos extendidos
En esta sección se explica cómo crear scripts de [eventos extendidos](https://docs.microsoft.com/en-us/sql/relational-databases/extended-events/extended-events). 

1. Conéctese a su servidor SQL Server.
2. Expanda el nodo **Administración**.
3. Expanda el nodo **Eventos extendidos**.
4. Expanda el nodo **Sesiones**.
5. Haga clic con el botón derecho en la sesión extendida que le interesa > **Script Session As** (Crear script de sesión como):

    ![Crear scripts de XEvents](media/scripting-ssms/scriptxevents.png) 

## <a name="next-steps"></a>Pasos siguientes
En el siguiente artículo se presentan las plantillas predefinidas que se encuentran en SSMS. 

Vaya al siguiente artículo para obtener más información
> [!div class="nextstepaction"]
> [Botón de pasos siguientes](templates-ssms.md)


