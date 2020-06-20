---
title: Conectarse a SQL Server cuando los administradores del sistema no tienen acceso | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- sa account
- connecting when locked out [SQL Server]
- locked out [SQL Server]
ms.assetid: c0c0082e-b867-480f-a54b-79f2a94ceb67
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 300e1b133691d91bf3955fbdd1fd6fbe24274177
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84935466"
---
# <a name="connect-to-sql-server-when-system-administrators-are-locked-out"></a>Conectarse a SQL Server cuando los administradores del sistema no tienen acceso
  En este tema se describe cómo puede recobrar el acceso a [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] como administrador del sistema. Un administrador del sistema puede perder el acceso a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debido a una de las razones siguientes:  
  
-   Por equivocación se han quitado todos los inicios de sesión que son miembros del rol fijo de servidor sysadmin.  
  
-   Por equivocación se han quitado todos los grupos de Windows que son miembros del rol fijo de servidor sysadmin.  
  
-   Los inicios de sesión que son miembros del rol fijo de servidor sysadmin son para individuos que han dejado la compañía o no están disponibles.  
  
-   La cuenta sa está deshabilitada o nadie conoce la contraseña.  
  
 Una manera de recobrar el acceso es reinstalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y adjuntar todas las bases de datos a la nueva instancia. Esta solución requiere mucho tiempo y, para recuperar los inicios de sesión, podría ser necesario restaurar la base de datos maestra a partir de una copia de seguridad. Si la copia de seguridad de la base de datos maestra es anterior, podría no tener toda la información. Si es más reciente, podría tener los mismos inicios de sesión que la instancia anterior; por consiguiente, los administradores aún no tendrán acceso.  
  
## <a name="resolution"></a>Solución  
 Inicie la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en modo de usuario único usando las opciones **-m** o **-f** . A continuación, cualquier miembro del grupo local de administradores del equipo puede conectarse a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como miembro del rol fijo de servidor sysadmin.  
  
> [!NOTE]  
>  Cuando inicie una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en modo de usuario único, detenga primero el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] : de lo contrario, el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podría conectarse primero e impedir que se conecte como un segundo usuario.  
  
 Cuando use la opción **-m** con **sqlcmd** o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], puede limitar las conexiones a una aplicación cliente especificada. Por ejemplo, **-m"sqlcmd"** limita las conexiones a una conexión única y esa conexión se debe identificar como el programa cliente **sqlcmd** . Use esta opción cuando esté iniciando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en modo de usuario único y una aplicación cliente desconocida esté usando la única conexión disponible. Para conectarse a través del Editor de consultas en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], use **-m"Microsoft SQL Server Management Studio - Query"** .  
  
> [!IMPORTANT]  
>  No use esta opción como una característica de seguridad. La aplicación cliente proporciona el nombre de la misma y puede proporcionar un nombre falso como parte de la cadena de conexión.  
  
 Para obtener instrucciones detalladas sobre cómo iniciar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el modo de usuario único, vea [Configurar opciones de inicio del servidor &#40;Administrador de configuración de SQL Server&#41;](scm-services-configure-server-startup-options.md).  
  
## <a name="step-by-step-instructions"></a>Instrucciones paso a paso  
 Las instrucciones siguientes describen el proceso para conectarse a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] que se ejecuta en Windows 8 o posterior. Se proporcionan pequeñas modificaciones para las versiones anteriores de SQL Server o de Windows. Estas instrucciones deben realizarse mientras se tiene iniciada sesión en Windows como miembro del grupo local de administradores y en ellas se da por supuesto que [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] está instalado en el equipo.  
  
