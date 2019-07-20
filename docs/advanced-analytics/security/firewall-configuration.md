---
title: Configuración del firewall
description: Configuración del firewall para las conexiones salientes desde SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 58a10c36eff06cd4e36f3e326407564b2657fec1
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345599"
---
# <a name="firewall-configuration-for-sql-server-machine-learning-services"></a>Configuración del firewall para SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

En este artículo se enumeran las consideraciones sobre la configuración del firewall que el administrador o el arquitecto deben tener en cuenta al usar los servicios de machine learning.

## <a name="default-firewall-rules"></a>Reglas predeterminadas de Firewall

De forma predeterminada, el programa de instalación de SQL Server deshabilita las conexiones salientes mediante la creación de reglas de Firewall.

En SQL Server 2016 y 2017, estas reglas se basan en las cuentas de usuario locales, donde el programa de instalación creó una regla de salida para **SQLRUserGroup** que denegó el acceso de red a sus miembros (cada cuenta de trabajo aparecía como un principio local sujeto a la regla). Para obtener más información sobre SQLRUserGroup, vea [información general sobre seguridad para el marco de extensibilidad en SQL Server Machine Learning Services](../../advanced-analytics/concepts/security.md#sqlrusergroup).

En SQL Server 2019, como parte del cambio a AppContainers, hay nuevas reglas de Firewall basadas en los SID de AppContainer: una para cada una de las 20 AppContainers creadas por SQL Server el programa de instalación. Las convenciones de nomenclatura para el nombre de la regla de firewall son **bloquear el acceso a la red para appcontainer-00 en SQL Server instancia MSSQLSERVER**, donde 00 es el número de appcontainer (00-20 de forma predeterminada) y MSSQLSERVER es el nombre de la instancia de SQL Server.

> [!Note]
> Si se requieren llamadas de red, puede deshabilitar las reglas de salida en el Firewall de Windows.

## <a name="restrict-network-access"></a>Restringir el acceso a la red

En una instalación predeterminada, se usa una regla de Firewall de Windows para bloquear todo el acceso de red saliente desde procesos en tiempo de ejecución externos. Se deben crear reglas de Firewall para evitar que los procesos de tiempo de ejecución externos descarguen paquetes o realicen otras llamadas de red que podrían ser malintencionadas.

Si usa otro programa de firewall, también puede crear reglas para bloquear la conexión de red saliente para los tiempos de ejecución externos, estableciendo reglas para las cuentas de usuario locales o para el grupo representado por el grupo de cuentas de usuario.

Se recomienda encarecidamente activar el Firewall de Windows (u otro Firewall de su elección) para evitar el acceso a la red sin restricciones mediante los tiempos de ejecución de R o Python.

## <a name="next-steps"></a>Pasos siguientes

[Configurar el Firewall de Windows para conexiones enlazadas](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)