---
title: Crear un inicio de sesión para SQLRUserGroup - SQL Server Machine Learning Services
description: Para las conexiones de bucle invertido mediante autenticación implícita, cree un inicio de sesión en SQL Server para SQLRUserGroup, para que una cuenta de trabajo puede iniciar sesión con el servidor, para la conversión de identidad al usuario que realiza la llamada.
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/25/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 62dd1ddf61c3cc2e1340619566ad9f4dcce062b7
ms.sourcegitcommit: 32a55df1275ad169bb1457243dc8caa8b48b206f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/28/2019
ms.locfileid: "55147050"
---
# <a name="create-a-login-for-sqlrusergroup"></a>Crear un inicio de sesión para SQLRUserGroup
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Crear un [inicio de sesión en SQL Server](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/create-a-login) para [SQLRUserGroup](../concepts/security.md#sqlrusergroup) cuando un [bucle de espera de conexión](../../advanced-analytics/concepts/security.md#implied-authentication) en el script especifica un *conexión de confianza*, y la identidad utilizada para ejecutar un objeto que contiene el código es una cuenta de usuario de Windows.

Las conexiones son aquellos que tengan de confianza `Trusted_Connection=True` en la cadena de conexión. Cuando SQL Server recibe una solicitud que especifica una conexión de confianza, comprueba si la identidad del usuario actual de Windows tiene un inicio de sesión. Para ejecutar como una cuenta de trabajo de procesos externos (como MSSQLSERVER01 desde **SQLRUserGroup**), se produce un error en la solicitud porque esas cuentas no tienen un inicio de sesión de forma predeterminada.

Puede solucionar el error de conexión mediante la creación de un inicio de sesión para **SQLServerRUserGroup**. Para obtener más información acerca de las identidades y los procesos externos, consulte [información general de seguridad para el marco de extensibilidad](../concepts/security.md).

> [!Note]
> Asegúrese de que **SQLRUserGroup** tiene permisos "Permitir inicio de sesión localmente". De forma predeterminada, este permiso se concede a todos los nuevos usuarios locales, pero algunas directivas de grupo más estrictas a las organizaciones podrían deshabilitar este derecho.

## <a name="create-a-login"></a>Crea un inicio de sesión

1. En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], en el Explorador de objetos, expanda **Seguridad**, haga clic con el botón derecho en **Inicios de sesión**y seleccione **Nuevo inicio de sesión**.

2. En el **inicio de sesión - nuevo** cuadro de diálogo, seleccione **búsqueda**. (No escriba nada en el cuadro aún.)
    
     ![Haga clic en Buscar para agregar el nuevo inicio de sesión para el aprendizaje automático](media/implied-auth-login1.png "haga clic en Buscar para agregar el nuevo inicio de sesión para el aprendizaje automático")

3. En el **Seleccionar usuario o grupo** cuadro, haga clic en el **tipos de objeto** botón.

     ![Buscar tipos de objeto para agregar el nuevo inicio de sesión para el aprendizaje automático](media/implied-auth-login2.png "buscar tipos de objeto para agregar el nuevo inicio de sesión para el aprendizaje automático")

4. En el **tipos de objeto** cuadro de diálogo, seleccione **grupos**. Desactive todas las demás casillas.

     ![Seleccione los grupos en el cuadro de diálogo tipos de objeto](media/implied-auth-login3.png "seleccionar grupos en el cuadro de diálogo tipos de objeto")

4. Haga clic en **avanzadas**, compruebe que la ubicación de búsqueda es el equipo actual y, a continuación, haga clic en **Buscar ahora**.

     ![Haga clic en Buscar ahora para obtener la lista de grupos de](media/implied-auth-login4.png "haga clic en Buscar ahora para obtener la lista de grupos")

5. Desplácese por la lista de cuentas de grupo en el servidor hasta que encuentre una que empiece con `SQLRUserGroup`.
    
    + El nombre del grupo al que está asociado con el servicio Launchpad para la _instancia predeterminada_ siempre **SQLRUserGroup**, independientemente de si ha instalado R, Python o ambos. Seleccione esta cuenta solo la instancia predeterminada.
    + Si usas un _instancia con nombre_, el nombre de instancia se anexa al nombre del nombre del grupo de trabajo de forma predeterminada, `SQLRUserGroup`. Por ejemplo, si la instancia se denomina "MLTEST", el nombre del grupo de usuario predeterminada para esta instancia sería **SQLRUserGroupMLTest**.
 
    ![Ejemplo de grupos de servidor](media/implied-auth-login5.png "ejemplo de grupos de servidor")
   
5. Haga clic en **Aceptar** para cerrar el cuadro de diálogo de búsqueda avanzada.

    > [!IMPORTANT]
    > Asegúrese de que ha seleccionado la cuenta correcta para la instancia. Cada instancia puede usar solo su propio servicio Launchpad y el grupo creado para ese servicio. Las instancias no pueden compartir una cuenta de servicio o de trabajo de Launchpad.

6. Haga clic en **Aceptar** otra vez para cerrar el **Seleccionar usuario o grupo** cuadro de diálogo.

7. En el **inicio de sesión - nuevo** cuadro de diálogo, haga clic en **Aceptar**. De forma predeterminada, el inicio de sesión se asigna al rol **público** y tiene permiso para conectarse al motor de base de datos.

## <a name="next-steps"></a>Pasos siguientes

+ [Información general sobre seguridad](../concepts/security.md)
+ [Marco de extensibilidad](../concepts/extensibility-framework.md)
