---
title: MSSQLSERVER_845 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 845 (Database Engine error)
ms.assetid: 8fff6ad4-234c-44be-b123-e25d5e1cd63e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9d98be02727582d4f9201ec7f47c3cdb8db5a56b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62761924"
---
# <a name="mssqlserver845"></a>MSSQLSERVER_845
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|845|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|BUFLATCH_TIMEOUT|  
|Texto del mensaje|Tiempo de espera agotado para el tipo de bloqueo temporal del búfer %d de la página %S_PGID, id. de base de datos %d.|  
  
## <a name="explanation"></a>Explicación  
Un proceso estaba a la espera de adquirir un bloqueo temporal, pero el proceso ha esperado hasta que transcurrió el límite de tiempo sin adquirirlo. Esto puede ocurrir si una operación de E/S tarda demasiado en completarse, normalmente debido a otras tareas que bloquean procesos del sistema. En algunos casos, este error puede ser el resultado de un error de hardware.  
  
## <a name="user-action"></a>Acción del usuario  
Las siguientes tareas pueden impedir este error:  
  
-   Reduzca la carga de trabajo.  
  
-   Compruebe si hay errores de E/S asociados en el registro de errores o en el registro de eventos. Normalmente, los errores de E/S se deben a un funcionamiento incorrecto del disco.  
  
-   Compruebe el registro de errores para ver si hay tareas que no rinden y otros errores críticos.  
  
-   Si se producen frecuentemente errores críticos, como aserciones, solucione estos problemas.  
  
Si el error persiste, póngase en contacto con el servicio de Soporte técnico y Atención al cliente de Microsoft.  
  
