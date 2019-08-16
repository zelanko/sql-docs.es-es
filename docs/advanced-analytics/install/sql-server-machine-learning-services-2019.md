---
title: Cambios de aislamiento para Windows
description: En este artículo se describen los cambios en el mecanismo de aislamiento en Machine Learning Services en SQL Server 2019 en Windows. Estos cambios afectan a SQLRUserGroup, las reglas de firewall, el permiso de archivo y la autenticación implícita.
ms.prod: sql
ms.technology: machine-learning
ms.date: 08/15/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 4fae460e78682263c604d8e1e86ca40b7b62df97
ms.sourcegitcommit: 187f6d327421e64f1802a3085f88bbdb0c79b707
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/16/2019
ms.locfileid: "69531044"
---
# <a name="sql-server-2019-on-windows-isolation-changes-for-machine-learning-services"></a>SQL Server 2019 en Windows: Cambios de aislamiento para Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En este artículo se describen los cambios en el mecanismo de aislamiento en Machine Learning Services en SQL Server 2019 en Windows. Estos cambios afectan a **SQLRUserGroup**, las reglas de firewall, el permiso de archivo y la autenticación implícita.

Para obtener más información, consulte Instalación [de SQL Server Machine Learning Services en Windows](sql-machine-learning-services-windows-install.md).

## <a name="changes-to-isolation-mechanism"></a>Cambios en el mecanismo de aislamiento

En Windows, el programa de instalación de SQL Server 2019 cambia el mecanismo de aislamiento para los procesos externos. Este cambio reemplaza las cuentas de trabajo local por [AppContainers](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation), una tecnología de aislamiento para las aplicaciones cliente que se ejecutan en Windows. 

No hay elementos de acción específicos para el administrador como resultado de la modificación. En un servidor nuevo o actualizado, todos los scripts externos y el código que se ejecutan desde [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) siguen automáticamente el nuevo modelo de aislamiento. 

En Resumen, las principales diferencias en esta versión son:

+ Las cuentas de usuario local en **grupo de usuarios restringidos de SQL (SQLRUserGroup)** ya no se crean ni se usan para ejecutar procesos externos. AppContainers reemplácelas.
+ La pertenencia a **SQLRUserGroup** ha cambiado. En lugar de varias cuentas de usuario locales, la pertenencia consta únicamente de la cuenta de servicio de SQL Server Launchpad. Los procesos de R y Python ahora se ejecutan con la identidad de servicio Launchpad, aislada a través de AppContainers.

Aunque el modelo de aislamiento ha cambiado, el Asistente para la instalación y los parámetros de la línea de comandos siguen siendo los mismos en SQL Server 2019. Para obtener ayuda con la instalación, consulte [instalar SQL Server Machine Learning Services](sql-machine-learning-services-windows-install.md).

## <a name="about-appcontainer-isolation"></a>Acerca del aislamiento de AppContainer

En versiones anteriores, **SQLRUserGroup** contenía un grupo de cuentas de usuario de Windows locales (MSSQLSERVER00-MSSQLSERVER20) que se usaba para aislar y ejecutar procesos externos. Cuando se necesitaba un proceso externo, SQL Server Launchpad servicio tomaría una cuenta disponible y la usaría para ejecutar un proceso. 

En SQL Server 2019, el programa de instalación ya no crea cuentas de trabajo local. En su lugar, el aislamiento se logra a través de [AppContainers](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation). En tiempo de ejecución, cuando se detecta código o script incrustado en un procedimiento almacenado o una consulta, SQL Server llama a Launchpad con una solicitud de un iniciador específico de la extensión. Launchpad invoca el entorno en tiempo de ejecución adecuado en un proceso bajo su identidad y crea una instancia de un AppContainer para que lo contenga. Este cambio es beneficioso porque ya no se requiere la administración de cuentas y contraseñas locales. Además, en las instalaciones en las que están prohibidas las cuentas de usuario locales, la eliminación de la dependencia de la cuenta de usuario local significa que ahora puede usar esta característica.

Tal y como lo implementa SQL Server, AppContainers son un mecanismo interno. Aunque no verá evidencia física de AppContainers en el monitor de procesos, puede encontrarlos en reglas de Firewall de salida creadas por el programa de instalación para evitar que los procesos realicen llamadas de red.

## <a name="firewall-rules-created-by-setup"></a>Reglas de Firewall creadas por el programa de instalación

De forma predeterminada, SQL Server deshabilita las conexiones salientes mediante la creación de reglas de Firewall. En el pasado, estas reglas se basaban en las cuentas de usuario locales, donde el programa de instalación creaba una regla de salida para **SQLRUserGroup** que denegó el acceso a la red a sus miembros (cada cuenta de trabajo aparecía como un principio local sujeto a rule_). 

Como parte de la migración a AppContainers, hay nuevas reglas de Firewall basadas en los SID de AppContainer: una para cada una de las 20 AppContainers creadas por SQL Server el programa de instalación. Las convenciones de nomenclatura para el nombre de la regla de firewall son **bloquear el acceso a la red para appcontainer-00 en SQL Server instancia MSSQLSERVER**, donde 00 es el número de appcontainer (00-20 de forma predeterminada) y MSSQLSERVER es el nombre de la instancia de SQL Server. 

> [!Note]
> Si se requieren llamadas de red, puede deshabilitar las reglas de salida en el Firewall de Windows.

## <a name="program-file-permissions"></a>Permisos de archivo de programa

Al igual que en las versiones anteriores, el **SQLRUserGroup** continúa proporcionando permisos de lectura y ejecución en los archivos ejecutables de los directorios de SQL Server **Binn**, **R_SERVICES**y **PYTHON_SERVICES** . En esta versión, el único miembro de **SQLRUserGroup** es la cuenta de servicio SQL Server Launchpad.  Cuando el servicio Launchpad inicia un entorno de ejecución de R o Python, el proceso se ejecuta como servicio LaunchPad.

## <a name="implied-authentication"></a>Autenticación implícita

Como antes, todavía se requiere configuración adicional para la *autenticación implícita* en los casos en los que el script o el código tienen que conectarse de nuevo a SQL Server con autenticación de confianza para recuperar datos o recursos. La configuración adicional implica la creación de un inicio de sesión de base de datos para **SQLRUserGroup**, cuyo único miembro es ahora la única cuenta de servicio de SQL Server Launchpad en lugar de varias cuentas de trabajo. Para obtener más información sobre esta tarea, vea [Agregar SQLRUserGroup como un usuario de base de datos](../security/create-a-login-for-sqlrusergroup.md).


## <a name="symbolic-link-created-by-setup"></a>Vínculo simbólico creado por el programa de instalación

Se crea un vínculo simbólico al **R_SERVICES** predeterminado actual y **PYTHON_SERVICES** como parte de SQL Server configuración. Si no desea crear este vínculo, una alternativa es conceder el permiso de lectura "todos los paquetes de aplicación" a la jerarquía que conduce a la carpeta.


## <a name="see-also"></a>Vea también

+ [Instalación de Machine Learning Services de SQL Server en Windows](sql-machine-learning-services-windows-install.md)
+ [Instalación de Machine Learning Services de SQL Server en Linux](../../linux/sql-server-linux-setup-machine-learning.md)
