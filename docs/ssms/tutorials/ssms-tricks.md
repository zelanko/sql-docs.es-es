---
Title: 'Tutorial: Additional tips and tricks for using SQL Server Management Studio'
description: 'Tutorial que incluye algunas recomendaciones y trucos adicionales al usar SSMS. '
keywords: SQL Server, SSMS, SQL Server Management Studio
author: MashaMSFT
ms.author: mathoma
ms.date: 03/13/2018
ms.topic: Tutorial
ms.suite: sql
ms.prod: sql
ms.technology: ssms
ms.prod_service: sql-tools
ms.reviewer: sstein
manager: craigg
helpviewer_keywords:
- source controls [SQL Server Management Studio], tutorials
- Help [SQL Server], SQL Server Management Studio
- tutorials [SQL Server Management Studio]
- Transact-SQL tutorials
- SQL Server Management Studio [SQL Server], tutorials
- Find SQL Server Instance
- find instance name
- find sql server instance name
ms.openlocfilehash: ef7bbf9b60cb29bee0285d8974a9b97cbe99a3c2
ms.sourcegitcommit: 0dff9dd43e80eee900eb92d25df9ca18397f3485
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/28/2018
ms.locfileid: "37080103"
---
# <a name="tutorial-additional-tips-and-tricks-for-using-ssms"></a>Tutorial: Recomendaciones y trucos adicionales al usar SSMS
En este tutorial se le ofrecen algunos trucos adicionales al usar SQL Server Management Studio (SSMS). En este artículo aprenderá a: 

> [!div class="checklist"]
> * Agregar o quitar marcas de comentario del texto de Transact-SQL (T-SQL)
> * Aplicar sangría al texto
> * Filtrar objetos en el Explorador de objetos
> * Acceder al registro de errores de SQL Server
> * Buscar el nombre de su instancia de SQL Server

## <a name="prerequisites"></a>Prerequisites
Para llevar a cabo este tutorial, necesita tener SQL Server Management Studio, acceso a un servidor SQL Server y una base de datos de AdventureWorks. 

