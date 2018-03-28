---
Title: 'Tutorial: Additional Tips and Tricks for using SSMS'
description: 'Tutorial que incluye algunas recomendaciones y trucos adicionales al usar SSMS. '
keywords: SQL Server, SSMS, SQL Server Management Studio
author: MashaMSFT
ms.author: mathoma
ms.date: 03/13/2018
ms.topic: Tutorial
ms.suite: sql
ms.prod_service: sql-tools
ms.reviewer: sstein
manager: craigg
helpviewer_keywords:
- source controls [SQL Server Management Studio], tutorials
- Help [SQL Server], SQL Server Management Studio
- tutorials [SQL Server Management Studio]
- Transact-SQL tutorials
- SQL Server Management Studio [SQL Server], tutorials
ms.openlocfilehash: 0613d9352e7be20de52fb771fb8e28823556304b
ms.sourcegitcommit: 8e897b44a98943dce0f7129b1c7c0e695949cc3b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/21/2018
---
# <a name="tutorial-additional-tips-and-tricks-for-using-ssms"></a>Tutorial: Otras recomendaciones y trucos al usar SSMS
Este tutorial le ofrece algunos trucos adicionales al usar SQL Server Management Studio. En este artículo aprenderá a: 

   - Agregar o quitar marcas de comentario del texto de Transact-SQL (T-SQL)
   - Aplicar sangría al texto
   - Filtrar objetos en el Explorador de objetos
   - Acceder al registro de errores de SQL Server
   - Buscar el nombre de su Instancia de SQL Server

## <a name="prerequisites"></a>Prerequisites
Para llevar a cabo este tutorial necesita tener SQL Server Management Studio, acceso a un servidor SQL Server y una base de datos de AdventureWorks. 

