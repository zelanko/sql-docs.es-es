---
title: COMO las limitaciones de predicados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- LIKE predicate limitations [ODBC]
- ODBC SQL grammar, LIKE predicate limitations
ms.assetid: dbd39099-caf6-4c4c-9ad8-f6c63c1bd5e4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6d596d688956d7bdbf3d9125184d81c16249781c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298965"
---
# <a name="like-predicate-limitations"></a>Al igual que las limitaciones de predicado
Si los datos de una columna tienen más de 255 caracteres, la comparación LIKE solo se basará en los primeros 255 caracteres.  
  
 Una LIKE utilizada en un procedimiento solo se admite con patrones constantes. Los controladores de base de datos de escritorio admiten SQL-92 como coincidencia de patrones.  
  
 No se admite el uso de una cláusula escape en un predicado LIKE.  
  
 No se debe realizar una comparación LIKE en una columna que contenga datos de un tipo de datos float o Numeric. Los resultados pueden ser imprevisibles. Para obtener más información, vea la *Guía del programador de Microsoft Jet motor de base de datos*.
