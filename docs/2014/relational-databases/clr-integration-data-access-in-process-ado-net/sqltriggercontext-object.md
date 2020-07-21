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
ms.openlocfilehash: f7eae3d290a70bedee0ed9badf9e6d0503caa2bc
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84955015"
---
# <a name="sqltriggercontext-object"></a>Objeto SqlTriggerContext
  La clase `SqlTriggerContext` proporciona información de contexto acerca del desencadenador. Esto incluye el tipo de acción que ha provocado la activación del desencadenador, las columnas que se modificaron en una operación UPDATE y, en el caso de un desencadenador de lenguaje de definición de datos (DDL), una estructura de XML `EventData` que describe la operación de desencadenamiento. Para obtener más información y ejemplos de cómo usar la `SqlTriggerContext` clase, vea [desencadenadores CLR](../../database-engine/dev-guide/clr-triggers.md).  
  
 Para obtener más información, vea la `Microsoft.SqlServer.Server.SqlTriggerContext` documentación de referencia de la clase en la documentación del SDK de .NET Framework.  
  
## <a name="see-also"></a>Consulte también  
 [Desencadenadores CLR](../../database-engine/dev-guide/clr-triggers.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](/sql/t-sql/functions/eventdata-transact-sql)  
  
  
