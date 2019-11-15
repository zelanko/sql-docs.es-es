---
title: Tutoriales de base de datos para RevoScaleR
description: Tutorial sobre cómo crear una base de datos de SQL Server para tutoriales de R.
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 537bfb64562dfad9dbefbce70423892cd6e1e431
ms.sourcegitcommit: 09ccd103bcad7312ef7c2471d50efd85615b59e8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2019
ms.locfileid: "73727123"
---
# <a name="create-a-database-and-permissions-sql-server-and-revoscaler-tutorial"></a>Creación de una base de datos y permisos (tutorial de SQL Server y RevoScaleR)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Esta lección forma parte del [tutorial de RevoScaleR](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md) sobre el uso de las [funciones de RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

La lección uno explica cómo configurar una base de datos SQL Server y los permisos necesarios para completar este tutorial. Use [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) u otro editor de consultas para completar las tareas siguientes:

> [!div class="checklist"]
> * Crear una base de datos para almacenar los datos destinados a entrenar y puntuar dos modelos de R
> * Crear un inicio de sesión de usuario de base de datos con permisos para crear y usar objetos de base de datos
  
## <a name="create-the-database"></a>Crear la base de datos

Para este tutorial, se necesita una base de datos en la que se almacenen los datos y el código. Si no es administrador, pida a su DBA que cree la base de datos y que inicie su sesión automáticamente. Necesitará permisos para escribir y leer datos, así como para ejecutar scripts de R.

1. En SQL Server Management Studio, conéctese a una instancia de base de datos habilitada para R.

2. Haga clic con el botón derecho en **Bases de datos** y seleccione **Nueva base de datos**.
  
2. Escriba un nombre para la nueva base de datos: RevoDeepDive.
  

## <a name="create-a-login"></a>Creación de un inicio de sesión
  
1. Haga clic en **Nueva consulta**y cambie el contexto de la base de datos a la base de datos maestra.
  
2. En la ventana **Nueva consulta** , ejecute los comandos siguientes para crear las cuentas de usuario y asignarlas a la base de datos usada en este tutorial. Asegúrese de cambiar el nombre de la base de datos si es necesario.

3. Para verificar el inicio de sesión, seleccione la nueva base de datos, expanda **Seguridad** y expanda **Usuarios**.
  
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

## <a name="assign-permissions"></a>Asignación de permisos

En este tutorial se muestran las operaciones de DDL y scripts de R, incluida la creación y la eliminación de tablas y procedimientos almacenados, así como la ejecución de scripts de R en un proceso externo en SQL Server. En este paso, asigne permisos para permitir estas tareas.

En este ejemplo se da por supuesto un inicio de sesión de SQL (DDUser01), pero si creó un inicio de sesión de Windows, úselo en su lugar.

```sql
USE RevoDeepDive
GO

EXEC sp_addrolemember 'db_owner', 'DDUser01'
GRANT EXECUTE ANY EXTERNAL SCRIPT TO DDUser01
GO
```

## <a name="troubleshoot-connections"></a>Solución de problemas de conexiones

En esta sección se enumeran algunos problemas comunes que podrían surgir durante la configuración de la base de datos.

- **¿Cómo puedo confirmar la conectividad de la base de datos y comprobar consultas de SQL?**
  
    Antes de ejecutar código de R con el servidor, quizás le interese comprobar que se puede tener acceso a la base de datos desde el entorno de desarrollo de R. Tanto [Explorador de servidores en Visual Studio](https://docs.microsoft.com/previous-versions/x603htbk(v=vs.140)) como [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md) son herramientas gratuitas con características eficaces de administración y conectividad de base de datos.
  
    Si no quiere instalar herramientas adicionales de administración de bases de datos, puede crear una conexión de prueba a la instancia de SQL Server mediante el [Administrador de orígenes de datos ODBC](https://docs.microsoft.com/sql/odbc/admin/odbc-data-source-administrator?view=sql-server-2017) en el Panel de control. Si la base de datos está configurada correctamente y escribe el nombre de usuario y la contraseña correctos, verá la base de datos que acaba de crear y podrá seleccionarla como la base de datos predeterminada.
  
    Algunos de los motivos comunes de los errores de conexión pueden ser que la conexión remota no esté habilitada para el servidor y que el protocolo de canalizaciones con nombre no esté habilitado. Encontrará más sugerencias para la solución de problemas en este artículo: [Solucionar problemas de conexión al motor de base de datos de SQL Server](https://docs.microsoft.com/sql/database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine).
  
- **¿Por qué el nombre de la tabla tiene como prefijo "datareader"?**
  
    Cuando se especifica el esquema predeterminado para este usuario como **db_datareader**, todas las tablas y los objetos que este usuario cree tendrán como prefijo este *esquema*. Un esquema es como una carpeta que puede agregar a una base de datos para organizar objetos. El esquema también define los privilegios de un usuario en la base de datos.
  
    Cuando el esquema se asocia con un nombre de usuario determinado, el usuario es el _propietario del esquema_. Cuando crea un objeto, siempre lo crea en su propio esquema, a menos que solicite específicamente que se cree en otro esquema.
  
    Por ejemplo, si crea una tabla denominada **TestData** y el esquema predeterminado es **db_datareader**, la tabla se creará con el nombre `<database_name>.db_datareader.TestData`.
  
    Por esta razón, una base de datos puede contener varias tablas con el mismo nombre, siempre y cuando las tablas pertenezcan a esquemas diferentes.
   
    Si busca una tabla y no especifica un esquema, el servidor de bases de datos buscará un esquema de su propiedad. Por lo tanto, no hace falta que especifique el nombre de esquema al tener acceso a tablas en un esquema asociado a su inicio de sesión.
  
- **No tengo privilegios DDL. ¿Puedo ejecutar el tutorial igualmente?**
  
    Sí, pero debe pedirle a alguien que cargue previamente los datos en las tablas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y vaya directamente a la lección siguiente. Siempre que sea posible, las funciones que requieren privilegios DDL estarán indicadas en el tutorial.

    Además, pida a su administrador que le conceda el permiso EXECUTE ANY EXTERNAL SCRIPT. Se necesita para la ejecución del script de R, ya sea remota o mediante `sp_execute_external_script`.

## <a name="next-steps"></a>Pasos siguientes

> [!div class="nextstepaction"]
> [Crear objetos de datos de SQL Server mediante RxSqlServerData](../../advanced-analytics/tutorials/deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)