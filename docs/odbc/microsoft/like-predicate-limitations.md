---
title: COMO Limitaciones de Predicados ( LIKE Predicate Limitations) Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298965"
---
# <a name="like-predicate-limitations"></a>Al igual que las limitaciones de predicado
Si los datos de una columna tienen más de 255 caracteres, la comparación LIKE se basará solo en los primeros 255 caracteres.  
  
 Un LIKE utilizado en un procedimiento se soporta solamente con patrones constantes. Los controladores de base de datos de escritorio admiten la coincidencia de patrones LIKE de SQL-92.  
  
 No se admite el uso de una cláusula de escape en un predicado LIKE.  
  
 No se debe realizar una comparación LIKE en una columna que contenga datos de un tipo de datos numérico o flotante. Los resultados pueden ser impredecibles. Para obtener más información, consulte la Guía del programador de *Microsoft Jet Database Engine*.
