---
title: MSSQLSERVER_21899 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 21899 (Database Engine error)
ms.assetid: 32b87a7c-5380-4638-b147-dd78618f6625
caps.latest.revision: 6
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 61fb6244439bff48e857b9766b2b311dfaf6a9fd
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver21899"></a>MSSQLSERVER_21899
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|21899|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SQLErrorNum21899|  
|Texto del mensaje|La consulta en el publicador redireccionado '%s' para determinar si hay entradas de sysserver para los suscriptores del publicador original '%s' no se ha realizado por el error '%d', mensaje de error '%s.|  
  
## <a name="explanation"></a>Explicación  
**sp_validate_redirected_publisher** consulta a las tablas de metadatos de suscripción de la base de datos del publicador en el servidor remoto para determinar sus suscriptores asociados. Se devuelve el error 21899 si no se puede realizar esta consulta. La consulta de validación requiere acceso a la base de datos publicada en el publicador redirigido. Si el inicio de sesión especificado cuando se llama a **sp_adddistpublisher** para el publicador original no está autorizado a acceder a la base de datos publicada en el publicador redirigido, se devuelve el error 21899.  
  
## <a name="user-action"></a>Acción del usuario  
Revise el mensaje de error citado para determinar la causa del error y llevar a cabo una acción correctora adecuada  
  
