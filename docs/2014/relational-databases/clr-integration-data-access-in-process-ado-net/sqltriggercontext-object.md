---
title: Objeto SqlTriggerContext | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- SqlTriggerContext object
- triggers [CLR integration]
- context [CLR integration]
ms.assetid: 472a2d0b-64ae-4877-8f11-a5620aa698b7
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: df384324ba16aac03a4c889cf4f3959c23374510
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62874691"
---
# <a name="sqltriggercontext-object"></a>Objeto SqlTriggerContext
  La clase `SqlTriggerContext` proporciona información de contexto acerca del desencadenador. Esto incluye el tipo de acción que ha provocado la activación del desencadenador, las columnas que se modificaron en una operación UPDATE y, en el caso de un desencadenador de lenguaje de definición de datos (DDL), una estructura de XML `EventData` que describe la operación de desencadenamiento. Para obtener más información y ejemplos de cómo usar el `SqlTriggerContext` de clases, vea [desencadenadores CLR](../../database-engine/dev-guide/clr-triggers.md).  
  
 Para obtener más información, consulte el `Microsoft.SqlServer.Server.SqlTriggerContext` documentación de referencia en la documentación del SDK de .NET Framework de la clase.  
  
## <a name="see-also"></a>Vea también  
 [Desencadenadores CLR](../../database-engine/dev-guide/clr-triggers.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](/sql/t-sql/functions/eventdata-transact-sql)  
  
  