1.  Desde la página de inicio, inicie [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. En el menú **Ver** , seleccione **Servidores registrados**. (Si el servidor aún no está registrado, haga clic con el botón derecho en **Grupos de servidores locales**, seleccione **Tareas**y, después, haga clic en **Registrar servidores locales**).  
  
2.  En el área Servidores registrados, haga clic con el botón derecho en el servidor y, después, haga clic en **Administrador de configuración de SQL Server**. Se debe solicitar permiso para ejecutarse como administrador y, a continuación, abrir el programa Administrador de configuración.  
  
3.  Cierre [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
4.  En el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , en el panel izquierdo, seleccione **Servicios de SQL Server**. En el panel derecho, busque la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. (La instancia predeterminada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incluye **(MSSQLSERVER)** después del nombre del equipo. Las instancias con nombre aparecen en mayúsculas con el mismo nombre que tienen en Servidores registrados). Haga clic con el botón derecho en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y, después, haga clic en **Propiedades**.  
  
5.  En la pestaña **parámetros de inicio** , en el cuadro **Especifique un parámetro de inicio** , escriba `-m` y, a continuación, haga clic en `Add` . (Es un guion y a continuación una letra m minúscula).  
  
    > [!NOTE]  
    >  En algunas versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no hay ninguna pestaña **Parámetros de inicio** . En ese caso, en la pestaña **Opciones avanzadas** , haga doble clic en **Parámetros de inicio**. Los parámetros se abrirán en una ventana muy pequeña. Tenga cuidado de no cambiar ninguno de los parámetros existentes. Al final, agregue un nuevo parámetro `;-m` y haga clic en `OK`. (Es un punto y coma, después un guion y a continuación una letra m minúscula).  
  
6.  Haga clic en `OK` y después del mensaje para reiniciar, haga clic con el botón secundario en el nombre del servidor y, a continuación, haga clic en **reiniciar**.  
  
7.  Después de que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se haya reiniciado, el servidor se encontrará en modo de usuario único. Asegúrese de que el Agente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se esté ejecutando. Si está iniciado, usará su única conexión.  
  
8.  En la pantalla de inicio de Windows 8, haga clic con el botón secundario en el icono de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. En la parte inferior de la pantalla, seleccione **Ejecutar como administrador**. (Esto pasará sus credenciales de administrador a SSMS).  
  
    > [!NOTE]  
    >  En versiones anteriores de Windows, la opción **Ejecutar como administrador** aparece como un submenú.  
  
     En algunas configuraciones, SSMS intentará realizar varias conexiones. Se producirá un error en varias conexiones porque [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está en modo de usuario único. Puede seleccionar una de las siguientes acciones para realizar. Realice una de las acciones siguientes.  
  
    1.  Conectar con el Explorador de objetos mediante la autenticación de Windows (que incluye sus credenciales de administrador). Expanda **Seguridad**e **Inicios de sesión**y haga doble clic en su propio inicio de sesión. En la página **roles de servidor** , seleccione y, `sysadmin` a continuación, haga clic en `OK` .  
  
    2.  En lugar de conectar con el Explorador de objetos, conectar con una ventana de consulta mediante la autenticación de Windows (que incluye sus credenciales de administrador). (Solo puede conectarse de esta forma si no se conectó con Explorador de objetos). Ejecute código como el siguiente para agregar un nuevo inicio de sesión de autenticación de Windows que sea miembro del `sysadmin` rol fijo de servidor. El ejemplo siguiente agrega un usuario de dominio denominado `CONTOSO\PatK`.  
  
        ```  
        CREATE LOGIN [CONTOSO\PatK] FROM WINDOWS;  
        ALTER SERVER ROLE sysadmin ADD MEMBER [CONTOSO\PatK];  
        ```  
  
    3.  Si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se ejecuta en modo de autenticación mixto, conectar con una ventana de consulta mediante la autenticación de Windows (que incluye sus credenciales de administrador). Ejecute código como el siguiente para crear un nuevo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Inicio de sesión de autenticación que sea miembro del `sysadmin` rol fijo de servidor.  
  
        ```  
        CREATE LOGIN TempLogin WITH PASSWORD = '************';  
        ALTER SERVER ROLE sysadmin ADD MEMBER TempLogin;  
        ```  
  
        > [!WARNING]  
        >  Reemplace ************ con una contraseña segura.  
  
    4.  Si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se está ejecutando en modo de autenticación mixta y desea restablecer la contraseña de la `sa` cuenta, conéctese con una ventana de consulta mediante la autenticación de Windows (que incluye sus credenciales de administrador). Cambie la contraseña de la `sa` cuenta con la siguiente sintaxis.  
  
        ```  
        ALTER LOGIN sa WITH PASSWORD = '************';  
        ```  
  
        > [!WARNING]  
        >  Reemplace ************ con una contraseña segura.  
  
9. En los pasos siguientes se vuelve a cambiar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al modo multiusuario. Cierre SSMS.  
  
10. En el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , en el panel izquierdo, seleccione **Servicios de SQL Server**. En el panel derecho, haga clic con el botón derecho en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]y, después, haga clic en **Propiedades**.  
  
11. En la pestaña **parámetros de inicio** , en el cuadro **parámetros existentes** , seleccione `-m` y, a continuación, haga clic en `Remove` .  
  
    > [!NOTE]  
    >  En algunas versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no hay ninguna pestaña **Parámetros de inicio** . En ese caso, en la pestaña **Opciones avanzadas** , haga doble clic en **Parámetros de inicio**. Los parámetros se abrirán en una ventana muy pequeña. Quite el `;-m` que agregó anteriormente y, a continuación, haga clic en `OK` .  
  
12. Haga clic con el botón derecho en el nombre del servidor y, después, haga clic en **Reiniciar**.  
  
 Ahora debería poder conectarse normalmente con una de las cuentas que ahora es miembro del `sysadmin` rol fijo de servidor.  
  
## <a name="see-also"></a>Consulte también  
 [Iniciar SQL Server en modo de usuario único](start-sql-server-in-single-user-mode.md)   
 [Opciones de inicio del servicio de motor de base de datos](database-engine-service-startup-options.md)  
  
  
