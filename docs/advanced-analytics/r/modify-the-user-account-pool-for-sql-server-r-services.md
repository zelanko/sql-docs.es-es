---
title: Modificar el grupo de cuentas de usuario de SQL Server R Services | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 58b79170-5731-46b5-af8c-21164d28f3b0
caps.latest.revision: 19
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 33e22f7edec807d046798d89a9cd5daa642e8d3b
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="modify-the-user-account-pool-for-sql-server-r-services"></a>Modificar el grupo de cuentas de usuario de SQL Server R Services
  Como parte del proceso de instalación de [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], se crea un *grupo de cuentas de usuario* de Windows para admitir la ejecución de tareas mediante el servicio [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]. El propósito de estas cuentas de trabajo es aislar la ejecución simultánea de scripts de R por parte de diferentes usuarios de SQL. 

En este tema se describen la configuración predeterminada, la seguridad y la capacidad de las cuentas de trabajo, y la manera de cambiar la configuración predeterminada.

## <a name="worker-accounts-used-by-r-services"></a>Cuentas de trabajo usadas por R Services   

El programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crea el grupo de cuentas de Windows para cada instancia en la que está instalado R Services. Por lo tanto, si ha instalado varias instancias que admiten R, habrá varios grupos de usuarios.

-   En una instancia predeterminada, el nombre del grupo es **SQLRUserGroup**. 
-   En una instancia con nombre, el nombre del grupo predeterminado tiene como sufijo el nombre de instancia, por ejemplo, **SQLRUserGroupMyInstanceName**. 

De forma predeterminada, el grupo de cuentas de usuario contiene 20 cuentas de usuario. En la mayoría de los casos, este número es más que suficiente para admitir sesiones de R, pero puede cambiar el número de cuentas.
-  En una instancia predeterminada, las cuentas individuales se denominan de **MSSQLSERVER01** a **MSSQLSERVER20**.  
-   En el caso de una instancia con nombre, las cuentas individuales reciben el nombre de la instancia, por ejemplo, de **MyInstanceName01** a **MyInstanceName20**.  

### <a name = "HowToChangeGroup"> </a>Cómo cambiar el número de cuentas de trabajo de R

Para modificar el número de usuarios del grupo de cuentas, debe modificar las propiedades del servicio [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] tal y como se describe a continuación.  
  
Las contraseñas asociadas con cada cuenta de usuario se generan aleatoriamente, pero puede cambiarlas más adelante, una vez que se hayan creado las cuentas.  
  
