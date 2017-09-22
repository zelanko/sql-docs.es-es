---
title: Trabajar con datos de SQL Server con R | Documentos de Microsoft
ms.custom:
- SQL2016_New_Updated
ms.date: 05/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: 0a3d7ba0-4113-4cde-9645-debba45cae8f
caps.latest.revision: 20
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: 6aa23c7a8f2daefcf0b138bb39926eb2e377c22b
ms.contentlocale: es-es
ms.lasthandoff: 09/21/2017

---
# <a name="work-with-sql-server-data-using-r"></a>Trabajar con datos de SQL Server con R

En esta lección, configurará el entorno, agregará los datos que necesita para entrenar los modelos y ejecutará algunos resúmenes rápidos de los datos. Como parte del proceso, llevará a cabo estas tareas:
  
- Crear una base de datos para almacenar los datos destinados a entrenar y puntuar dos modelos de R.
  
- Crear una cuenta (un usuario de Windows o un inicio de sesión de SQL) para usarla al comunicarse entre la estación de trabajo y equipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
  
- Crear orígenes de datos en R para trabajar con objetos de base de datos y datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
  
- Usar el origen de datos de R para cargar datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
  
- Usar R para obtener una lista de variables y modificar los metadatos de la tabla [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .
  
- Crear un contexto de proceso para habilitar la ejecución remota de código R.
  
- Aprender a habilitar el seguimiento en el contexto de proceso remoto.
  
## <a name="create-the-database-and-user"></a>Crear la base de datos y el usuario

Para este tutorial, creará una base de datos en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]y agregará un inicio de sesión de SQL con permisos para escribir y leer datos, así como para ejecutar scripts de R.

> [!NOTE]
> Si solo está leyendo datos, la cuenta que ejecuta los scripts de R requiere solo permisos SELECT (**db_datareader** rol) en la base de datos especificada. Pero en este tutorial necesitará privilegios de administrador DDL para preparar la base de datos y crear tablas para guardar los resultados de puntuación.
> 
> Además, si no es el propietario de la base de datos, necesitará el permiso EXECUTE ANY EXTERNAL SCRIPT, para poder ejecutar scripts de R.

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
  
    Antes de ejecutar código de R con el servidor, quizás le interese comprobar que se puede tener acceso a la base de datos desde el entorno de desarrollo de R. Tanto [Explorador de servidores en Visual Studio](https://msdn.microsoft.com/library/x603htbk.aspx) como [SQL Server Management Studio](/sql-docs/docs/ssms/download-sql-server-management-studio-ssms) son herramientas gratuitas con características eficaces de administración y conectividad de base de datos.
  
    Si no quiere instalar herramientas adicionales de administración de bases de datos, puede crear una conexión de prueba a la instancia de SQL Server mediante el [Administrador de orígenes de datos ODBC](https://msdn.microsoft.com/library/ms714024.aspx) en el Panel de control. Si la base de datos está configurada correctamente y escribe el nombre de usuario y la contraseña correctos, verá la base de datos que acaba de crear y podrá seleccionarla como la base de datos predeterminada.
  
    Si no se puede conectar a la base de datos, compruebe que las conexiones remotas están habilitadas para el servidor y que se ha habilitado el protocolo Canalizaciones con nombre. En [este artículo](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx)encontrará más sugerencias para solucionar problemas.
  
- **¿Por qué el nombre de la tabla tiene como prefijo "datareader"?**
  
    Cuando se especifica el esquema predeterminado para este usuario como **db_datareader**, todas las tablas y los objetos que este usuario cree tendrán como prefijo este *esquema*. Un esquema es como una carpeta que puede agregar a una base de datos para organizar objetos. El esquema también define los privilegios de un usuario en la base de datos.
  
    Cuando el esquema se asocia con un nombre de usuario determinado, el usuario es el propietario del esquema. Cuando crea un objeto, siempre lo crea en su propio esquema, a menos que solicite específicamente que se cree en otro esquema.
  
    Por ejemplo, si crea una tabla denominada *TestData* y el esquema predeterminado es **db_datareader**, la tabla se creará con el nombre *<nombre_de_base_de_datos>.db_datareader.TestData*.
  
    Por esta razón, una base de datos puede contener varias tablas con el mismo nombre, siempre y cuando las tablas pertenezcan a esquemas diferentes.
   
    Si busca una tabla y no especifica un esquema, el servidor de bases de datos buscará un esquema de su propiedad. Por lo tanto, no hace falta que especifique el nombre de esquema al tener acceso a tablas en un esquema asociado a su inicio de sesión.
  
- **No tengo privilegios DDL. ¿Puedo ejecutar el tutorial igualmente?**
  
    Sí, pero debe pedirle a alguien que cargue previamente los datos en las tablas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y omitir las secciones en las que se crean tablas. Por lo general, las funciones que requieren privilegios DDL están indicadas en el tutorial.

    Además, pida al administrador que le conceda el permiso EXECUTE ANY EXTERNAL SCRIPT. Es necesario para la ejecución de script de R, si es remoto o mediante `sp_execute_external_script`.

## <a name="next-step"></a>Paso siguiente

[Crear objetos de datos de SQL Server mediante RxSqlServerData](../../advanced-analytics/tutorials/deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)

## <a name="overview"></a>Información general

[Análisis detallado de ciencia de datos: Usar los paquetes de RevoScaleR](../../advanced-analytics/tutorials/deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)




