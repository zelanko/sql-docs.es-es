---
title: Objeto SqlTriggerContext ? Microsoft Docs
description: En la integración de SQL Server CLR, la clase SqlTriggerContext proporciona información de contexto para un desencadenador, incluido el tipo de acción y las columnas modificadas en la operación.
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
ms.openlocfilehash: 55e0ac850071615d9be7fb47442ed674eefab00a
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487470"
---
# <a name="sqltriggercontext-object"></a>Objeto SqlTriggerContext
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La clase **SqlTriggerContext** proporciona información de contexto acerca del desencadenador. Esto incluye el tipo de acción que ha provocado la activación del desencadenador, las columnas que se modificaron en una operación UPDATE y, en el caso de un desencadenador de lenguaje de definición de datos (DDL), una estructura de XML **EventData** que describe la operación de desencadenamiento. Para obtener más información y ejemplos de cómo utilizar la clase **SqlTriggerContext,** vea [Desencadenadores de CLR](https://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c).  
  
 Para obtener más información, vea la documentación de referencia de la clase **Microsoft.SqlServer.Server.SqlTriggerContext** en la documentación del SDK de .NET Framework.  
  
## <a name="see-also"></a>Consulte también  
 [Desencadenadores de CLR](https://msdn.microsoft.com/library/302a4e4a-3172-42b6-9cc0-4a971ab49c1c)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)  
  
  