- Instale [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).
- Instale [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads).
- Descargue una [base de datos de ejemplo AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases). Para aprender a restaurar una base de datos en SSMS, vea [Restaurar una base de datos](https://docs.microsoft.com/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms). 


## <a name="commentuncomment-your-t-sql-code"></a>Agregar o quitar marcas de comentario del código de T-SQL
Se puede usar el botón **Comentario** de la barra de herramientas para agregar o quitar marcas de comentario en las secciones del texto. El texto al que se haya quitado la marca de comentario no se ejecutará. 

1. Abra SQL Server Management Studio. 
2. Conéctese a su servidor de SQL Server.
3. Abra una ventana de nueva consulta. 
4. Pegue el siguiente código de T-SQL en la ventana de texto: 

  ```sql
    USE master
    GO

    -- Drop the database if it already exists
    IF  EXISTS (
        SELECT name 
            FROM sys.databases 
            WHERE name = N'TutorialDB'
            )

    DROP DATABASE TutorialDB
    GO

    CREATE DATABASE TutorialDB
    GO

    ALTER DATABASE [TutorialDB] SET QUERY_STORE=ON
    GO
 ``` 


5. Resalte la sección **Alter Database** (Modificar base de datos) del texto y, después, seleccione el botón **Comentario** de la barra de herramientas: 

    ![Botón Comentario](media/ssms-tricks/comment.png)
6. Seleccione **Ejecutar** para ejecutar la sección del texto a la que se ha quitado la marca de comentario. 
7. Resáltelo todo excepto el comando **Alter Database** y, después, seleccione el botón **Comentario**:

    ![Agregar un comentario a todo](media/ssms-tricks/commenteverything.png)

8. Resalte la sección **Alter Database** del texto y, después, seleccione el botón **Quitar la marca de comentario** para quitar las marcas de comentario del texto:

    ![Quitar la marca de comentario del texto](media/ssms-tricks/uncomment.png)
    
9. Seleccione **Ejecutar** para ejecutar la sección del texto a la que se ha quitado la marca de comentario. 

## <a name="indent-your-text"></a>Aplicar sangría al texto
Puede usar los botones de sangría de la barra de herramientas para aumentar o reducir la sangría del texto. 

1. Abra una ventana de nueva consulta. 
2. Pegue el siguiente código de T-SQL en la ventana de texto: 

  ```sql
    USE master
    GO

    -- Drop the database if it already exists
    IF  EXISTS (
        SELECT name 
            FROM sys.databases 
            WHERE name = N'TutorialDB'
            )

    DROP DATABASE TutorialDB
    GO

    CREATE DATABASE TutorialDB
    GO

    ALTER DATABASE [TutorialDB] SET QUERY_STORE=ON
    GO
 ``` 
 
3. Resalte la sección **Alter Database** (Modificar base de datos) del texto y, después, seleccione el botón **Aumentar sangría** de la barra de herramientas para hacer avanzar este texto:

    ![Aumentar la sangría](media/ssms-tricks/increaseindent.png)

4. Vuelva a resaltar la sección **Alter Database** (Modificar base de datos) del texto y, después, seleccione el botón **Reducir sangría** para hacer retroceder este texto.

    ![Reducir la sangría](media/ssms-tricks/decreaseindent.png)


## <a name="filter-objects-in-object-explorer"></a>Filtrar objetos en el Explorador de objetos
Puede filtrar los objetos para que resulte más fácil encontrar un objeto específico en las bases de datos que contienen muchos objetos. En esta sección se describe cómo filtrar las tablas, pero puede seguir estos pasos en cualquier otro nodo del Explorador de objetos:

1. Conéctese a su servidor de SQL Server.
2. Expanda **Bases de datos** > **AdventureWorks** > **Tablas**. Aparecerán todas las tablas de la base de datos.
5. Haga clic con el botón derecho en **Tablas** y, después, seleccione **Filtro** > **Configuración del filtro**:

    ![Configuración del filtro](media/ssms-tricks/filtersettings.png)

6. En la ventana **Configuración del filtro** puede modificar algunas de las siguientes opciones de filtro:
    - Filtrar por nombre: 
   
      ![Filtrar por nombre](media/ssms-tricks/filterbyname.png)

    - Filtrar por esquema: 
    
      ![Filtrar por esquema](media/ssms-tricks/filterbyschema.png)

7. Para borrar el filtro, haga clic con el botón derecho en **Tablas** y, después, seleccione **Quitar filtro**.

    ![Quitar filtro](media/ssms-tricks/removefilter.png)
    


## <a name="access-your-sql-server-error-log"></a>Acceder al registro de errores de SQL Server
El registro de errores es un archivo que contiene información sobre lo que ocurre en su instancia de SQL Server. Puede examinar y consultar el registro de errores en SSMS. El registro de errores es un archivo .log que se encuentra en el disco.

### <a name="open-the-error-log-in-ssms"></a>Abrir el registro de errores en SSMS
1. Conéctese a su servidor de SQL Server.  
2. Expanda **Administración** > **Registros de SQL Server**. 
4. Haga clic con el botón derecho en el registro de errores **Actual** y, después, seleccione **Ver registro de SQL Server**:

    ![Ver el registro de errores en SSMS](media/ssms-tricks/viewerrorloginssms.png)

### <a name="query-the-error-log-in-ssms"></a>Consultar el registro de errores en SSMS
1. Conéctese a su servidor de SQL Server.
2. Abra una ventana de nueva consulta.
3. Pegue el siguiente código de T-SQL en la ventana de consulta:

 ```sql
   sp_readerrorlog 0,1,'Server process ID' 
  ``` 

4. Modifique el texto situado dentro de las comillas simples que quiere buscar.
5. Ejecute la consulta y, después, revise los resultados:
   
    ![Consultar el registro de errores](media/ssms-tricks/queryerrorlog.png)


### <a name="find-the-error-log-location-if-youre-connected-to-sql-server"></a>Buscar la ubicación del registro de errores si se ha conectado a SQL Server
1. Conéctese a su servidor de SQL Server.
2. Abra una ventana de nueva consulta.
3. Pegue el siguiente código de T-SQL en la ventana de consulta y, después, seleccione **Ejecutar**:

 ```sql
    SELECT SERVERPROPERTY('ErrorLogFileName') AS 'Error log file location'  
  ``` 

4. Los resultados muestran la ubicación del registro de errores en el sistema de archivos: 

    ![Buscar el registro de errores por consulta](media/ssms-tricks/finderrorlogquery.png)

### <a name="find-the-error-log-location-if-you-cant-connect-to-sql-server"></a>Buscar la ubicación del registro de errores si no se puede conectar a SQL Server
1. Abra el Administrador de configuración de SQL Server. 
2. Expanda **Servicios**.
3. Haga clic con el botón derecho en la instancia de SQL Server y, después, seleccione **Propiedades**:

    ![Propiedades del Administrador de configuración de SQL Server](media/ssms-tricks/serverproperties.PNG)

4. Seleccione la pestaña **Parámetros de inicio**.
5. En el área **Parámetros existentes**, la ruta de acceso indicada después de la "-e" es la ubicación del registro de errores: 
    
    ![Registro de errores](media/ssms-tricks/errorlog.png)
    
    En esta ubicación hay varios archivos errorlog.*. El nombre de archivo que termina por *.log es el archivo de registro de errores actual. Los nombres de archivo que terminan con números son archivos de registro anteriores. Cada vez que se reinicia SQL Server se crea un registro nuevo.

6. Abra el archivo errorlog.log en el Bloc de notas. 

## <a name="determine-sql-server-name"></a>Búsqueda del nombre de la instancia de SQL Server.
Tiene a su disposición algunas opciones para buscar el nombre de su instancia de SQL Server antes y después de conectarse a SQL Server.  

### <a name="before-you-connect-to-sql-server"></a>Antes de conectarse a SQL Server
1. Siga los pasos necesarios para buscar el [registro de errores de SQL Server en el disco](#finding-your-error-log-if-you-cannot-connect-to-sql). 
2. Abra el archivo errorlog.log en el Bloc de notas.  
3. Busque el texto *El nombre del servidor es*.
    
    Lo que aparezca entre las comillas simples es el nombre de la instancia de SQL Server a la que se conectará:

    ![Buscar el nombre del servidor en el registro de errores](media/ssms-tricks/servernameinlog.png)
    
    El formato del nombre es NOMBRE_HOST\NOMBRE_INSTANCIA. Si lo único que ve es el nombre de host, significa que ha instalado la instancia predeterminada y el nombre de instancia será MSSQLSERVER. Al establecer conexión con una instancia predeterminada, lo único que tiene que indicar para conectarse a SQL Server es el nombre de host.  

### <a name="when-youre-connected-to-sql-server"></a>Si se ha conectado a SQL Server 
Si se ha conectado a SQL Server, puede buscar el nombre del servidor en tres sitios: 

1. El nombre del servidor se muestra en el Explorador de objetos:

    ![Nombre de la instancia de SQL Server en el Explorador de objetos](media/ssms-tricks/nameinobjectexplorer.png)
2. El nombre del servidor se muestra en la ventana de consulta:

    ![Nombre de la instancia de SQL Server en la ventana de consulta](media/ssms-tricks/nameinquerywindow.png)
3. El nombre del servidor se muestra en **Propiedades**.
    - En el menú **Ver**, seleccione **Ventana de propiedades**:

      ![Nombre de la instancia de SQL Server en la ventana Propiedades](media/ssms-tricks/nameinproperties.png)

### <a name="if-youre-connected-to-an-alias-or-availability-group-listener"></a>Si se ha conectado a un alias o a un agente de escucha del grupo de disponibilidad 
Si se ha conectado a un alias o a un agente de escucha del grupo de disponibilidad, esa información aparecerá en Explorador de objetos y en Propiedades. En este caso, puede que el nombre de la instancia de SQL Server no sea claro y se deba consultar: 

1. Conéctese a su servidor de SQL Server.
2. Abra una ventana de nueva consulta.
3. Pegue el siguiente código de T-SQL en la ventana: 

  ```sql
   select @@Servername 
 ``` 
4. Vea los resultados de la consulta para identificar el nombre de la instancia de SQL Server a la que se ha conectado: 
    
    ![Consultar el nombre de SQL Server](media/ssms-tricks/queryservername.png)


