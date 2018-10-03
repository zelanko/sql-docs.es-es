---
title: MSSQLSERVER_844 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 844 (Database Engine error)
ms.assetid: 2060c886-1226-4066-bc0c-de90a1cfb82b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2fd81f5892f524dbff63e8d2a74bf8adf50bca60
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47782176"
---
# <a name="mssqlserver844"></a>MSSQLSERVER_844
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|844|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|BUFLATCH_TIMEOUT_CONTINUE|  
|Texto del mensaje|Tiempo de espera agotado mientras se esperaba el bloqueo temporal del búfer -- tipo %d, bp %p, página %d:%d, stat %#x, id. de base de datos: %d, id. de unidad de asignación: %I64d%ls, tarea 0x%p : %d, tiempo de espera %d, marcas 0x%I64x, tarea propietaria 0x%p.  Esperando.|  
  
## <a name="explanation"></a>Explicación  
Un proceso está esperando para adquirir un bloqueo temporal. Este problema puede estar causado por una operación de E/S que está tardando mucho en llevarse a cabo. Normalmente, este tipo de error es el resultado de que otras tareas estén bloqueando los procesos del sistema. En algunos casos, este error puede ser el resultado de un error de hardware.  
  
## <a name="user-action"></a>Acción del usuario  
Para evitar que ocurra este error, intente lo siguiente:  
  
-   Reduzca la carga de trabajo.  
  
-   Busque errores de E/S asociados en el registro de errores o el registro de eventos. Normalmente, los errores de E/S indican un funcionamiento incorrecto del disco.  
  
-   Compruebe el registro de errores para ver si hay tareas que no rinden y otros errores críticos.  
  
-   Si se producen frecuentemente errores críticos, como aserciones, solucione estos problemas.  
  
Si el error persiste, póngase en contacto con el servicio de Soporte técnico y Atención al cliente de Microsoft.  
  
