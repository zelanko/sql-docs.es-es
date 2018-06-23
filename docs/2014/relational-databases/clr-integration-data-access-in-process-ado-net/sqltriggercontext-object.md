---
title: Objeto SqlTriggerContext | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SqlTriggerContext object
- triggers [CLR integration]
- context [CLR integration]
ms.assetid: 472a2d0b-64ae-4877-8f11-a5620aa698b7
caps.latest.revision: 18
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: dbdaefa1e3c5e1c5a53cd6179f4b96320434dbdf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36104913"
---
# <a name="sqltriggercontext-object"></a>Objeto SqlTriggerContext
  La clase `SqlTriggerContext` proporciona información de contexto acerca del desencadenador. Esto incluye el tipo de acción que ha provocado la activación del desencadenador, las columnas que se modificaron en una operación UPDATE y, en el caso de un desencadenador de lenguaje de definición de datos (DDL), una estructura de XML `EventData` que describe la operación de desencadenamiento. Para obtener más información y ejemplos de cómo usar el `SqlTriggerContext` de clases, consulte [desencadenadores CLR](../../database-engine/dev-guide/clr-triggers.md).  
  
 Para obtener más información, consulte el `Microsoft.SqlServer.Server.SqlTriggerContext` documentación de referencia en la documentación del SDK de .NET Framework de la clase.  
  
## <a name="see-also"></a>Vea también  
 [Desencadenadores CLR](../../database-engine/dev-guide/clr-triggers.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](/sql/t-sql/functions/eventdata-transact-sql)  
  
  
