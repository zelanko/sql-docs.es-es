---
title: Creación de un inicio de sesión para SQLRUserGroup
description: En el caso de las conexiones de bucle invertido con autenticación implícita, cree un inicio de sesión en SQL Server para SQLRUserGroup, de modo que una cuenta de trabajo pueda iniciar sesión en el servidor para realizar la conversión de identidad en el usuario que realiza la llamada.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/25/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a5194f251b7ea47e0d9485446b8957e96037ded0
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714959"
---
# <a name="create-a-login-for-sqlrusergroup"></a>Creación de un inicio de sesión para SQLRUserGroup
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Cree un [inicio de sesión en SQL Server](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/create-a-login) para [SQLRUserGroup](../concepts/security.md#sqlrusergroup) cuando una [conexión de bucle invertido](../../advanced-analytics/concepts/security.md#implied-authentication) del script especifique una *conexión de confianza* y la identidad que se usa para ejecutar un objeto que contiene el código sea una cuenta de usuario de Windows.

Las conexiones de confianza son aquellas que tienen `Trusted_Connection=True` en la cadena de conexión. Cuando SQL Server recibe una solicitud que especifica una conexión de confianza, comprueba si la identidad del usuario actual de Windows tiene un inicio de sesión. En el caso de los procesos externos que se ejecutan como una cuenta de trabajo (como MSSQLSERVER01 de **SQLRUserGroup**), se produce un error en la solicitud, ya que esas cuentas no tienen un inicio de sesión de forma predeterminada.

Puede evitar el error de conexión creando un inicio de sesión para **SQLServerRUserGroup**. Para obtener más información sobre las identidades y los procesos externos, vea [Información general sobre seguridad para el marco de extensibilidad](../concepts/security.md).

> [!Note]
> Asegúrese de que **SQLRUserGroup** tiene los permisos "Permitir el inicio de sesión local". De forma predeterminada, este derecho se concede a todos los usuarios locales nuevos, pero algunas de las directivas de grupo de las organizaciones más estrictas podrían deshabilitarlo.

## <a name="create-a-login"></a>Creación de un inicio de sesión

1. En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], en el Explorador de objetos, expanda **Seguridad**, haga clic con el botón derecho en **Inicios de sesión**y seleccione **Nuevo inicio de sesión**.

2. En el cuadro de diálogo **Inicio de sesión - Nuevo**, haga clic en **Buscar**. (No escriba nada en el cuadro todavía).
    
     ![Haga clic en buscar para agregar un nuevo inicio de sesión para aprendizaje automático](media/implied-auth-login1.png "Click search to add new login for machine learning")

3. En el cuadro **Seleccionar usuario o grupo**, haga clic en el botón **Tipos de objeto**.

     ![Buscar tipos de objeto para agregar un nuevo inicio de sesión para aprendizaje automático](media/implied-auth-login2.png "Search object types to add new login for machine learning")

4. En el cuadro de diálogo **Tipos de objeto**, seleccione **Grupos**. Desactive las demás casillas.

     ![Seleccione Grupos en el cuadro de diálogo Tipos de objeto](media/implied-auth-login3.png "Select Groups in Object Types dialog box")

4. Haga clic en **Avanzadas**, compruebe que la ubicación para buscar es el equipo actual y, después, haga clic en **Buscar ahora**.

     ![Haga clic en Buscar ahora para obtener una lista de grupos](media/implied-auth-login4.png "Click Find Now to get list of groups")

5. Desplácese por la lista de cuentas del grupo en el servidor hasta que encuentre una que comience por `SQLRUserGroup`.
    
    + El nombre del grupo que está asociado con el servicio Launchpad para la _instancia predeterminada_ siempre es **SQLRUserGroup**, independientemente de si instaló R, Python o ambos. Seleccione esta cuenta solo para la instancia predeterminada.
    + Si usa una _instancia con nombre_, el nombre de la instancia se anexa al nombre del grupo de trabajo predeterminado, `SQLRUserGroup`. Por ejemplo, si la instancia se denomina "MLTEST", el nombre del grupo de usuarios predeterminado para esta instancia sería **SQLRUserGroupMLTest**.
 
    ![Ejemplo de grupos en el servidor](media/implied-auth-login5.png "Example of groups on server")
   
5. Haga clic en **Aceptar** para cerrar el cuadro de diálogo de búsqueda avanzada.

    > [!IMPORTANT]
    > Asegúrese de que ha seleccionado la cuenta correcta para la instancia. Cada instancia solo puede utilizar su propio servicio Launchpad y el grupo creado para ese servicio. Las instancias no pueden compartir el servicio de Launchpad ni las cuentas de trabajo.

6. Vuelva a hacer clic en **Aceptar** para cerrar el cuadro de diálogo **Seleccionar usuario o grupo**.

7. En el cuadro de diálogo **Inicio de sesión: Nuevo**, haga clic en **Aceptar**. De forma predeterminada, el inicio de sesión se asigna al rol **público** y tiene permiso para conectarse al motor de base de datos.

## <a name="next-steps"></a>Pasos siguientes

+ [Información general sobre seguridad](../concepts/security.md)
+ [Marco de extensibilidad](../concepts/extensibility-framework.md)
