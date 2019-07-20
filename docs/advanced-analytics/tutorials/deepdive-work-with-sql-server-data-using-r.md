---
title: Crear una base de datos y permisos para los tutoriales de RevoScaleR
description: Tutorial tutorial sobre cómo crear una base de datos de SQL Server para tutoriales de R.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 88a8bb4ab81f3e7c18bcafce70488583fa0421fa
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344642"
---
# <a name="create-a-database-and-permissions-sql-server-and-revoscaler-tutorial"></a>Crear una base de datos y permisos (tutorial de SQL Server y RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Esta lección forma parte del [tutorial de RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre cómo usar [las funciones de RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

La lección uno consiste en configurar una base de datos SQL Server y los permisos necesarios para completar este tutorial. Use [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) u otro editor de consultas para completar las siguientes tareas:

> [!div class="checklist"]
> * Crear una nueva base de datos para almacenar los datos para el entrenamiento y la puntuación de dos modelos de R
> * Crear un inicio de sesión de usuario de base de datos con permisos para crear y usar objetos de base de datos
  
## <a name="create-the-database"></a>Crear la base de datos

En este tutorial se necesita una base de datos para almacenar datos y código. Si no es administrador, pida a su DBA que cree la base de datos e inicie sesión automáticamente. Necesitará permisos para escribir y leer datos, y para ejecutar scripts de R.

1. En SQL Server Management Studio, conéctese a una instancia de base de datos habilitada para R.

2. Haga clic con el botón derecho en **bases**de **datos y seleccione nueva base de datos**.
  
2. Escriba un nombre para la nueva base de datos: RevoDeepDive.
  

## <a name="create-a-login"></a>Creación de un inicio de sesión
  
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

En este tutorial se muestran las operaciones de scripts y DDL de R, incluida la creación y eliminación de tablas y procedimientos almacenados, y la ejecución de scripts de R en un proceso externo en SQL Server. En este paso, asigne permisos para permitir estas tareas.

En este ejemplo se da por supuesto un inicio de sesión de SQL (DDUser01), pero si creó un inicio de sesión de Windows, úselo en su lugar.

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
  
    Antes de ejecutar código de R con el servidor, quizás le interese comprobar que se puede tener acceso a la base de datos desde el entorno de desarrollo de R. Tanto [Explorador de servidores en Visual Studio](https://docs.microsoft.com/previous-versions/x603htbk(v=vs.140)) como [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md) son herramientas gratuitas con características eficaces de administración y conectividad de base de datos.
  
    Si no quiere instalar herramientas adicionales de administración de bases de datos, puede crear una conexión de prueba a la instancia de SQL Server mediante el [Administrador de orígenes de datos ODBC](https://docs.microsoft.com/sql/odbc/admin/odbc-data-source-administrator?view=sql-server-2017) en el Panel de control. Si la base de datos está configurada correctamente y escribe el nombre de usuario y la contraseña correctos, verá la base de datos que acaba de crear y podrá seleccionarla como la base de datos predeterminada.
  
    Entre los motivos comunes de los errores de conexión se incluyen las conexiones remotas no están habilitadas para el servidor y el protocolo de canalizaciones con nombre no está habilitado. Puede encontrar más sugerencias para la solución de problemas en este artículo: [Solucionar problemas de conexión al Motor de base de datos SQL Server](https://docs.microsoft.com/sql/database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine).
  
- **¿Por qué el nombre de la tabla tiene como prefijo "datareader"?**
  
    Cuando se especifica el esquema predeterminado para este usuario como **db_datareader**, todas las tablas y otros objetos nuevos creados por este usuario tienen como prefijo el nombre del *esquema* . Un esquema es como una carpeta que puede agregar a una base de datos para organizar objetos. El esquema también define los privilegios de un usuario en la base de datos.
  
    Cuando el esquema está asociado a un nombre de usuario determinado, el usuario es el _propietario del esquema_. Cuando crea un objeto, siempre lo crea en su propio esquema, a menos que solicite específicamente que se cree en otro esquema.
  
    Por ejemplo, si crea una tabla con el nombre **TestData**y el esquema predeterminado es **db_datareader**, la tabla se crea con el nombre `<database_name>.db_datareader.TestData`.
  
    Por esta razón, una base de datos puede contener varias tablas con el mismo nombre, siempre y cuando las tablas pertenezcan a esquemas diferentes.
   
    Si busca una tabla y no especifica un esquema, el servidor de base de datos buscará un esquema de su propiedad. Por lo tanto, no hace falta que especifique el nombre de esquema al tener acceso a tablas en un esquema asociado a su inicio de sesión.
  
- **No tengo privilegios DDL. ¿Puedo ejecutar el tutorial igualmente?**
  
    Sí, pero debe pedirle a alguien que cargue previamente los datos en las [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tablas y vaya directamente a la lección siguiente. Siempre que sea posible, se llama a las funciones que requieren privilegios DDL en el tutorial.

    Además, pida a su administrador que le conceda el permiso, ejecute cualquier SCRIPT externo. Es necesario para la ejecución del script de R, ya sea remota `sp_execute_external_script`o mediante.

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Crear objetos de datos de SQL Server mediante RxSqlServerData](../../advanced-analytics/tutorials/deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)