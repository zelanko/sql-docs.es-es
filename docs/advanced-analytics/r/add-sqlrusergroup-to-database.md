---
title: Agregar SQLRUserGroup como un usuario de base de datos | Documentos de Microsoft
ms.custom: 
ms.date: 12/21/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
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
ms.openlocfilehash: 7de60bccb72364e124656f03f043c03e812187db
ms.sourcegitcommit: ed9335fe62c0c8d94ee87006c6957925d09ee301
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/22/2017
---
# <a name="add-sqlrusergroup-as-a-database-user"></a>Agregar SQLRUserGroup como un usuario de base de datos

En este artículo se explica cómo conceder al grupo de cuentas de trabajo utilizada los servicios de aprendizaje de máquina de SQL Server los permisos necesitan para conectarse a la base de datos y ejecutar trabajos de R o Python en nombre del usuario.

## <a name="what-is-sqlrusergroup"></a>¿Qué es SQLRUserGroup?

Durante la instalación de [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)] o [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)], se crean nuevas cuentas de usuario de Windows para admitir la ejecución de R o Python script tareas en el token de seguridad de la [!INCLUDE[rsql_launchpad_md](../../includes/rsql-launchpad-md.md)] servicio.

Puede ver estas cuentas en el grupo de usuarios de Windows **SQLRUserGroup**. De forma predeterminada, se crean 20 cuentas de trabajo, que normalmente es más que suficiente para ejecutar el aprendizaje automático de trabajos.

Cuando un usuario envía un script desde un cliente externo, de aprendizaje automático [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] activa una cuenta de trabajo disponible, lo asigna a la identidad del usuario que realiza la llamada y se ejecuta la secuencia de comandos en nombre del usuario. Este nuevo servicio del motor de base de datos admite la ejecución segura de scripts externos, denominado *autenticación implícita*.

Sin embargo, si necesita ejecutar scripts de R o Python desde un cliente de ciencia de datos remotos, y está usando la autenticación de Windows, debe asignar a estas cuentas de trabajo permiso para iniciar sesión en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia en su nombre.

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
    
    + El nombre del grupo que esté asociada con el servicio Launchpad para la _instancia predeterminada_ siempre es **SQLRUserGroup**, independientemente de si ha instalado R, Python o ambos. Seleccione esta cuenta para la instancia predeterminada solo.
    + Si usas un _con el nombre de instancia_, el nombre de instancia se anexa al nombre del nombre del grupo de trabajo de forma predeterminada, `SQLRUserGroup`. Por lo tanto, si la instancia se denomina "MLTEST", el nombre del grupo de usuario predeterminada para esta instancia sería **SQLRUserGroupMLTest**.
 
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
