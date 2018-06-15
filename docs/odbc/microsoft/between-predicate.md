---
title: ENTRE predicado | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- BETWEEN predicate [ODBC]
- SQL grammar [ODBC], between predicate
ms.assetid: 0cc7464b-d788-4720-98d8-411e1169185f
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9909930941c7dfd6a180ca3e33b7e89c7d9c4825
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32898400"
---
# <a name="between-predicate"></a>ENTRE el predicado
La sintaxis siguiente:  
  
```  
expression1 BETWEEN expression2 AND expression3  
```  
  
 Devuelve true solo si *expression1* es mayor o igual que *expression2* y *expression1* es menor o igual que *expression3*.  
  
 La semántica de esta sintaxis es diferente para los controladores de base de datos de escritorio y el motor de Microsoft Jet. En Microsoft Jet SQL *expression2* puede ser mayor que *expression3* para que la instrucción devolverá TRUE solo si *expression1* es mayor o igual que *expression3*, y *expression1* es menor o igual que *expression2*.
