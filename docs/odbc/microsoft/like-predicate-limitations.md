---
title: Al igual que las limitaciones de predicado | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- LIKE predicate limitations [ODBC]
- ODBC SQL grammar, LIKE predicate limitations
ms.assetid: dbd39099-caf6-4c4c-9ad8-f6c63c1bd5e4
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 5668f03e785c0d27133965f16af40ce69c2a2567
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="like-predicate-limitations"></a>Al igual que las limitaciones de predicado
Si los datos de una columna tiene más de 255 caracteres, la comparación LIKE se basará en los primeros 255 caracteres.  
  
 Un tipo que se usa en un procedimiento es compatible solo con modelos de constante. Los controladores de base de datos de escritorio admiten SQL-92 como coincidencia de patrones.  
  
 No se admite el uso de una cláusula de escape en un predicado LIKE.  
  
 No se debe realizar una comparación LIKE en una columna que contiene los datos de un tipo de datos numérico o float. Los resultados pueden ser impredecibles. Para obtener más información, consulte el *Guía del programador del motor de base de datos Jet de Microsoft*.

