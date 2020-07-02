---
title: Objeto SqlTriggerContext | Microsoft Docs
description: En SQL Server la integración CLR, la clase SqlTriggerContext proporciona información de contexto para un desencadenador que incluye el tipo de acción y las columnas modificadas en la operación.
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
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
ms.openlocfilehash: 4634a0c95e64516b6364fbfd68edeb9cd6156511
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85765411"
---
# <a name="sqltriggercontext-object"></a>Objeto SqlTriggerContext
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  La clase **SqlTriggerContext** proporciona información de contexto acerca del desencadenador. Esto incluye el tipo de acción que ha provocado la activación del desencadenador, las columnas que se modificaron en una operación UPDATE y, en el caso de un desencadenador de lenguaje de definición de datos (DDL), una estructura de XML **EventData** que describe la operación de desencadenamiento. Para obtener más información y ejemplos sobre cómo usar la clase **SqlTriggerContext** , vea [desencadenadores CLR](https://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c).  
  
 Para obtener más información, vea la documentación de referencia de la clase **Microsoft. SqlServer. Server. SqlTriggerContext** en la documentación del SDK de .NET Framework.  
  
## <a name="see-also"></a>Consulte también  
 [Desencadenadores CLR](https://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
