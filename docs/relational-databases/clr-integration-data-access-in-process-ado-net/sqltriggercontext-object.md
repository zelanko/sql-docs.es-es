---
title: Objeto SqlTriggerContext | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SqlTriggerContext object
- triggers [CLR integration]
- context [CLR integration]
ms.assetid: 472a2d0b-64ae-4877-8f11-a5620aa698b7
caps.latest.revision: 18
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: aa0a8c6de586e35ac2ee533c90f87825525659de
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqltriggercontext-object"></a>Objeto SqlTriggerContext
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La clase **SqlTriggerContext** proporciona información de contexto acerca del desencadenador. Esto incluye el tipo de acción que ha provocado la activación del desencadenador, las columnas que se modificaron en una operación UPDATE y, en el caso de un desencadenador de lenguaje de definición de datos (DDL), una estructura de XML **EventData** que describe la operación de desencadenamiento. Para obtener más información y ejemplos de cómo usar el **SqlTriggerContext** de clases, consulte [desencadenadores CLR](http://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c).  
  
 Para obtener más información, vea la documentación de referencia de la clase **Microsoft.SqlServer.Server.SqlTriggerContext** en la documentación del SDK de .NET Framework.  
  
## <a name="see-also"></a>Vea también  
 [Desencadenadores CLR](http://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
