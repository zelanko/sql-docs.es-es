---
title: Trabajar con datos de SQL Server con R (SQL y R profundización) | Documentos de Microsoft
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: e57e94d1d7856bfc9082c1a73a13a5c0a620b5ed
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="work-with-sql-server-data-using-r-sql-and-r-deep-dive"></a>Trabajar con datos de SQL Server con R (SQL y R profundización)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Este artículo forma parte del tutorial exhaustiva de ciencia de datos, acerca de cómo usar [RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler) con SQL Server.

En esta lección, configurar el entorno y agregar los datos que necesita para entrenar los modelos y ejecutar algunos rápidos resúmenes de los datos. Como parte del proceso, debe completar estas tareas:
  
- Crear una base de datos para almacenar los datos destinados a entrenar y puntuar dos modelos de R.
  
- Crear una cuenta (un usuario de Windows o un inicio de sesión de SQL) para usarla al comunicarse entre la estación de trabajo y equipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
  
- Crear orígenes de datos en R para trabajar con objetos de base de datos y datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
  
- Usar el origen de datos de R para cargar datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
- Usar R para obtener una lista de variables y modificar los metadatos de la tabla [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
  
- Crear un contexto de proceso para habilitar la ejecución remota de código R.
  
- (Opcional) Habilitar el seguimiento en el contexto de proceso remoto.
  
## <a name="create-the-database-and-user"></a>Crear la base de datos y el usuario

Para este tutorial, creará una nueva base de datos en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]y agregar un inicio de sesión SQL con permisos para escribir y leer datos y para ejecutar scripts de R.

> [!NOTE]
> Si solo está leyendo datos, la cuenta que ejecuta los scripts de R requiere permisos SELECT (**db_datareader** rol) en la base de datos especificada. Sin embargo, en este tutorial, debe tener privilegios de administrador DDL que se va a preparar la base de datos como crear tablas para guardar los resultados de puntuación.
> 
> Además, si no es el propietario de la base de datos, necesita el permiso EXECUTE ANY EXTERNAL SCRIPT, para ejecutar scripts de R.

1. En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], seleccione la instancia donde está habilitado [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] , haga clic con el botón derecho en **Bases de datos**y seleccione **Nueva base de datos**.
  
2. Escriba un nombre para la nueva base de datos. Puede usar el nombre que quiera, pero recuerde editar en consecuencia todos los scripts de [!INCLUDE[tsql](../../includes/tsql-md.md)] y de R en este tutorial.
  
    > [!TIP]
    > Para ver el nombre de la base de datos actualizado, haga clic con el botón derecho en **Bases de datos** y seleccione **Actualizar** .
  
3. Haga clic en **Nueva consulta**y cambie el contexto de la base de datos a la base de datos maestra.
  
4. En la ventana **Nueva consulta** , ejecute los comandos siguientes para crear las cuentas de usuario y asignarlas a la base de datos usada en este tutorial. Asegúrese de cambiar el nombre de la base de datos si es necesario.
  
**Usuario de Windows**
  
```SQL
 -- Create server user based on Windows account
USE master
GO
CREATE LOGIN [<DOMAIN>\<user_name>] FROM WINDOWS WITH DEFAULT_DATABASE=[DeepDive]

 --Add the new user to tutorial database
USE [DeepDive]
GO
CREATE USER [<user_name>] FOR LOGIN [<DOMAIN>\<user_name>] WITH DEFAULT_SCHEMA=[db_datareader]
```

**Inicio de sesión de SQL**

```SQL
-- Create new SQL login
USE master
GO
CREATE LOGIN DDUser01 WITH PASSWORD='<type password here>', CHECK_EXPIRATION=OFF, CHECK_POLICY=OFF;

-- Add the new SQL login to tutorial database
USE [DeepDive]
GO
CREATE USER [DDUser01] FOR LOGIN [DDUser01] WITH DEFAULT_SCHEMA=[db_datareader]
```

