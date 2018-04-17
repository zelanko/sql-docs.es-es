---
title: Secuencias de Escape Interval | Documentos de Microsoft
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
- interval literals [ODBC]
- escape sequences [ODBC], interval
- ODBC escape sequences [ODBC], interval
ms.assetid: 303e8dab-8f13-4fa5-857f-15cc1f75bdd6
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a9ef232521850dbf6007942d7758ce2b5820a335
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="interval-escape-sequences"></a>Secuencias de Escape Interval
ODBC utiliza secuencias de escape para literales de intervalo. La sintaxis de esta secuencia de escape es como sigue:  
  
 {*intervalo literal*}  
  
 Para obtener la sintaxis BNF de *intervalo literal*, consulte el [sintaxis de literales de intervalo](../../../odbc/reference/appendixes/interval-literal-syntax.md) sección más adelante en este apéndice.  
  
 Se admite la secuencia de escape de literales de intervalo si los tipos de datos de intervalo son compatibles con el origen de datos. Una aplicación debe llamar a **SQLGetTypeInfo** para determinar si se admiten estos tipos de datos.
