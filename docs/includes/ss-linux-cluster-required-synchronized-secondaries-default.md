---
ms.openlocfilehash: 2dc81d434714e0a13912fa6f14e1194df5e5afe3
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "68215606"
---
> [!NOTE]
> Cuando crea el recurso, y posteriormente de forma periódica, el agente del recurso de Pacemaker establece automáticamente el valor de `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` en el grupo de disponibilidad según la configuración del grupo. Por ejemplo, si el grupo de disponibilidad tiene tres réplicas sincrónicas, el agente establecerá `REQUIRED_SYNCHRONIZED_SECONDARIES_TO_COMMIT` en `1`. Para detalles y opciones de configuración adicional, consulte el artículo sobre [alta disponibilidad y protección de datos para configuraciones de grupos de disponibilidad](../linux/sql-server-linux-availability-group-ha.md). 