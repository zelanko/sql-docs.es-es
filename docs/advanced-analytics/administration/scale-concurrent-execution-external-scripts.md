---
title: Escalar la ejecución simultánea de scripts externos
description: Configure la ejecución de scripts de R y Python paralelas o simultáneas en un grupo de cuentas de usuario para escalar SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 09/25/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: =sql-server-2016||=sql-server-2017||=sqlallproducts-allversions
ms.openlocfilehash: 262810be3ad1fd246c6f60383e28d456c6b79e08
ms.sourcegitcommit: fd3e81c55745da5497858abccf8e1f26e3a7ea7d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2019
ms.locfileid: "71714339"
---
# <a name="scale-concurrent-execution-of-external-scripts-in-sql-server-machine-learning-services"></a>Escalar la ejecución simultánea de scripts externos en SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Obtenga información sobre las cuentas de trabajo de SQL Server Machine Learning Services y cómo cambiar la configuración predeterminada para escalar el número de ejecuciones simultáneas de scripts externos.

Como parte del proceso de instalación de Machine Learning Services, se crea un nuevo *grupo de cuentas de usuario* de Windows para admitir la ejecución de tareas por parte del servicio [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]. El propósito de estas cuentas de trabajo es aislar la ejecución simultánea de scripts externos por diferentes SQL Server usuarios.

> [!Note]
> En SQL Server 2019, **SQLRUserGroup** solo tiene un miembro que ahora es la cuenta de servicio de SQL Server Launchpad única en lugar de varias cuentas de trabajo. En este artículo se describen las cuentas de trabajo para SQL Server 2016 y 2017.

## <a name="worker-account-group"></a>Grupo de cuentas de trabajo

El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] programa de instalación de crea un grupo de cuentas de Windows para cada instancia en la que machine learning está instalado y habilitado.

- En una instancia predeterminada, el nombre del grupo es **SQLRUserGroup**. El nombre es el mismo si usa Python o R o ambos.
- En una instancia con nombre, el nombre del grupo predeterminado tiene como sufijo el nombre de instancia, por ejemplo, **SQLRUserGroupMyInstanceName**.

De forma predeterminada, el grupo de cuentas de usuario contiene 20 cuentas de usuario. En la mayoría de los casos, 20 es más adecuado para admitir tareas de aprendizaje automático, pero puede cambiar el número de cuentas. El número máximo de cuentas es 100.

- En una instancia predeterminada, las cuentas individuales se denominan de **MSSQLSERVER01** a **MSSQLSERVER20**.
- En el caso de una instancia con nombre, las cuentas individuales reciben el nombre de la instancia, por ejemplo, de **MyInstanceName01** a **MyInstanceName20**.

Si más de una instancia usa el aprendizaje automático, el equipo tendrá varios grupos de usuarios. No se puede compartir un grupo entre instancias.

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

El número de cuentas de este grupo determina el número de sesiones de script externo que pueden estar activas simultáneamente.  De forma predeterminada, se crean 20 cuentas, lo que significa que 20 usuarios diferentes pueden tener sesiones activas de Python o R al mismo tiempo. Puede aumentar el número de cuentas de trabajo si espera ejecutar más de 20 scripts simultáneos.

Cuando el mismo usuario ejecuta varios scripts externos simultáneamente, todas las sesiones ejecutadas por ese usuario usan la misma cuenta de trabajo. Por ejemplo, un solo usuario puede tener 100 scripts de Python o R diferentes que se ejecutan simultáneamente, siempre y cuando los recursos lo permitan, pero todos los scripts se ejecutarían con una sola cuenta de trabajo.

El número de cuentas de trabajo que puede admitir y el número de sesiones simultáneas que un solo usuario puede ejecutar, solo está limitado por los recursos del servidor. Normalmente, la memoria es el primer cuello de botella que encontrará al usar el tiempo de ejecución de Python o R.

Los recursos que pueden usar los scripts de Python o R se rigen por SQL Server. Se recomienda supervisar el uso de recursos mediante DMV de SQL Server, o bien examinar los contadores de rendimiento del objeto de trabajo de Windows asociado y ajustar en consecuencia el uso de memoria del servidor. Si tiene SQL Server Enterprise Edition, puede asignar los recursos usados para ejecutar scripts externos mediante la configuración de un [grupo de recursos externos](how-to-create-a-resource-pool.md).

## <a name="next-steps"></a>Pasos siguientes

- [Supervisión de la ejecución de scripts de Python y R mediante informes personalizados en SQL Server Management Studio](../../advanced-analytics/administration/monitor-sql-server-machine-learning-services-using-custom-reports-management-studio.md)
- [Supervisar SQL Server Machine Learning Services mediante vistas de administración dinámica (DMV)](../../advanced-analytics/administration/monitor-sql-server-machine-learning-services-using-dynamic-management-views.md)