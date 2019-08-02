---
title: Escalar la ejecución simultánea de scripts externos
description: Configure la ejecución de scripts de R y Python paralelas o simultáneas en un grupo de cuentas de usuario para escalar SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a5a0cd5ab05f7675ce011fe5205cbba3432725f4
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715864"
---
# <a name="scale-concurrent-execution-of-external-scripts-in-sql-server-machine-learning-services"></a>Escalar la ejecución simultánea de scripts externos en SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Como parte del proceso de instalación de [!INCLUDE[rsql-productnamenew-md](../../includes/rsql-productnamenew-md.md)], se crea un *grupo de cuentas de usuario* de Windows para admitir la ejecución de tareas mediante el servicio [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]. El propósito de estas cuentas de trabajo es aislar la ejecución simultánea de scripts externos por parte de distintos usuarios de SQL.

En este artículo se describe la configuración predeterminada y la capacidad de las cuentas de trabajo, y cómo cambiar la configuración predeterminada para escalar el número de ejecuciones simultáneas de scripts externos en SQL Server Machine Learning Services.

## <a name="worker-account-group"></a>Grupo de cuentas de trabajo

El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] programa de instalación de crea un grupo de cuentas de Windows para cada instancia en la que machine learning está instalado y habilitado.

- En una instancia predeterminada, el nombre del grupo es **SQLRUserGroup**. El nombre es el mismo si usa R o Python o ambos.
- En una instancia con nombre, el nombre del grupo predeterminado tiene como sufijo el nombre de instancia, por ejemplo, **SQLRUserGroupMyInstanceName**.

De forma predeterminada, el grupo de cuentas de usuario contiene 20 cuentas de usuario. En la mayoría de los casos, 20 es más adecuado para admitir tareas de aprendizaje automático, pero puede cambiar el número de cuentas. El número máximo de cuentas es 100.

- En una instancia predeterminada, las cuentas individuales se denominan de **MSSQLSERVER01** a **MSSQLSERVER20**.
- En el caso de una instancia con nombre, las cuentas individuales reciben el nombre de la instancia, por ejemplo, de **MyInstanceName01** a **MyInstanceName20**.

Si más de una instancia usa el aprendizaje automático, el equipo tendrá varios grupos de usuarios. No se puede compartir un grupo entre instancias.

> [!Note]
> En SQL Server 2019, **SQLRUserGroup** solo tiene un miembro que ahora es la cuenta de servicio de SQL Server Launchpad única en lugar de varias cuentas de trabajo.

<a name = "HowToChangeGroup"> </a>

## <a name="number-of-worker-accounts"></a>Número de cuentas de trabajo

Para modificar el número de usuarios del grupo de cuentas, debe modificar las propiedades del servicio [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] tal y como se describe a continuación.

Las contraseñas asociadas con cada cuenta de usuario se generan aleatoriamente, pero puede cambiarlas más adelante, una vez que se hayan creado las cuentas.

1. Abra el Administrador de configuración de SQL Server y seleccione **Servicios de SQL Server**.
2. Haga doble clic en el servicio SQL Server Launchpad y detenga el servicio si se está ejecutando.
3.  En la pestaña **Servicio**, asegúrese de que el modo de inicio esté establecido en Automático. No se pueden iniciar scripts externos cuando Launchpad no se está ejecutando.
4.  Haga clic en la pestaña **Avanzado** y modifique el valor de **Recuento de usuarios externos** si es necesario. Esta configuración controla el número de usuarios de SQL diferentes que pueden ejecutar sesiones de script externo simultáneamente. El valor predeterminado es 20 cuentas. El número máximo de usuarios es 100.
5. Opcionalmente, puede establecer la opción **Restablecer contraseña de usuarios externos** en _Sí_ si su organización tiene una directiva que requiere cambiar las contraseñas periódicamente. De este modo, se regeneran las contraseñas cifradas que Launchpad mantiene para las cuentas de usuario. Para obtener más información, vea [Aplicar una directiva de contraseñas](../security/sql-server-launchpad-service-account.md#bkmk_EnforcePolicy).
6.  Reinicie el servicio Launchpad.

## <a name="managing-workloads"></a>Administración de cargas de trabajo

El número de cuentas de este grupo determina el número de sesiones de script externo que pueden estar activas simultáneamente.  De forma predeterminada, se crean 20 cuentas, lo que significa que 20 usuarios diferentes pueden tener sesiones activas de R o Python al mismo tiempo. Puede aumentar el número de cuentas de trabajo si espera ejecutar más de 20 scripts simultáneos.

Cuando el mismo usuario ejecuta varios scripts externos simultáneamente, todas las sesiones ejecutadas por ese usuario usan la misma cuenta de trabajo. Por ejemplo, un solo usuario puede tener 100 scripts de R diferentes que se ejecutan simultáneamente, siempre y cuando los recursos lo permitan, pero todos los scripts se ejecutarían con una sola cuenta de trabajo.

El número de cuentas de trabajo que puede admitir y el número de sesiones simultáneas que un solo usuario puede ejecutar, solo está limitado por los recursos del servidor. Normalmente, la memoria es el primer cuello de botella que surge al usar el tiempo de ejecución de R.

Los recursos que pueden usar los scripts de Python o R se rigen por SQL Server. Se recomienda supervisar el uso de recursos mediante DMV de SQL Server, o bien examinar los contadores de rendimiento del objeto de trabajo de Windows asociado y ajustar en consecuencia el uso de memoria del servidor. Si tiene SQL Server Enterprise Edition, puede asignar los recursos usados para ejecutar scripts externos mediante la configuración de un [grupo de recursos externos](how-to-create-a-resource-pool.md).

## <a name="see-also"></a>Vea también

Para obtener más información sobre la configuración de la capacidad, consulte estos artículos:

- [Configuración de SQL Server para R Services](../../advanced-analytics/r/sql-server-configuration-r-services.md)
- [Caso práctico de rendimiento para R Services](../../advanced-analytics/r/performance-case-study-r-services.md)