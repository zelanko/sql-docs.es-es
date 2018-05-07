---
title: Al igual que las limitaciones de predicado | Documentos de Microsoft
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
- LIKE predicate limitations [ODBC]
- ODBC SQL grammar, LIKE predicate limitations
ms.assetid: dbd39099-caf6-4c4c-9ad8-f6c63c1bd5e4
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 891c6499f54c56635d74289517e8cf33f66ba4ee
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="like-predicate-limitations"></a>Al igual que las limitaciones de predicado
Si los datos de una columna tiene más de 255 caracteres, la comparación LIKE se basará en los primeros 255 caracteres.  
  
 Un tipo que se usa en un procedimiento es compatible solo con modelos de constante. Los controladores de base de datos de escritorio admiten SQL-92 como coincidencia de patrones.  
  
 No se admite el uso de una cláusula de escape en un predicado LIKE.  
  
 No se debe realizar una comparación LIKE en una columna que contiene los datos de un tipo de datos numérico o float. Los resultados pueden ser impredecibles. Para obtener más información, consulte el *Guía del programador del motor de base de datos Jet de Microsoft*.