- Instale [SQL Server Management Studio](https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms).
- Instale [SQL Server 2017 Developer Edition](https://www.microsoft.com/en-us/sql-server/sql-server-downloads).
- Descargar una [Base de datos de ejemplo AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases). 
    - Aquí encontrará instrucciones para restaurar bases de datos en SSMS: [Restaurar una base de datos](https://docs.microsoft.com/en-us/sql/relational-databases/backup-restore/restore-a-database-backup-using-ssms). 

## <a name="commenting--uncommenting-your-t-sql"></a>Agregar o quitar marcas de comentario del código de T-SQL
Se puede usar el botón Comentario de la barra de herramientas para agregar o quitar marcas de comentario en las secciones del texto. El texto al que se haya quitado la marca de comentario no se ejecutará. 

1. Abra SQL Server Management Studio. 
2. Conéctese a su servidor SQL Server.
3. Abra una ventana de **nueva consulta**. 
4. Pegue el siguiente fragmento de código de T-SQL en la ventana de texto: 

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
2. Resalte la sección **Alter Database** (Modificar base de datos) del texto y haga clic en **Comentario** en la barra de herramientas: 

    ![Comentario](media/ssms-tricks/comment.png)
3. Haga clic en **Ejecutar** para ejecutar la sección del texto a la que se ha quitado la marca de comentario. 
4. Resalte todo excepto el comando **Alter Database** y haga clic en **Comentario** en la barra de herramientas:

    ![Agregar un comentario a todo](media/ssms-tricks/commenteverything.png)

5. Resalte la sección **Alter Database** (Modificar base de datos) y haga clic en **Quitar marca de comentario** para quitarle la marca de comentario:

    ![Quitar la marca de comentario](media/ssms-tricks/uncomment.png)
    
6. Haga clic en **Ejecutar** para ejecutar la sección del texto a la que se ha quitado la marca de comentario. 

## <a name="indent-your-text"></a>Aplicar sangría al texto
Los botones de sangría le permiten aumentar y reducir la sangría del texto. 

1. Abra una ventana de **nueva consulta**. 
2. Pegue el siguiente fragmento de código de T-SQL en la ventana de texto: 

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
2. Resalte la sección **Alter Database** (Modificar base de datos) del texto y presione **Aumentar sangría** en la barra de herramientas para hacer avanzar este texto.

    ![Aumentar sangría](media/ssms-tricks/increaseindent.png)

3. Vuelva a resaltar la sección **Alter Database** (Modificar base de datos) del texto y, esta vez, haga clic en **Reducir sangría** para hacer retroceder este texto. 
    ![Disminuir sangría](media/ssms-tricks/decreaseindent.png)


## <a name="filtering-objects-in-object-explorer"></a>Filtrar objetos en el Explorador de objetos
Cuando una base de datos tiene muchos objetos, puede resultar difícil buscar un objeto específico. Para facilitar esta tarea, tiene la posibilidad de filtrar objetos. En esta sección se explica cómo filtrar las tablas, aunque se pueden aplicar los mismos pasos a cualquier nodo del **Explorador de objetos**.

1. Conéctese a su servidor SQL Server.
2. Expanda el nodo **Bases de datos**.
3. Expanda el nodo de la base de datos **AdventureWorks**. 
4. Expanda el nodo **Tablas**. 
   - Observará que puede ver todas las tablas que se encuentran en la base de datos.
5. Haga clic con el botón derecho en el nodo **Tablas** > **Filtro** > **Configuración del filtro**:

    ![Configuración del filtro](media/ssms-tricks/filtersettings.png)

6. En la ventana Configuración del filtro puede modificar la configuración del filtro. Algunos ejemplos:
    - Filtrar por nombre: ![Filtrar por nombre](media/ssms-tricks/filterbyname.png)
    - Filtrar por esquema: ![Filtrar por esquema](media/ssms-tricks/filterbyschema.png)

7. Para borrar el filtro, haga clic con el botón derecho en **Tablas** > **Quitar filtro**.

    ![Quitar filtro](media/ssms-tricks/removefilter.png)
    


## <a name="accessing-your-sql-server-error-log"></a>Acceder al registro de errores de SQL Server
El registro de errores es un archivo que contiene detalles sobre lo que ocurre en SQL Server. Se puede navegar por él y efectuar consultas en SSMS. También se puede encontrar como archivo .log en el disco.

### <a name="finding-your-error-log-if-you-cannot-connect-to-sql"></a>Buscar el registro de errores si no se puede conectar a SQL
1. Abra el Administrador de configuración de SQL Server. 
2. Expanda el nodo **Servicios**.
3. Haga clic con el botón derecho en la instancia de SQL Server > **Propiedades**:

    ![Propiedades del servidor del Administrador de configuración](media/ssms-tricks/serverproperties.PNG)

4. Seleccione la pestaña **Parámetros de inicio**.
5. En el área **Parámetros existentes**, la ruta de acceso indicada después de la "-e" es la ubicación del registro de errores: 
    
    ![Registro de errores](media/ssms-tricks/errorlog.png)
    - Observará que hay varios archivos errorlog.* en esta ubicación. El que termina en *.log es el actual, mientras que los que terminan con números son registros anteriores, puesto que se crea un nuevo registro cada vez que se reinicia SQL Server. 
6. Abra este archivo en el Bloc de notas. 

### <a name="finding-your-error-log-if-youre-connected-to-sql"></a>Buscar el registro de errores si está conectado a SQL
1. Conéctese a su servidor SQL Server.
2. Abra una ventana de **nueva consulta**. 
3. Pegue el siguiente fragmento de código de T-SQL en la ventana de consulta y haga clic en **Ejecutar**:


  ```sql
   SELECT SERVERPROPERTY('ErrorLogFileName') AS 'Error log file location' 
  ```
3. Los resultados muestran la ubicación del registro de errores dentro del sistema de archivos: 

![Buscar el registro de errores por consulta](media/ssms-tricks/finderrorlogquery.png)

### <a name="open-error-log-within-ssms"></a>Abrir el registro de errores en SSMS
1. Conéctese a su servidor SQL Server.
2. Expanda el nodo **Administración** . 
3. Expanda el nodo **Registros de SQL Server**. 
4. Haga clic con el botón derecho en el registro de errores **actual** > **Ver registro de SQL Server**:

    ![Ver el registro de errores en SSMS](media/ssms-tricks/viewerrorloginssms.png)

### <a name="query-error-log-within-ssms"></a>Consultar el registro de errores en SSMS
1. Conéctese a su servidor SQL Server.
2. Abra una ventana de **nueva consulta**.
3. Pegue el siguiente fragmento de código de T-SQL en la ventana de consulta:

 ```sql
   sp_readerrorlog 0,1,'Server process ID' 
  ``` 
4. Modifique como quiera el texto situado dentro de las comillas.
5. Ejecute la consulta y revise los resultados:
   
    ![Consultar el registro de errores](media/ssms-tricks/queryerrorlog.png)

## <a name="determine-sql-server-instance-name"></a>Determinar el nombre de la instancia de SQL Server…
Hay distintas maneras de determinar el nombre de la instancia antes y después de conectarse a SQL Server.  

### <a name="when-you-dont-know-it"></a>… Si lo desconoce
1. Siga los pasos necesarios para buscar el [registro de errores de SQL Server en el disco.](#finding-your-error-log-if-you-cannot-connect-to-sql) 
2. Abra el archivo errorlog.log en el Bloc de notas. 
3. Desplácese por él hasta que encuentre el texto "Server name is" (El nombre del servidor es):
  - Lo que aparezca entre las comillas simples es el nombre de la instancia y a lo que se deberá conectar: ![Nombre del servidor en el registro de errores](media/ssms-tricks/servernameinlog.png)

### <a name="once-youre-connected"></a>… Una vez que está conectado
Hay tres lugares en los que puede buscar la instancia a la que se ha conectado. 

1. El nombre del servidor aparecerá en el **Explorador de objetos**.

    ![Nombre de la instancia en el Explorador de objetos](media/ssms-tricks/nameinobjectexplorer.png)
2. El nombre del servidor se mostrará en la ventana de consulta:

    ![Nombre en la ventana de consulta](media/ssms-tricks/nameinquerywindow.png)
3. . El nombre del servidor también se mostrará en la **ventana Propiedades**.
    - Para acceder a ella, abra el menú **Vista** > **ventana Propiedades**

    ![Nombre en Propiedades](media/ssms-tricks/nameinproperties.png)

### <a name="if-youre-connected-to-an-alias-or-availability-group-listener"></a>… Si se ha conectado a un alias o a un agente de escucha del grupo de disponibilidad 
Si se ha conectado a un alias o a un agente de escucha del grupo de disponibilidad, eso es lo que se mostrará en el **Explorador de objetos** y en **Propiedades**. En este caso, puede que el nombre del servidor SQL Server no sea claro y se deba consultar. 

1. Conéctese a SQL Server.
2. Abra una ventana de **nueva consulta**.
3. Pegue el siguiente fragmento de código de T-SQL en la ventana: 

  ```sql
   select @@Servername 
 ``` 
4. Vea los resultados de la consulta para identificar el nombre del servidor de SQL Server al que se ha conectado: 
    
    ![Nombre del servidor de consulta](media/ssms-tricks/queryservername.png)


