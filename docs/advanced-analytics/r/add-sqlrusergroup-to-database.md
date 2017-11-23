---
title: Agregar SQLRUserGroup como un usuario de base de datos | Documentos de Microsoft
ms.custom: 
ms.date: 11/13/2017
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- "autenticación implícita"
- SQLRUserGroup
ms.assetid: 4d773c74-c779-4fc2-b1b6-ec4b4990950d
caps.latest.revision: "1"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Active
ms.openlocfilehash: 97a571a9a91ac31e955f6833e27a975f87267218
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="add-sqlrusergroup-as-a-database-user"></a>Agregar SQLRUserGroup como un usuario de base de datos

Durante la instalación de [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)] o [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)], se crean nuevas cuentas de usuario de Windows para ejecutar tareas en el token de seguridad de la [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] servicio. Cuando un usuario envía un script desde un cliente externo, de aprendizaje automático [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] activa una cuenta de trabajo disponible, lo asigna a la identidad del usuario que realiza la llamada y se ejecuta la secuencia de comandos en nombre del usuario. Este nuevo servicio del motor de base de datos admite la ejecución segura de scripts externos, denominado *autenticación implícita*.

Puede ver estas cuentas en el grupo de usuarios de Windows **SQLRUserGroup**. De forma predeterminada, se crean 20 cuentas de trabajo, que normalmente es más que suficiente para ejecutar código R trabajos.

Sin embargo, si necesita ejecutar scripts de R desde un cliente de ciencia de datos remotos y usa la autenticación de Windows, debe conceder estas cuentas de trabajo permiso para iniciar sesión en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia en su nombre.

## <a name="add-sqlrusergroup-as-a-sql-server-login"></a>Agregar SQLRUserGroup como un inicio de sesión de SQL Server

1. En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], en el Explorador de objetos, expanda **Seguridad**, haga clic con el botón derecho en **Inicios de sesión**y seleccione **Nuevo inicio de sesión**.

2. En el **inicio de sesión - nuevo** cuadro de diálogo, seleccione **búsqueda**. (No escriba nada en el cuadro aún.)
    
     ![Haga clic en Buscar para agregar el nuevo inicio de sesión para el aprendizaje automático](media/implied-auth-login1.png "haga clic en Buscar para agregar el nuevo inicio de sesión para el aprendizaje automático")

3. En el **Seleccionar usuario o grupo** cuadro, haga clic en el **tipos de objetos** botón.

     ![Buscar tipos de objeto para agregar el nuevo inicio de sesión para el aprendizaje automático](media/implied-auth-login2.png "buscar tipos de objeto para agregar el nuevo inicio de sesión para el aprendizaje automático")

4. En el **tipos de objeto** cuadro de diálogo, seleccione **grupos**. Desactive todas las demás casillas.

     ![Seleccione grupos en el cuadro de diálogo tipos de objeto](media/implied-auth-login3.png "seleccionar grupos en el cuadro de diálogo tipos de objeto")

4. Haga clic en **avanzadas**, compruebe que la ubicación de búsqueda es el equipo actual y, a continuación, haga clic en **Buscar ahora**.

     ![Haga clic en Buscar ahora para obtener la lista de grupos de](media/implied-auth-login4.png "haga clic en Buscar ahora para obtener la lista de grupos")

5. Desplácese por la lista de cuentas de grupo en el servidor hasta que encuentre una que comience con `SQLRUserGroup`.
    
    + El nombre del grupo que esté asociada con el servicio Launchpad para la _instancia predeterminada_ es siempre **SQLRUserGroup**. Seleccione esta cuenta solo para la instancia predeterminada.
    + Si usas un _con el nombre de instancia_, el nombre de instancia se anexa al nombre predeterminado `SQLRUserGroup`. Por lo tanto, si la instancia se denomina "MLTEST", el nombre del grupo de usuario predeterminada para esta instancia sería **SQLRUserGroupMLTest**.
 
     ![Ejemplo de grupos de servidor](media/implied-auth-login5.png "ejemplo de grupos de servidor")
   
5. Haga clic en **Aceptar** para cerrar el cuadro de diálogo de búsqueda avanzada.

    > [!IMPORTANT]
    > Asegúrese de que ha seleccionado la cuenta correcta para la instancia. Cada instancia puede usar solo su propio servicio de Launchpad y el grupo creado para ese servicio. Instancias no pueden compartir una cuenta de servicio o de trabajo de Launchpad.

6. Haga clic en **Aceptar** otra vez para cerrar el **Seleccionar usuario o grupo** cuadro de diálogo.

7. En el **inicio de sesión - nuevo** cuadro de diálogo, haga clic en **Aceptar**. De forma predeterminada, el inicio de sesión se asigna al rol **público** y tiene permiso para conectarse al motor de base de datos.

## <a name="change-the-number-of-worker-accounts-in-sqlrusergroup"></a>Cambiar el número de cuentas de trabajo en SQLRUserGroup

Si va a hacer un uso intensivo de aprendizaje automático, puede aumentar el número de cuentas utilizadas para ejecutar scripts externos, como se describe en este artículo: 

+ [Modificar el grupo de cuentas de usuario para el aprendizaje automático](modify-the-user-account-pool-for-sql-server-r-services.md)

De forma predeterminada, se crean 20 cuentas, que es compatible con 20 sesiones simultáneas. Tareas de ejecución en paralelo no consuman cuentas adicionales. Por ejemplo, si un usuario ejecuta una tarea de puntuación que utiliza el procesamiento en paralelo, se reutiliza la misma cuenta de trabajo para todos los subprocesos.