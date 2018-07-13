---
title: MSSQLSERVER_845 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 845 (Database Engine error)
ms.assetid: 8fff6ad4-234c-44be-b123-e25d5e1cd63e
caps.latest.revision: 17
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 860fce7c9e8794fce89c76c7f6abb51a1a6773d2
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37421014"
---
# <a name="mssqlserver845"></a>MSSQLSERVER_845
    
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
  
  
