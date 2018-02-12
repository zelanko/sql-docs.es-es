---
title: "Modificar el grupo de cuentas de usuario para el aprendizaje automático de SQL Server | Documentos de Microsoft"
ms.date: 11/03/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 58b79170-5731-46b5-af8c-21164d28f3b0
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: d12de2f8298e23d5396d7caf2496b293f1bf28ed
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2018
---
# <a name="modify-the-user-account-pool-for-sql-server-machine-learning"></a>Modificar el grupo de cuentas de usuario para el aprendizaje automático de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Como parte del proceso de instalación de [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)], se crea un *grupo de cuentas de usuario* de Windows para admitir la ejecución de tareas mediante el servicio [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]. El propósito de estas cuentas de trabajo es aislar la ejecución simultánea de scripts externos por usuarios diferentes de SQL.

Este artículo describe la configuración predeterminada, la seguridad y la capacidad de las cuentas de trabajo y cómo cambiar la configuración predeterminada.

**Se aplica a:** [!INCLUDE[sssql15-md](../../includes/sssql15-md.md)] [!INCLUDE[rsql-productname-md](../../includes/rsql-productname-md.md)], [!INCLUDE[sscurrent-md](../../includes/sscurrent-md.md)] [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)]

## <a name="worker-accounts-used-for-external-script-execution"></a>Cuentas de trabajo utilizadas para la ejecución de scripts externos

Crea el grupo de cuentas de Windows [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el programa de instalación para cada instancia en el equipo que el aprendizaje está instalado y habilitado.

-   En una instancia predeterminada, el nombre del grupo es **SQLRUserGroup**. El nombre es el mismo independientemente de si usa R, Python o ambos.
-   En una instancia con nombre, el nombre del grupo predeterminado tiene como sufijo el nombre de instancia, por ejemplo, **SQLRUserGroupMyInstanceName**.

De forma predeterminada, el grupo de cuentas de usuario contiene 20 cuentas de usuario. En la mayoría de los casos, resulta más adecuado para admitir tareas de aprendizaje automático 20, pero puede cambiar el número de cuentas.
-  En una instancia predeterminada, las cuentas individuales se denominan de **MSSQLSERVER01** a **MSSQLSERVER20**.
-   En el caso de una instancia con nombre, las cuentas individuales reciben el nombre de la instancia, por ejemplo, de **MyInstanceName01** a **MyInstanceName20**.

Si más de una instancia usa el aprendizaje automático, el equipo tendrá varios grupos de usuarios. Un grupo no se pueden compartir entre instancias.

### <a name = "HowToChangeGroup"></a>Cómo cambiar el número de cuentas de trabajo

Para modificar el número de usuarios del grupo de cuentas, debe modificar las propiedades del servicio [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] tal y como se describe a continuación.

Las contraseñas asociadas con cada cuenta de usuario se generan aleatoriamente, pero puede cambiarlas más adelante, una vez que se hayan creado las cuentas.

1. Abra el Administrador de configuración de SQL Server y seleccione **Servicios de SQL Server**.
2. Haga doble clic en el servicio SQL Server Launchpad y detenga el servicio si se está ejecutando.
3.  En la pestaña **Servicio**, asegúrese de que el modo de inicio esté establecido en Automático. No se pueden iniciar scripts externos cuando no se está ejecutando el Launchpad.
4.  Haga clic en la pestaña **Avanzado** y modifique el valor de **Recuento de usuarios externos** si es necesario. Este valor controla cuántos usuarios diferentes de SQL puede ejecutar scripts externos de las sesiones al mismo tiempo. El valor predeterminado es 20 cuentas.
5. Opcionalmente, puede establecer la opción **Restablecer contraseña de usuarios externos** en _Sí_ si su organización tiene una directiva que requiere cambiar las contraseñas periódicamente. De este modo, se regeneran las contraseñas cifradas que Launchpad mantiene para las cuentas de usuario. Para obtener más información, vea [Aplicar una directiva de contraseñas](#bkmk_EnforcePolicy).
6.  Reinicie el servicio Launchpad.

## <a name="managing-machine-learning-workloads"></a>Administración de cargas de trabajo de aprendizaje de máquina

El número de cuentas de este grupo determina la cantidad de sesiones de scripts externos puede estar activas simultáneamente.  De forma predeterminada, se crean 20 cuentas, lo que significa que 20 usuarios diferentes pueden tener R o Python sesiones activas al mismo tiempo. Puede aumentar el número de cuentas de trabajo, si tiene previsto ejecutar más de 20 secuencias de comandos simultáneos.

Cuando el mismo usuario ejecuta varios scripts externos de forma simultánea, todas las sesiones ejecución ese usuario usar la misma cuenta de trabajo. Por ejemplo, un usuario podría tener 100 diferentes scripts de R ejecutando al mismo tiempo, mientras que permitan los recursos, pero todos los scripts se ejecutaría con una cuenta de trabajo único.

El número de cuentas de trabajo que se pueden admitir y el número de sesiones simultáneas que se puede ejecutar cualquier usuario único, está limitado por los recursos del servidor. Normalmente, la memoria es el primer cuello de botella que surge al usar el tiempo de ejecución de R.

Los recursos que se pueden usar secuencias de comandos Python o R son gobernados por SQL Server. Se recomienda supervisar el uso de recursos mediante DMV de SQL Server, o bien examinar los contadores de rendimiento del objeto de trabajo de Windows asociado y ajustar en consecuencia el uso de memoria del servidor. Si tiene SQL Server Enterprise Edition, puede asignar los recursos que usa para ejecutar scripts externos mediante la configuración de un [grupo de recursos externo](../../advanced-analytics/r-services/how-to-create-a-resource-pool-for-r.md).

Para obtener información adicional acerca de cómo administrar máquina aprendizaje capacidad de tarea, vea estos artículos:

- [Configuración de SQL Server para R Services](../../advanced-analytics/r/sql-server-configuration-r-services.md)
-  [Caso práctico de rendimiento para R Services](../../advanced-analytics/r/performance-case-study-r-services.md)

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

Para asegurarse de que se admiten estos escenarios, el administrador de bases de datos debe proporcionar al grupo de cuentas de trabajo de R permiso para iniciar sesión en la instancia de SQL Server donde se van a ejecutar scripts de R (permisos **Conectar a**). Esto se conoce como *autenticación implícita*y permite a SQL Server ejecutar los scripts de R con las credenciales del usuario remoto.

> [!NOTE]
> Esta limitación no se aplica si usa inicios de sesión de SQL para ejecutar scripts de R desde una estación de trabajo remota, ya que las credenciales de inicio de sesión de SQL se pasan explícitamente desde el cliente de R a la instancia de SQL Server y, después, a ODBC.


### <a name="how-to-enable-implied-authentication"></a>Cómo habilitar la autenticación implícita

1. Abra SQL Server Management Studio como administrador en la instancia donde se ejecutará el código de R o Python.

2. Ejecute el script siguiente. Asegúrese de editar el nombre del grupo de usuarios, si ha cambiado el valor predeterminado, y el nombre de equipo y de instancia.

    ```sql
    USE [master]
    GO
    
    CREATE LOGIN [computername\SQLRUserGroup] FROM WINDOWS WITH DEFAULT_DATABASE=[master], DEFAULT_LANGUAGE=[language]
    GO
    ````

