---
title: Creación de un inicio de sesión para SQLRUserGroup
description: Cree un inicio de sesión en SQL Server para SQLRUserGroup, con autenticación implícita para iniciar sesión en el servidor, a fin de convertir la identidad al usuario que realiza la llamada.
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 01/25/2019
ms.topic: how-to
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: fcdb8353abe029291352f031d5261849514ef8fd
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/22/2020
ms.locfileid: "92195759"
---
# <a name="create-a-login-for-sqlrusergroup"></a>Creación de un inicio de sesión para SQLRUserGroup
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

Cree un [inicio de sesión en SQL Server](../../relational-databases/security/authentication-access/create-a-login.md) para [SQLRUserGroup](../concepts/security.md#sqlrusergroup) cuando una [conexión de bucle invertido](../../machine-learning/concepts/security.md#implied-authentication) del script especifique una *conexión de confianza* y la identidad que se usa para ejecutar un objeto que contiene el código sea una cuenta de usuario de Windows.

Las conexiones de confianza son aquellas que tienen `Trusted_Connection=True` en la cadena de conexión. Cuando SQL Server recibe una solicitud que especifica una conexión de confianza, comprueba si la identidad del usuario actual de Windows tiene un inicio de sesión. En el caso de los procesos externos que se ejecutan como una cuenta de trabajo (como MSSQLSERVER01 de **SQLRUserGroup**), se produce un error en la solicitud, ya que esas cuentas no tienen un inicio de sesión de forma predeterminada.

Puede evitar el error de conexión creando un inicio de sesión para **SQLServerRUserGroup**. Para obtener más información sobre las identidades y los procesos externos, vea [Información general sobre seguridad para el marco de extensibilidad](../concepts/security.md).

> [!Note]
> Asegúrese de que **SQLRUserGroup** tiene los permisos "Permitir el inicio de sesión local". De forma predeterminada, este derecho se concede a todos los usuarios locales nuevos, pero algunas de las directivas de grupo de las organizaciones más estrictas podrían deshabilitarlo.

## <a name="create-a-login"></a>Creación de un inicio de sesión

1. En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], en el Explorador de objetos, expanda **Seguridad**, haga clic con el botón derecho en **Inicios de sesión**y seleccione **Nuevo inicio de sesión**.

2. En el cuadro de diálogo **Inicio de sesión - Nuevo**, haga clic en **Buscar**. (No escriba nada en el cuadro todavía).
    
     ![Haga clic en buscar para agregar un nuevo inicio de sesión para aprendizaje automático](media/implied-auth-login1.png "Haga clic en buscar para agregar un nuevo inicio de sesión para aprendizaje automático")

3. En el cuadro **Seleccionar usuario o grupo**, haga clic en el botón **Tipos de objeto**.

     ![Busque tipos de objeto para agregar un nuevo inicio de sesión para aprendizaje automático](media/implied-auth-login2.png "Busque tipos de objeto para agregar un nuevo inicio de sesión para aprendizaje automático")

4. En el cuadro de diálogo **Tipos de objeto**, seleccione **Grupos**. Desactive las demás casillas.

     ![Seleccione Grupos en el cuadro de diálogo Tipos de objeto](media/implied-auth-login3.png "Seleccione Grupos en el cuadro de diálogo Tipos de objeto")

4. Haga clic en **Avanzadas**, compruebe que la ubicación para buscar es el equipo actual y, después, haga clic en **Buscar ahora**.

     ![Haga clic en Buscar ahora para obtener una lista de grupos](media/implied-auth-login4.png "Haga clic en Buscar ahora para obtener una lista de grupos")

5. Desplácese por la lista de cuentas del grupo en el servidor hasta que encuentre una que comience por `SQLRUserGroup`.
    
    + El nombre del grupo que está asociado con el servicio Launchpad para la _instancia predeterminada_ siempre es **SQLRUserGroup**, independientemente de si instaló R, Python o ambos. Seleccione esta cuenta solo para la instancia predeterminada.
    + Si usa una _instancia con nombre_, el nombre de la instancia se anexa al nombre del grupo de trabajo predeterminado, `SQLRUserGroup`. Por ejemplo, si la instancia se denomina "MLTEST", el nombre del grupo de usuarios predeterminado para esta instancia sería **SQLRUserGroupMLTest**.
 
    ![Ejemplo de grupos del servidor](media/implied-auth-login5.png "Ejemplo de grupos del servidor")
   
5. Haga clic en **Aceptar** para cerrar el cuadro de diálogo de búsqueda avanzada.

    > [!IMPORTANT]
    > Asegúrese de que ha seleccionado la cuenta correcta para la instancia. Cada instancia solo puede utilizar su propio servicio Launchpad y el grupo creado para ese servicio. Las instancias no pueden compartir el servicio de Launchpad ni las cuentas de trabajo.

6. Vuelva a hacer clic en **Aceptar** para cerrar el cuadro de diálogo **Seleccionar usuario o grupo**.

7. En el cuadro de diálogo **Inicio de sesión: Nuevo**, haga clic en **Aceptar**. De forma predeterminada, el inicio de sesión se asigna al rol **público** y tiene permiso para conectarse al motor de base de datos.

## <a name="next-steps"></a>Pasos siguientes

+ [Información general sobre seguridad](../concepts/security.md)
+ [Plataforma de extensibilidad](../concepts/extensibility-framework.md)