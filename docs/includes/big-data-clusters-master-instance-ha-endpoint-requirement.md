---
ms.openlocfilehash: 497a564a10a3d35b33f47222fce8f89fe36bd15e
ms.sourcegitcommit: 830149bdd6419b2299aec3f60d59e80ce4f3eb80
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/04/2019
ms.locfileid: "73530918"
---
Ciertas operaciones, incluida la configuración del servidor (nivel de instancia) o la adición manual de una base de datos a un grupo de disponibilidad, requieren una conexión a la instancia de SQL Server. Las operaciones como `sp_configure`, `RESTORE DATABASE` o cualquier comando DDL en una base de datos que pertenezca a un grupo de disponibilidad requieren una conexión a la instancia de SQL Server. De forma predeterminada, un clúster de macrodatos no incluye un punto de conexión que permita una conexión a la instancia. Debe exponer este punto de conexión manualmente.

Para obtener instrucciones, consulte [Conexión a las bases de datos de la réplica principal](../big-data-cluster/deployment-high-availability.md#instance-connect).