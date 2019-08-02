---
title: Creación de un inicio de sesión para SQLRUserGroup
description: En el caso de las conexiones de bucle invertido con autenticación implícita, cree un inicio de sesión en SQL Server para SQLRUserGroup, de modo que una cuenta de trabajo pueda iniciar sesión en el servidor para realizar la conversión de identidad en el usuario que realiza la llamada.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/25/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a5194f251b7ea47e0d9485446b8957e96037ded0
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714959"
---
# <a name="create-a-login-for-sqlrusergroup"></a>Creación de un inicio de sesión para SQLRUserGroup
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Cree un [Inicio de sesión en SQL Server](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/create-a-login) para [SQLRUserGroup](../concepts/security.md#sqlrusergroup) cuando una [conexión de bucle](../../advanced-analytics/concepts/security.md#implied-authentication) invertido en el script especifica una *conexión de confianza*y la identidad que se usa para ejecutar un objeto contiene el código es una cuenta de usuario de Windows.

Las conexiones de confianza son `Trusted_Connection=True` las que tienen la cadena de conexión. Cuando SQL Server recibe una solicitud que especifica una conexión de confianza, comprueba si la identidad del usuario actual de Windows tiene un inicio de sesión. En el caso de los procesos externos que se ejecutan como una cuenta de trabajo (por ejemplo, MSSQLSERVER01 de **SQLRUserGroup**), se produce un error en la solicitud porque esas cuentas no tienen un inicio de sesión de forma predeterminada.

Puede evitar el error de conexión creando un inicio de sesión para **SQLServerRUserGroup**. Para obtener más información sobre las identidades y los procesos externos, vea [información general sobre seguridad para el marco de extensibilidad](../concepts/security.md).

> [!Note]
> Asegúrese de que **SQLRUserGroup** tenga los permisos "permitir el inicio de sesión local". De forma predeterminada, este derecho se concede a todos los nuevos usuarios locales, pero algunas de las directivas de grupo de las organizaciones más estrictas podrían deshabilitar este derecho.

## <a name="create-a-login"></a>Creación de un inicio de sesión

1. En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], en el Explorador de objetos, expanda **Seguridad**, haga clic con el botón derecho en **Inicios de sesión**y seleccione **Nuevo inicio de sesión**.

2. En el cuadro de diálogo **Inicio de sesión-nuevo** , seleccione **Buscar**. (No escriba nada en el cuadro todavía).
    
     ![Haga clic en buscar para agregar un nuevo inicio de sesión para machine learning](media/implied-auth-login1.png "Haga clic en buscar para agregar un nuevo inicio de sesión para machine learning")

3. En el cuadro **Seleccionar usuario o grupo** , haga clic en el botón **tipos de objeto** .

     ![Buscar tipos de objeto para agregar un nuevo inicio de sesión para machine learning](media/implied-auth-login2.png "Buscar tipos de objeto para agregar un nuevo inicio de sesión para machine learning")

4. En el cuadro de diálogo **tipos de objeto** , seleccione **grupos**. Desactive todas las demás casillas.

     ![Cuadro de diálogo Seleccionar grupos en tipos de objeto](media/implied-auth-login3.png "Cuadro de diálogo Seleccionar grupos en tipos de objeto")

4. Haga clic en **Opciones avanzadas**, compruebe que la ubicación para buscar es el equipo actual y, a continuación, haga clic en **Buscar ahora**.

     ![Haga clic en Buscar ahora para obtener una lista de grupos] . (media/implied-auth-login4.png "Haga clic en Buscar ahora para obtener una lista de grupos") .

5. Desplácese por la lista de cuentas de grupo en el servidor hasta que encuentre una `SQLRUserGroup`a partir de.
    
    + El nombre del grupo que está asociado con el servicio Launchpad para la _instancia predeterminada_ es siempre **SQLRUserGroup**, independientemente de Si instaló R o Python o ambos. Seleccione esta cuenta solo para la instancia predeterminada.
    + Si usa una _instancia con nombre_, el nombre de la instancia se anexa al nombre del grupo de trabajo predeterminado, `SQLRUserGroup`. Por ejemplo, si la instancia se denomina "MLTEST", el nombre del grupo de usuarios predeterminado para esta instancia sería **SQLRUserGroupMLTest**.
 
    ![Ejemplo de grupos en el servidor](media/implied-auth-login5.png "Ejemplo de grupos en el servidor")
   
5. Haga clic en **Aceptar** para cerrar el cuadro de diálogo búsqueda avanzada.

    > [!IMPORTANT]
    > Asegúrese de que ha seleccionado la cuenta correcta para la instancia. Cada instancia solo puede utilizar su propio servicio Launchpad y el grupo creado para ese servicio. Las instancias no pueden compartir las cuentas de servicio o de trabajo de Launchpad.

6. Haga clic en **Aceptar** una vez más para cerrar el cuadro de diálogo **Seleccionar usuario o grupo** .

7. En el cuadro de diálogo **Inicio de sesión-nuevo** , haga clic en **Aceptar**. De forma predeterminada, el inicio de sesión se asigna al rol **público** y tiene permiso para conectarse al motor de base de datos.

## <a name="next-steps"></a>Pasos siguientes

+ [Información general sobre seguridad](../concepts/security.md)
+ [Marco de extensibilidad](../concepts/extensibility-framework.md)
