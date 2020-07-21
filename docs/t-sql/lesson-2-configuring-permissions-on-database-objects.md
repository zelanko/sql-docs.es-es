---
title: 'Tutorial: Configuración de permisos en objetos de base de datos'
ms.custom: seo-lt-2019
ms.date: 07/31/2018
ms.prod: sql
ms.technology: t-sql
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- database permissions
ms.assetid: f964b66a-ec32-44c2-a185-6a0f173bfa22
author: MikeRayMSFT
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 991bdef702b1ed298bb492172ef65c6d25d5d0ab
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "75244745"
---
# <a name="lesson-2-configure-permissions-on-database-objects"></a>Lección 2: Configuración de permisos en objetos de base de datos
[!INCLUDE[tsql-appliesto-ss2008-all-md](../includes/tsql-appliesto-ss2008-all-md.md)]
La concesión de acceso de usuario a una base de datos implica tres pasos. Primero, debe crear un inicio de sesión. El inicio de sesión permite al usuario conectarse a [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)]. Luego, debe configurar el inicio de sesión como un usuario de una base de datos determinada. Y, por último, debe conceder al usuario permiso a objetos de la base de datos. En esta lección se muestran estos tres pasos y cómo crear una vista y un procedimiento almacenado como el objeto.  

  >[!NOTE]
  > En esta sección se utilizan los objetos creados en [Lección 1: Creación de objetos de base de datos](lesson-1-creating-database-objects.md). Complete la primera lección antes de continuar con la segunda. 

## <a name="prerequisites"></a>Prerrequisitos
Para llevar a cabo este tutorial necesita tener SQL Server Management Studio, así como acceso a una instancia de SQL Server. 

- Instale [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms).

