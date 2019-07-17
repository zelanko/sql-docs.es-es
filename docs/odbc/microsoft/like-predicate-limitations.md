---
title: Al igual que las limitaciones de predicado | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8cd3cebfcf20df2f8a3a786ea66fd28dd76307c0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68119711"
---
# <a name="like-predicate-limitations"></a>Al igual que las limitaciones de predicado
Si los datos de una columna tiene más de 255 caracteres, la comparación LIKE se basará únicamente en los primeros 255 caracteres.  
  
 Un tipo que se usa en un procedimiento solo se admite con modelos de constante. Los controladores de base de datos de escritorio admiten SQL-92 como coincidencia de patrones.  
  
 No se admite el uso de una cláusula de escape en un predicado LIKE.  
  
 No debe realizarse una comparación LIKE en una columna que contiene los datos de un tipo de datos numérico o float. Los resultados pueden ser imprevisibles. Para obtener más información, consulte el *Guía del programador del motor de base de datos Jet de Microsoft*.
