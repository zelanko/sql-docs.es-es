---
title: 'Diferencias en SQL Server 2019: SQL Server Machine Learning Services'
description: Obtenga información sobre cuáles son las novedades para R y Python de SQL Server machine learning las extensiones en la versión preliminar de SQL Server 2019.
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/22/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 43d427129cae773fc17a0d73f57a26144b7cd09f
ms.sourcegitcommit: 944af0f6b31bf07c861ddd4d7960eb7f018be06e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/31/2019
ms.locfileid: "66454518"
---
# <a name="differences-in-sql-server-machine-learning-services-installation-in-sql-server-2019"></a>Diferencias en la instalación de SQL Server Machine Learning Services en SQL Server 2019  
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En Windows, el programa de instalación de SQL Server de 2019 cambia el mecanismo de aislamiento de procesos externos. Este cambio reemplaza las cuentas de trabajo local con [AppContainers](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation), una tecnología de aislamiento para las aplicaciones cliente que se ejecutan en Windows. 

No hay ningún elemento de acción específica para el administrador como resultado de la modificación. En un servidor nuevo o actualizado, todos los scripts externos y el código ejecutado desde [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) siga automáticamente el nuevo modelo de aislamiento. 

En resumen, las principales diferencias en esta versión son:

+ Las cuentas de usuario local con **grupo restringido de usuarios de SQL (SQLRUserGroup)** ya no se crean o se usa para ejecutar los procesos externos. AppContainers reemplazarlos.
+ **SQLRUserGroup** pertenencia ha cambiado. En lugar de varias cuentas de usuario local, pertenencia consta de sólo la cuenta del servicio Launchpad de SQL Server. Los procesos de R y Python ahora se ejecutan bajo la identidad del servicio Launchpad aislada a través de AppContainers.

Aunque ha cambiado el modelo de aislamiento, los parámetros de línea de comandos y el Asistente para instalación son iguales en SQL Server 2019. Para obtener ayuda con la instalación, consulte [instalar SQL Server Machine Learning Services](sql-machine-learning-services-windows-install.md).

## <a name="about-appcontainer-isolation"></a>Acerca del aislamiento de AppContainer

En versiones anteriores, **SQLRUserGroup** contenidos de un grupo locales Windows de cuentas de usuario (MSSQLSERVER00-MSSQLSERVER20) utilizado para aislar y ejecutar procesos externos. Cuando se necesitaba un proceso externo, servicio Launchpad de SQL Server podría tener una cuenta disponible y utilizarlo para ejecutar un proceso. 

En SQL Server 2019, el programa de instalación ya no crea cuentas de trabajo local. En su lugar, se logra el aislamiento a través de [AppContainers](https://docs.microsoft.com/windows/desktop/secauthz/appcontainer-isolation). En tiempo de ejecución, cuando se detecta código o script incrustado en un procedimiento almacenado o una consulta, SQL Server llama a Launchpad con una solicitud para un iniciador específica de la extensión. LaunchPad invoca el entorno adecuado en tiempo de ejecución en un proceso bajo su identidad y crea una instancia de un AppContainer que lo contiene. Este cambio es beneficiosa porque ya no es necesaria la administración local de cuenta y la contraseña. Además, en las instalaciones donde las cuentas de usuario local están prohibidas, eliminación de la dependencia de la cuenta de usuario local significa que ahora puede usar esta característica.

Como se implementa mediante SQL Server, AppContainers son un mecanismo interno. Aunque no verá las evidencias físicas de AppContainers en el Monitor de proceso, se puede encontrar en las reglas de firewall de salida creadas por el programa de instalación para evitar que los procesos de realizar llamadas de red.

## <a name="firewall-rules-created-by-setup"></a>Reglas de firewall creadas por el programa de instalación

De forma predeterminada, SQL Server deshabilita las conexiones salientes mediante la creación de reglas de firewall. En el pasado, estas reglas se basan en cuentas de usuario local, donde el programa de instalación crea una regla de salida para **SQLRUserGroup** que deniega el acceso de red a sus miembros (se enumera cada cuenta de trabajo como una entidad de seguridad local sujetos a la rule_. 

Como parte de la migración a AppContainers, hay nuevas reglas de firewall basadas en AppContainer SIDs: uno para cada uno de los 20 AppContainers creado por el programa de instalación de SQL Server. Convenciones de nomenclatura para el nombre de regla de firewall son **bloquear el acceso de red para AppContainer 00 en la instancia de SQL Server MSSQLSERVER**, donde 00 es el número de AppContainer (00-20 de forma predeterminada) y MSSQLSERVER es el nombre de la consulta SQL Instancia del servidor. 

> [!Note]
> Si se requieren las llamadas de red, puede deshabilitar las reglas de salida en el Firewall de Windows.

## <a name="program-file-permissions"></a>Permisos de archivos de programa

Al igual que con versiones anteriores, el **SQLRUserGroup** continúa proporcionar la lectura y permisos de ejecución en los archivos ejecutables de SQL Server **Binn**, **R_SERVICES**y  **PYTHON_SERVICES** directorios. En esta versión, el único miembro de **SQLRUserGroup** es la cuenta del servicio Launchpad de SQL Server.  Cuando el servicio Launchpad inicia un entorno de ejecución de R o Python, el proceso se ejecuta como servicio LaunchPad.

## <a name="implied-authentication"></a>Autenticación implícita

Como antes, sigue siendo necesaria para una configuración adicional *autenticación implícita* en casos donde tiene un script o código para conectarse a SQL Server mediante autenticación de confianza para recuperar datos o recursos. La configuración adicional implica la creación de un inicio de sesión de base de datos para **SQLRUserGroup**, cuyo único miembro ahora es la única cuenta de servicio Launchpad de SQL Server en lugar de varias cuentas de trabajo. Para obtener más información acerca de esta tarea, vea [agregar SQLRUserGroup como un usuario de base de datos](../security/create-a-login-for-sqlrusergroup.md).


## <a name="symbolic-link-created-by-setup"></a>Vínculo simbólico creado por el programa de instalación

Se crea un vínculo simbólico para el valor predeterminado actual **R_SERVICES** y **PYTHON_SERVICES** como parte del programa de instalación de SQL Server. Si no desea crear este vínculo, una alternativa es conceder el permiso de lectura 'todos los paquetes de aplicación' a la jerarquía que hicieron nacer a la carpeta.


## <a name="see-also"></a>Vea también

+ [Instalar SQL Server Machine Learning Services en Windows](sql-machine-learning-services-windows-install.md)

+ [Instalar SQL Server 2019 Machine Learning Services en Linux](../../linux/sql-server-linux-setup-machine-learning.md)