Si no tiene acceso a ninguna instancia de SQL Server, seleccione su plataforma en uno de los vínculos siguientes. Si elige la autenticación de SQL, use sus credenciales de inicio de sesión de SQL Server.
- **Windows**: [Descargar SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads).
- **macOS**: [Descargar SQL Server 2017 en Docker](https://docs.microsoft.com/sql/linux/quickstart-install-connect-docker).

[!INCLUDE[Freshness](../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="create-a-login"></a>Creación de un inicio de sesión
Para tener acceso a [!INCLUDE[ssDE](../includes/ssde-md.md)], los usuarios necesitan un inicio de sesión. El inicio de sesión puede representar la identidad del usuario como una cuenta de Windows o como un miembro de un grupo de Windows, o el inicio de sesión puede ser un inicio de sesión de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que solo exista en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Siempre que sea posible, use la autenticación de Windows.  
  
De forma predeterminada, los administradores del equipo tienen acceso total a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para esta lección, deseamos tener un usuario con menos privilegios; por tanto, creará una nueva cuenta de autenticación de Windows local en el equipo. Para hacerlo, debe ser un administrador del equipo. A continuación, concederá al nuevo usuario acceso a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
### <a name="create-a-new-windows-account"></a>Creación de una cuenta de Windows  
  
1.  Haga clic en **Inicio**y en **Ejecutar**, en el cuadro **Abrir** , escriba **%SystemRoot%\system32\compmgmt.msc /s**y, después, haga clic en **Aceptar** para abrir el programa Administración de equipos. 
2.  En **Herramientas del sistema**, expanda **Usuarios y grupos locales**, haga clic con el botón derecho en **Usuarios**y luego haga clic en **Nuevo usuario**.    
3.  En el cuadro **Nombre de usuario** , escriba **Mary**.    
4.  En los cuadros **Contraseña** y **Confirmar contraseña** , escriba una contraseña segura y, a continuación, haga clic en **Crear** para crear un nuevo usuario de Windows local.  
  
### <a name="create-a-sql-login"></a>Creación de un inicio de sesión de SQL  

En una ventana del Editor de consultas de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], escriba y ejecute el siguiente código reemplazando `computer_name` con el nombre del equipo. `FROM WINDOWS` indica que Windows autenticará al usuario. El argumento opcional `DEFAULT_DATABASE` conecta `Mary` con la base de datos `TestData` , a menos que la cadena de conexión indique otra base de datos. Esta instrucción introduce el punto y coma como una terminación opcional de una instrucción [!INCLUDE[tsql](../includes/tsql-md.md)] .
  
  ```sql  
  CREATE LOGIN [computer_name\Mary]  
      FROM WINDOWS  
      WITH DEFAULT_DATABASE = [TestData];  
  GO  
  ```  
  
  Esto autoriza al nombre de usuario `Mary`, autenticado por el equipo, a tener acceso a esta instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Si existe más de una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en el equipo, debe crear el inicio de sesión en cada instancia a la que `Mary` deba tener acceso.    
  > [!NOTE]  
  > Puesto que `Mary` no es una cuenta de dominio, este nombre de usuario solo puede autenticarse en este equipo. 


## <a name="grant-access-to-a-database"></a>Concesión de acceso a una base de datos
Mary ahora tiene acceso a esta instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], pero no tiene permiso para tener acceso a las bases de datos. Incluso no tiene acceso a su propia base de datos **TestData** hasta que la autorice como usuario de base de datos.  
  
Para conceder acceso a Mary, cambie a la base de datos **TestData** y, a continuación, use la instrucción CREATE USER para asignar su inicio de sesión a un usuario denominado Mary.  
  
### <a name="to-create-a-user-in-a-database"></a>Para crear un usuario en una base de datos  
  
Escriba y ejecute las siguientes instrucciones (reemplace `computer_name` con el nombre de su equipo) para conceder acceso a `Mary` a la base de datos `TestData` .
  
 ```sql  
 USE [TestData];  
 GO  
 
 CREATE USER [Mary] FOR LOGIN [computer_name\Mary];  
 GO    
 ```  
  
 Ahora, Mary tiene acceso a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y a la base de datos `TestData` .  


## <a name="create-views-and-stored-procedures"></a>Creación de vistas y procedimientos almacenados
Como administrador, puede ejecutar la instrucción SELECT desde la tabla **Products** y la vista **vw_Names** , y ejecutar el procedimiento **pr_Names** ; en cambio, Mary no puede hacerlo. Para conceder a Mary los permisos necesarios, use la instrucción GRANT.  

### <a name="grant-permission-to-stored-procedure"></a>Concesión de permiso a procedimientos almacenados  
Ejecute la siguiente instrucción para conceder a `Mary` el permiso `EXECUTE` para el procedimiento almacenado `pr_Names` .
  
  ```sql  
  GRANT EXECUTE ON pr_Names TO Mary;  
  GO  
  ```  
  
En este escenario, Mary solo puede tener acceso a la tabla **Products** si utiliza el procedimiento almacenado. Si desea que Mary pueda ejecutar una instrucción SELECT con la vista, también debe ejecutar `GRANT SELECT ON vw_Names TO Mary`. Para quitar el acceso a objetos de base de datos, use la instrucción REVOKE.  
  
> [!NOTE]  
> Si la tabla, la vista y el procedimiento almacenado no son propiedad del mismo esquema, la concesión de permisos es más compleja.  
  
### <a name="about-grant"></a>Acerca de GRANT  
Para ejecutar un procedimiento almacenado, debe tener permiso EXECUTE. Para tener acceso a datos y cambiarlos, debe tener permisos SELECT, INSERT, UPDATE y DELETE. La instrucción GRANT también se usa para otros permisos, como el permiso para crear tablas.  
  
## <a name="next-steps"></a>Pasos siguientes
En el siguiente artículo se muestra cómo quitar objetos de base de datos creados en otras lecciones. 

Vaya al siguiente artículo para más información:
> [!div class="nextstepaction"]
>[Pasos siguientes](lesson-3-deleting-database-objects.md)
  
