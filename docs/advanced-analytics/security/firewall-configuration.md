---
title: Configuración de firewall
description: Configuración del firewall para las conexiones salientes desde SQL Server Machine Learning Services.
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/17/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: c55f68a1134fee6477c52182ad66b8705e363296
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715595"
---
# <a name="firewall-configuration-for-sql-server-machine-learning-services"></a>Configuración de firewall para SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

En este artículo se enumeran las consideraciones sobre la configuración del firewall que el administrador o el arquitecto deben tener en cuenta al usar los servicios de aprendizaje automático.

## <a name="default-firewall-rules"></a>Reglas de firewall predeterminadas

De forma predeterminada, el programa de instalación de SQL Server deshabilita las conexiones salientes mediante la creación de reglas de firewall.

En SQL Server 2016 y 2017, estas reglas se basaban en cuentas de usuario locales, en las que el programa de instalación creó una regla de salida para **SQLRUserGroup** que denegaba a sus miembros el acceso a la red (cada cuenta profesional aparecía como un principio local sujeto a la regla). Para obtener más información sobre SQLRUserGroup, vea [Información general sobre seguridad para el marco de extensibilidad en SQL Server Machine Learning Services](../../advanced-analytics/concepts/security.md#sqlrusergroup).

En SQL Server 2019, como parte del cambio a contenedores de AppContainer, hay nuevas reglas de firewall que se basan en los SID de AppContainer: una para cada uno de los 20 contenedores AppContainer creados por el programa de instalación de SQL Server. Las convenciones de nomenclatura para el nombre de la regla de firewall se corresponden a **Block network access for AppContainer-00 in SQL Server instance MSSQLSERVER** (Bloquear el acceso a la red para AppContainer-00 en la instancia MSSQLSERVER de SQL Server), en el que 00 es el número del contenedor AppContainer (00-20 de forma predeterminada) y MSSQLSERVER es el nombre de la instancia de SQL Server.

> [!Note]
> Si se requieren llamadas de red, puede deshabilitar las reglas de salida en Firewall de Windows.

## <a name="restrict-network-access"></a>Restricción del acceso a la red

En una instalación predeterminada, se utiliza una regla del Firewall de Windows para bloquear el acceso a toda la red saliente desde procesos de runtime externos. Hay que crear reglas de firewall para impedir que los procesos de runtime externos descarguen paquetes o realicen otras llamadas de red que pudieran ser malintencionadas.

Si usa otro programa de firewall, también puede crear reglas para bloquear la conexión de red saliente para el runtime externo estableciendo reglas para las cuentas de usuario locales o para el grupo representado por el grupo de cuentas de usuario.

Se recomienda encarecidamente que active Firewall de Windows (u otro firewall de su elección) para impedir el acceso a la red sin restricciones mediante el runtime de R o Python.

## <a name="next-steps"></a>Pasos siguientes

[Configurar Firewall de Windows para conexiones enlazadas](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)