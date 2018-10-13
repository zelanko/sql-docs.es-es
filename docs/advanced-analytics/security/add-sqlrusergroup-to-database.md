---
title: Agregar SQLRUserGroup como un usuario de base de datos (SQL Server Machine Learning) | Microsoft Docs
description: Cómo agregar SQLRUserGroup como un usuario de base de datos de SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/10/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: fc5294453def64d13cc43a74a8a5fb299c3e23e3
ms.sourcegitcommit: 485e4e05d88813d2a8bb8e7296dbd721d125f940
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/11/2018
ms.locfileid: "49100326"
---
# <a name="add-sqlrusergroup-as-a-database-user"></a>Agregar SQLRUserGroup como usuario de base de datos
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Crear un inicio de sesión de base de datos para el [SQLRUserGroup](../concepts/security.md#sqlrusergroup) para permitir las conexiones de confianza que se originan desde scripts de R y Python, cuando el destino son los datos o las operaciones en la instancia de SQL Server. 

Para los scripts que contienen cadenas de conexión con los inicios de sesión de SQL Server o un nombre de usuario completamente especificada y una contraseña, no es necesario crear un inicio de sesión.

## <a name="when-a-login-is-required"></a>Cuando se requiere un inicio de sesión

Si el script de R o Python incluye una cadena de conexión especifica una conexión de confianza (por ejemplo, "Trusted_Connection = True"), una configuración adicional es necesaria para la presentación correcta de la identidad del usuario a SQL Server. Para los procesos externos que se ejecutan en un **SQLRUserGroup** cuenta de trabajo, como MSSQLSERVER01, el usuario de confianza se presenta como la identidad del trabajo. Dado que esta identidad no tiene derechos de inicio de sesión en SQL Server, de confianza se producirá un error en las conexiones a menos que agregue **SQLRUserGroup** como un usuario de base de datos. Para obtener más información, consulte [ *autenticación implícita*](../../advanced-analytics/concepts/security.md#implied-authentication).

Recuerde que Launchpad mantiene una asignación del usuario original que invocó el script y la cuenta de trabajo que ejecuta el proceso. Cuando se complete correctamente la conexión de confianza para la cuenta de trabajo, la identidad del usuario que realiza la llamada original asume y se usa para recuperar los datos. No es necesario conceder permisos db_datareader para **SQLRUserGroup**.

> [!Note]
>  Asegúrese de que **SQLRUserGroup** tiene permisos "Permitir inicio de sesión localmente". De forma predeterminada, este permiso se concede a todos los nuevos usuarios locales, pero en algunas organizaciones podrían aplicarse directivas de grupo más estrictas.

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
    + Si usas un _instancia con nombre_, el nombre de instancia se anexa al nombre del nombre del grupo de trabajo de forma predeterminada, `SQLRUserGroup`. Por lo tanto, si la instancia se denomina "MLTEST", el nombre del grupo de usuario predeterminada para esta instancia sería **SQLRUserGroupMLTest**.
 
     ![Ejemplo de grupos de servidor](media/implied-auth-login5.png "ejemplo de grupos de servidor")
   
5. Haga clic en **Aceptar** para cerrar el cuadro de diálogo de búsqueda avanzada.

    > [!IMPORTANT]
    > Asegúrese de que ha seleccionado la cuenta correcta para la instancia. Cada instancia puede usar solo su propio servicio Launchpad y el grupo creado para ese servicio. Las instancias no pueden compartir una cuenta de servicio o de trabajo de Launchpad.

6. Haga clic en **Aceptar** otra vez para cerrar el **Seleccionar usuario o grupo** cuadro de diálogo.

7. En el **inicio de sesión - nuevo** cuadro de diálogo, haga clic en **Aceptar**. De forma predeterminada, el inicio de sesión se asigna al rol **público** y tiene permiso para conectarse al motor de base de datos.