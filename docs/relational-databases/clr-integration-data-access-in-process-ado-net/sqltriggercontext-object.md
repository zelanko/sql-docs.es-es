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
ms.openlocfilehash: c6f11eda2ef791eb8c987af8d82149507770d47a
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/07/2020
ms.locfileid: "91809168"
---
# <a name="sqltriggercontext-object"></a>Objeto SqlTriggerContext
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  La clase **SqlTriggerContext** proporciona información de contexto acerca del desencadenador. Esto incluye el tipo de acción que ha provocado la activación del desencadenador, las columnas que se modificaron en una operación UPDATE y, en el caso de un desencadenador de lenguaje de definición de datos (DDL), una estructura de XML **EventData** que describe la operación de desencadenamiento. Para obtener más información y ejemplos sobre cómo usar la clase **SqlTriggerContext** , vea [desencadenadores CLR](/dotnet/framework/data/adonet/sql/clr-triggers).  
  
 Para obtener más información, vea la documentación de referencia de la clase **Microsoft. SqlServer. Server. SqlTriggerContext** en la documentación del SDK de .NET Framework.  
  
## <a name="see-also"></a>Consulte también  
 [Desencadenadores CLR](/dotnet/framework/data/adonet/sql/clr-triggers)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
