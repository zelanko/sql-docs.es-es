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
ms.topic: conceptual
helpviewer_keywords:
- interval literals [ODBC]
- escape sequences [ODBC], interval
- ODBC escape sequences [ODBC], interval
ms.assetid: 303e8dab-8f13-4fa5-857f-15cc1f75bdd6
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0e3a475170fed349a5bf85eb4f23bb93fe4ae804
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="interval-escape-sequences"></a>Secuencias de Escape Interval
ODBC utiliza secuencias de escape para literales de intervalo. La sintaxis de esta secuencia de escape es como sigue:  
  
 {*intervalo literal*}  
  
 Para obtener la sintaxis BNF de *intervalo literal*, consulte el [sintaxis de literales de intervalo](../../../odbc/reference/appendixes/interval-literal-syntax.md) sección más adelante en este apéndice.  
  
 Se admite la secuencia de escape de literales de intervalo si los tipos de datos de intervalo son compatibles con el origen de datos. Una aplicación debe llamar a **SQLGetTypeInfo** para determinar si se admiten estos tipos de datos.
