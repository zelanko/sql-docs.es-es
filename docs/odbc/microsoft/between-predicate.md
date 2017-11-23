---
title: ENTRE predicado | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- BETWEEN predicate [ODBC]
- SQL grammar [ODBC], between predicate
ms.assetid: 0cc7464b-d788-4720-98d8-411e1169185f
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c93e94ff9b4b3c0b4117e3e4b8c3fafd35fac09a
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="between-predicate"></a>ENTRE el predicado
La sintaxis siguiente:  
  
```  
expression1 BETWEEN expression2 AND expression3  
```  
  
 Devuelve true solo si *expression1* es mayor o igual que *expression2* y *expression1* es menor o igual que *expression3*.  
  
 La semántica de esta sintaxis es diferente para los controladores de base de datos de escritorio y el motor de Microsoft Jet. En Microsoft Jet SQL *expression2* puede ser mayor que *expression3* para que la instrucción devolverá TRUE solo si *expression1* es mayor o igual que *expression3*, y *expression1* es menor o igual que *expression2*.