1. Abra el Administrador de configuración de SQL Server y seleccione **Servicios de SQL Server**.
2. Haga doble clic en el servicio SQL Server Launchpad y detenga el servicio si se está ejecutando. 
3.  En la pestaña **Servicio**, asegúrese de que el modo de inicio esté establecido en Automático. Se producirá un error en los scripts de R si Launchpad no se está ejecutando.
4.  Haga clic en la pestaña **Avanzado** y modifique el valor de **Recuento de usuarios externos** si es necesario. Esta opción de configuración controla cuántos usuarios diferentes de SQL pueden ejecutar consultas simultáneamente en R. El valor predeterminado es 20 cuentas.
5. Opcionalmente, puede establecer la opción **Restablecer contraseña de usuarios externos** en _Sí_ si su organización tiene una directiva que requiere cambiar las contraseñas periódicamente. De este modo, se regeneran las contraseñas cifradas que Launchpad mantiene para las cuentas de usuario. Para obtener más información, vea [Aplicar una directiva de contraseñas](#bkmk_EnforcePolicy).    
6.  Reiniciar el servicio.  

## <a name="managing-r-workload"></a>Administrar la carga de trabajo de R

El número de cuentas de este grupo determina el número de sesiones de R que pueden estar activas simultáneamente.  De forma predeterminada, se crean 20 cuentas, lo que significa que 20 usuarios diferentes pueden tener sesiones de R activas al mismo tiempo. Si prevé que más usuarios simultáneos ejecutarán scripts de R, puede aumentar el número de cuentas de trabajo. 

Cuando un mismo usuario ejecute simultáneamente varios scripts de R, todas las sesiones ejecutadas por dicho usuario usarán la misma cuenta de trabajo. Por ejemplo, un mismo usuario podría tener 100 scripts de R diferentes en ejecución al mismo tiempo (siempre y cuando los recursos lo permitan) con una sola cuenta de trabajo.

El número de cuentas de trabajo que se pueden admitir y el número de sesiones simultáneas de R que puede ejecutar un mismo usuario está limitado exclusivamente por los recursos del servidor.  Normalmente, la memoria es el primer cuello de botella que surge al usar el tiempo de ejecución de R.

En R Services, los recursos que los scripts de R pueden usar están regidos por SQL Server. Se recomienda supervisar el uso de recursos mediante DMV de SQL Server, o bien examinar los contadores de rendimiento del objeto de trabajo de Windows asociado y ajustar en consecuencia el uso de memoria del servidor. 
 
Si tiene SQL Server Enterprise Edition, puede asignar los recursos usados para ejecutar scripts de R mediante la configuración de un [grupo de recursos externos](../../advanced-analytics/r-services/how-to-create-a-resource-pool-for-r.md). 

Para obtener más información sobre cómo administrar la capacidad de script de R, vea estos artículos:

- [Configuración de SQL Server (R Services)](../../advanced-analytics/r-services/sql-server-configuration-r-services.md)
-  [Caso práctico de rendimiento (R Services)](../../advanced-analytics/r-services/performance-case-study-r-services.md)

## <a name="security"></a>Seguridad

Cada grupo de usuarios está asociado con el servicio [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] en una instancia específica y no es compatible con trabajos de R que se ejecutan en otras instancias.

Para cada cuenta de trabajo, mientras la sesión está activa, se crea una carpeta temporal para almacenar los objetos de script, los resultados intermedios y otra información que R y SQL Server usan durante la ejecución de scripts de R. Estos archivos de trabajo, ubicados en la carpeta ExtensibilityData, son de acceso restringido a los administradores y SQL Server los limpia una vez completado el script. 

Para obtener más información, vea [Security Overview](../../advanced-analytics/r-services/security-overview-sql-server-r.md) (Información general de seguridad).

### <a name="bkmk_EnforcePolicy"></a>Aplicar una directiva de contraseñas

Si su organización tiene una directiva que requiere el cambio de contraseñas de forma periódica, podría tener que forzar el servicio Launchpad para que regenere las contraseñas cifradas que Launchpad conserva para sus cuentas de trabajo.  

Para habilitar esta opción de configuración y forzar la actualización de las contraseñas, abra el panel **Propiedades** del servicio Launchpad en el Administrador de configuración de SQL Server, haga clic en **Avanzado** y cambie **Restablecer contraseña de usuarios externos** a **Sí**. Al aplicar este cambio, las contraseñas se regenerarán inmediatamente para todas las cuentas de usuario. Para usar el script de R después de este cambio, debe reiniciar el servicio Launchpad, momento en el cual leerá las contraseñas recién generadas. 

Para restablecer las contraseñas a intervalos regulares, puede establecer esta marca manualmente o usar un script.

### <a name="additional-permission-required-to-support-remote-compute-contexts"></a>Permiso adicional necesario para admitir contextos de cálculo remoto

De forma predeterminada, el grupo de cuentas de trabajo de R **no** tiene permisos de inicio de sesión en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a la que está asociado. Esto puede ser un problema si se conectan usuarios de R a SQL Server desde un cliente remoto para ejecutar scripts de R, o si un script usa ODBC para obtener datos adicionales. 

Para asegurarse de que se admiten estos escenarios, el administrador de bases de datos debe proporcionar al grupo de cuentas de trabajo de R permiso para iniciar sesión en la instancia de SQL Server donde se van a ejecutar scripts de R (permisos **Conectar a**). Esto se conoce como *autenticación implícita* y permite a SQL Server ejecutar los scripts de R con las credenciales del usuario remoto.

> [!NOTE]
> Esta limitación no se aplica si usa inicios de sesión de SQL para ejecutar scripts de R desde una estación de trabajo remota, ya que las credenciales de inicio de sesión de SQL se pasan explícitamente desde el cliente de R a la instancia de SQL Server y, después, a ODBC.


### <a name="how-to-enable-implied-authentication"></a>Cómo habilitar la autenticación implícita

1. Abra SQL Server Management Studio como administrador en la instancia donde se ejecutará código de R.

2. Ejecute el script siguiente. Asegúrese de editar el nombre del grupo de usuarios, si ha cambiado el valor predeterminado, y el nombre de equipo y de instancia.

    ```sql
    USE [master]
    GO
    
    CREATE LOGIN [computername\SQLRUserGroup] FROM WINDOWS WITH DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[language]
    GO  
    ````


  
## <a name="see-also"></a>Vea también  
 [Configuración (SQL Server R Services)](../../advanced-analytics/r-services/configuration-sql-server-r-services.md)
  

