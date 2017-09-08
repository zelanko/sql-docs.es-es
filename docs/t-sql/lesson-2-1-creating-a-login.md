---
title: "Crear un inicio de sesión | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- creating a login
ms.assetid: a2512310-bdb6-41dc-858a-e866b2b58afc
caps.latest.revision: 16
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c8d1edc92b209fc73eb85af703058cc329a775cb
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="lesson-2-1---creating-a-login"></a>Lección 2-1: crear un inicio de sesión
Para tener acceso a [!INCLUDE[ssDE](../includes/ssde-md.md)], los usuarios necesitan un inicio de sesión. El inicio de sesión puede representar la identidad del usuario como una cuenta de Windows o como un miembro de un grupo de Windows, o el inicio de sesión puede ser un inicio de sesión de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que solo exista en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Siempre que sea posible, use la autenticación de Windows.  
  
De forma predeterminada, los administradores del equipo tienen acceso total a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para esta lección, deseamos tener un usuario con menos privilegios; por tanto, creará una nueva cuenta de autenticación de Windows local en el equipo. Para hacerlo, debe ser un administrador del equipo. A continuación, concederá al nuevo usuario acceso a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
### <a name="to-create-a-new-windows-account"></a>Para crear una cuenta de Windows nueva  
  
1.  Haga clic en **Inicio**y en **Ejecutar**, en el cuadro **Abrir** , escriba **%SystemRoot%\system32\compmgmt.msc /s**y, después, haga clic en **Aceptar** para abrir el programa Administración de equipos.  
  
2.  En **Herramientas del sistema**, expanda **Usuarios y grupos locales**, haga clic con el botón derecho en **Usuarios**y luego haga clic en **Nuevo usuario**.  
  
3.  En el cuadro **Nombre de usuario** , escriba **Mary**.  
  
4.  En los cuadros **Contraseña** y **Confirmar contraseña** , escriba una contraseña segura y, a continuación, haga clic en **Crear** para crear un nuevo usuario de Windows local.  
  
### <a name="to-create-a-login"></a>Para crear un inicio de sesión  
  
1.  En una ventana del Editor de consultas de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], escriba y ejecute el siguiente código reemplazando `computer_name` con el nombre del equipo. `FROM WINDOWS` indica que Windows autenticará al usuario. El argumento opcional `DEFAULT_DATABASE` conecta `Mary` con la base de datos `TestData` , a menos que la cadena de conexión indique otra base de datos. Esta instrucción introduce el punto y coma como una terminación opcional de una instrucción [!INCLUDE[tsql](../includes/tsql-md.md)] .  
  
    ```  
    CREATE LOGIN [computer_name\Mary]  
        FROM WINDOWS  
        WITH DEFAULT_DATABASE = [TestData];  
    GO  
    ```  
  
    Esto autoriza al nombre de usuario `Mary`, autenticado por el equipo, a tener acceso a esta instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Si existe más de una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] en el equipo, debe crear el inicio de sesión en cada instancia a la que `Mary` deba tener acceso.  
  
    > [!NOTE]  
    > Puesto que `Mary` no es una cuenta de dominio, este nombre de usuario solo puede autenticarse en este equipo.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
[Conceder acceso a una base de datos](../t-sql/lesson-2-2-granting-access-to-a-database.md)  
  
## <a name="see-also"></a>Vea también  
[CREATE LOGIN &#40;Transact-SQL&#41;](../t-sql/statements/create-login-transact-sql.md)  
[Elegir un modo de autenticación](../relational-databases/security/choose-an-authentication-mode.md)  
  
  
  

