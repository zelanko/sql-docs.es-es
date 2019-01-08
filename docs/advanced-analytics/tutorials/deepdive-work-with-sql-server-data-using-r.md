---
title: 'Crear una base de datos y permisos para ver tutoriales RevoScaleR: SQL Server Machine Learning'
description: Tutorial de tutorial sobre cómo crear una base de datos de SQL Server para los tutoriales de R...
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 15032b604d7ea28ad03acb837f997dac3afa84b8
ms.sourcegitcommit: ee76332b6119ef89549ee9d641d002b9cabf20d2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/20/2018
ms.locfileid: "53645274"
---
# <a name="create-a-database-and-permissions-sql-server-and-revoscaler-tutorial"></a>Crear una base de datos y permisos (tutorial de SQL Server y RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En esta lección forma parte de la [RevoScaleR tutorial](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre cómo usar [funciones de RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

Lección uno es sobre cómo configurar una base de datos de SQL Server y los permisos necesarios para completar este tutorial. Use [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) u otro editor de consultas para completar las tareas siguientes:

> [!div class="checklist"]
> * Crear una nueva base de datos para almacenar los datos de entrenamiento y puntuación dos modelos de R
> * Crear un inicio de sesión de usuario de base de datos con permisos para crear y utilizar objetos de base de datos
  
## <a name="create-the-database"></a>Crear la base de datos

Este tutorial requiere una base de datos para almacenar datos y el código. Si no es un administrador, solicitar el DBA para crear la base de datos y el inicio de sesión para usted. Necesitará permisos para leer y escribir datos y para ejecutar scripts de R.

1. En SQL Server Management Studio, conéctese a una instancia de base de datos habilitada para R.

2. Haga clic en **bases de datos**y seleccione **nueva base de datos**.
  
2. Escriba un nombre para la nueva base de datos: RevoDeepDive.
  

## <a name="create-a-login"></a>Crea un inicio de sesión
  
1. Haga clic en **Nueva consulta**y cambie el contexto de la base de datos a la base de datos maestra.
  
2. En la ventana **Nueva consulta** , ejecute los comandos siguientes para crear las cuentas de usuario y asignarlas a la base de datos usada en este tutorial. Asegúrese de cambiar el nombre de la base de datos si es necesario.

3. Para comprobar el inicio de sesión, seleccione la nueva base de datos, expanda **seguridad**y expanda **usuarios**.
  
**usuario de Windows**
  
```sql
 -- Create server user based on Windows account
USE master
GO
CREATE LOGIN [<DOMAIN>\<user_name>] FROM WINDOWS WITH DEFAULT_DATABASE=[RevoDeepDive]

 --Add the new user to tutorial database
USE [RevoDeepDive]
GO
CREATE USER [<user_name>] FOR LOGIN [<DOMAIN>\<user_name>] WITH DEFAULT_SCHEMA=[db_datareader]
```

**Inicio de sesión de SQL**

```sql
-- Create new SQL login
USE master
GO
CREATE LOGIN [DDUser01] WITH PASSWORD='<type password here>', CHECK_EXPIRATION=OFF, CHECK_POLICY=OFF;

-- Add the new SQL login to tutorial database
USE RevoDeepDive
GO
CREATE USER [DDUser01] FOR LOGIN [DDUser01] WITH DEFAULT_SCHEMA=[db_datareader]
```

## <a name="assign-permissions"></a>Asignar permisos

Este tutorial muestra el script de R y las operaciones de DDL, incluida la creación y eliminación de tablas y procedimientos almacenados y ejecutar el script de R en un proceso externo en SQL Server. En este paso, asigne permisos para permitir que estas tareas.

En este ejemplo se da por supuesto un inicio de sesión SQL (DDUser01), pero si ha creado un inicio de sesión de Windows, use en su lugar.

```sql
USE RevoDeepDive
GO

EXEC sp_addrolemember 'db_owner', 'DDUser01'
GRANT EXECUTE ANY EXTERNAL SCRIPT TO DDUser01
GO
```

## <a name="troubleshoot-connections"></a>Solucionar problemas de conexiones

En esta sección se enumeran algunos problemas comunes que podrían surgir durante la configuración de la base de datos.

- **¿Cómo puedo confirmar la conectividad de la base de datos y comprobar consultas de SQL?**
  
    Antes de ejecutar código de R con el servidor, quizás le interese comprobar que se puede tener acceso a la base de datos desde el entorno de desarrollo de R. Tanto [Explorador de servidores en Visual Studio](https://msdn.microsoft.com/library/x603htbk.aspx) como [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md) son herramientas gratuitas con características eficaces de administración y conectividad de base de datos.
  
    Si no quiere instalar herramientas adicionales de administración de bases de datos, puede crear una conexión de prueba a la instancia de SQL Server mediante el [Administrador de orígenes de datos ODBC](https://msdn.microsoft.com/library/ms714024.aspx) en el Panel de control. Si la base de datos está configurada correctamente y escribe el nombre de usuario y la contraseña correctos, verá la base de datos que acaba de crear y podrá seleccionarla como la base de datos predeterminada.
  
    Causas comunes de errores de conexión incluyen remota no están habilitadas las conexiones para el servidor y no está habilitado el protocolo Canalizaciones con nombre. Puede encontrar más sugerencias para solucionar problemas en este artículo: [Solucionar problemas de conexión para el motor de base de datos SQL Server](https://docs.microsoft.com/sql/database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine).
  
- **¿Por qué el nombre de la tabla tiene como prefijo "datareader"?**
  
    Cuando se especifica el esquema predeterminado para este usuario como **db_datareader**, todas las tablas y los objetos creados por este usuario tienen el prefijo con el *esquema* nombre. Un esquema es como una carpeta que puede agregar a una base de datos para organizar objetos. El esquema también define los privilegios de un usuario en la base de datos.
  
    Cuando el esquema se asocia con un nombre de usuario en particular, el usuario es el _propietario del esquema_. Cuando crea un objeto, siempre lo crea en su propio esquema, a menos que solicite específicamente que se cree en otro esquema.
  
    Por ejemplo, si crea una tabla con el nombre **TestData**, y su esquema predeterminado es **db_datareader**, se crea la tabla con el nombre `<database_name>.db_datareader.TestData`.
  
    Por esta razón, una base de datos puede contener varias tablas con el mismo nombre, siempre y cuando las tablas pertenezcan a esquemas diferentes.
   
    Si está buscando una tabla y no se especifica un esquema, el servidor de base de datos buscará un esquema que posee. Por lo tanto, no hace falta que especifique el nombre de esquema al tener acceso a tablas en un esquema asociado a su inicio de sesión.
  
- **No tengo privilegios DDL. ¿Puedo ejecutar el tutorial igualmente?**
  
    Sí, pero se debe pedirle a alguien que cargue previamente los datos en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tablas e ir directamente a la lección siguiente. Las funciones que requieren privilegios DDL se mencionan en el tutorial siempre que sea posible.

    Además, pida al administrador que conceda el permiso EXECUTE ANY EXTERNAL SCRIPT. Es necesario para la ejecución del script de R, si es remoto o mediante `sp_execute_external_script`.

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Crear objetos de datos de SQL Server mediante RxSqlServerData](../../advanced-analytics/tutorials/deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)