5. Seleccione la nueva base de datos, expanda **Seguridad**y expanda **Usuarios**para comprobar que se ha creado el usuario.

## <a name="troubleshooting"></a>Solucionar problemas

En esta sección se enumeran algunos problemas comunes que podrían surgir durante la configuración de la base de datos.

- **¿Cómo puedo confirmar la conectividad de la base de datos y comprobar consultas de SQL?**
  
    Antes de ejecutar código de R con el servidor, quizás le interese comprobar que se puede tener acceso a la base de datos desde el entorno de desarrollo de R. Tanto [Explorador de servidores en Visual Studio](https://msdn.microsoft.com/library/x603htbk.aspx) como [SQL Server Management Studio](../../ssms/download-sql-server-management-studio-ssms.md) son herramientas gratuitas con características eficaces de administración y conectividad de base de datos.
  
    Si no quiere instalar herramientas adicionales de administración de bases de datos, puede crear una conexión de prueba a la instancia de SQL Server mediante el [Administrador de orígenes de datos ODBC](https://msdn.microsoft.com/library/ms714024.aspx) en el Panel de control. Si la base de datos está configurada correctamente y escribe el nombre de usuario y la contraseña correctos, verá la base de datos que acaba de crear y podrá seleccionarla como la base de datos predeterminada.
  
    Si no se puede conectar a la base de datos, compruebe que las conexiones remotas están habilitadas para el servidor y que se ha habilitado el protocolo Canalizaciones con nombre. Se proporcionan varias sugerencias de solución de problemas adicionales en este artículo: [solucionar problemas de conexión para el motor de base de datos de SQL Server](https://docs.microsoft.com/sql/database-engine/configure-windows/troubleshoot-connecting-to-the-sql-server-database-engine).
  
- **¿Por qué el nombre de la tabla tiene como prefijo "datareader"?**
  
    Cuando se especifica el esquema predeterminado para este usuario como **db_datareader**, todas las tablas y otros objetos nuevos creados por este usuario tienen el prefijo con el *esquema* nombre. Un esquema es como una carpeta que puede agregar a una base de datos para organizar objetos. El esquema también define los privilegios de un usuario en la base de datos.
  
    Si el esquema se asocia con un nombre de usuario en particular, el usuario es el _propietario del esquema_. Cuando crea un objeto, siempre lo crea en su propio esquema, a menos que solicite específicamente que se cree en otro esquema.
  
    Por ejemplo, si crea una tabla con el nombre `*`TestData`, and your default schema is **db\_datareader**, the table is created with the name `.db_datareader < database_name >. TestData'.
  
    Por esta razón, una base de datos puede contener varias tablas con el mismo nombre, siempre y cuando las tablas pertenezcan a esquemas diferentes.
   
    Si está buscando una tabla y no especifica un esquema, el servidor de base de datos busca un esquema perteneciente al usuario. Por lo tanto, no hace falta que especifique el nombre de esquema al tener acceso a tablas en un esquema asociado a su inicio de sesión.
  
- **No tengo privilegios DDL. ¿Puedo ejecutar el tutorial igualmente?**
  
    Sí, pero debe pedirle a alguien que cargue previamente los datos en las tablas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y omitir las secciones en las que se crean tablas. Las funciones que requieren privilegios DDL se indican en el tutorial siempre que sea posible.

    Además, pida al administrador que le conceda el permiso EXECUTE ANY EXTERNAL SCRIPT. Es necesario para la ejecución de script de R, si es remoto o mediante `sp_execute_external_script`.

## <a name="next-step"></a>Paso siguiente

[Crear objetos de datos de SQL Server mediante RxSqlServerData](../../advanced-analytics/tutorials/deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)

## <a name="overview"></a>Información general

[Análisis detallado de ciencia de datos: Usar los paquetes de RevoScaleR](../../advanced-analytics/tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)



