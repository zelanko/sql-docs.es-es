---
description: ENTRE el predicado
title: BETWEEN (predicado) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- BETWEEN predicate [ODBC]
- SQL grammar [ODBC], between predicate
ms.assetid: 0cc7464b-d788-4720-98d8-411e1169185f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2f2283f5824e4be0c9702bfe8feef9fe3109849a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500388"
---
# <a name="between-predicate"></a>ENTRE el predicado
La sintaxis es:  
  
```  
expression1 BETWEEN expression2 AND expression3  
```  
  
 Devuelve true solo si *expression1* es mayor o igual que *expression2* y *expression1* es menor o igual que *expression3*.  
  
 La semántica de esta sintaxis es diferente para los controladores de base de datos de escritorio y el motor de Microsoft Jet. En Microsoft Jet SQL, *expression2* puede ser mayor que *expression3* para que la instrucción devuelva true solo si *expression1* es mayor o igual que *expression3*, y *expression1* es menor o igual que *expression2*.
