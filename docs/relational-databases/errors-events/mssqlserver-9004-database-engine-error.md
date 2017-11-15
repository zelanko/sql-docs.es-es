---
title: MSSQLSERVER_9004 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 9004 (Database Engine error)
ms.assetid: b528bb49-340c-4a81-9c8d-cefce6562f16
caps.latest.revision: "16"
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.openlocfilehash: 8c794316e9995e4a61fd0af55318c411dbcbda61
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="mssqlserver9004"></a>MSSQLSERVER_9004
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|9004|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|LOG_CORRUPT|  
|Texto del mensaje|Se produjo un error mientras se procesaba el registro para la base de datos '%.*ls'.  If possible, restore from backup. Si no dispone de una copia de seguridad, puede ser necesario generar de nuevo el registro.|  
  
## <a name="explanation"></a>Explicación  
Se encontró un error al procesar el registro durante la operación de reversión, recuperación o replicación. Esto puede indicar un error detectado por el sistema operativo o un error de coherencia interno detectado por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="user-action"></a>Acción del usuario  
Este error se corregirá con una de las siguientes acciones:  
  
-   Restaure desde una copia de seguridad  
  
-   Vuelva a generar el registro  
  
Además, consulte los registros de eventos y errores del sistema para identificar posibles causas del problema en el sistema.  
  
