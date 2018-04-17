---
title: ENTRE predicado | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- BETWEEN predicate [ODBC]
- SQL grammar [ODBC], between predicate
ms.assetid: 0cc7464b-d788-4720-98d8-411e1169185f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 538d1a6600d0b47967ad7ed67d9a07843af15c29
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="between-predicate"></a>ENTRE el predicado
La sintaxis siguiente:  
  
```  
expression1 BETWEEN expression2 AND expression3  
```  
  
 Devuelve true solo si *expression1* es mayor o igual que *expression2* y *expression1* es menor o igual que *expression3*.  
  
 La semántica de esta sintaxis es diferente para los controladores de base de datos de escritorio y el motor de Microsoft Jet. En Microsoft Jet SQL *expression2* puede ser mayor que *expression3* para que la instrucción devolverá TRUE solo si *expression1* es mayor o igual que *expression3*, y *expression1* es menor o igual que *expression2*.
