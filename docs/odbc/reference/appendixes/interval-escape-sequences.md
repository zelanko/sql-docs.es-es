---
title: Secuencias de escape de intervalos ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interval literals [ODBC]
- escape sequences [ODBC], interval
- ODBC escape sequences [ODBC], interval
ms.assetid: 303e8dab-8f13-4fa5-857f-15cc1f75bdd6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9fe7f6941e9ec9fba8b6698faaa18a678732dd6f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304960"
---
# <a name="interval-escape-sequences"></a>Secuencias de escape de intervalo
ODBC utiliza secuencias de escape para literales de intervalo. La sintaxis de esta secuencia de escape es la siguiente:  
  
 •*Intervalo-literal*?  
  
 Para la sintaxis BNF de *interval-literal*, consulte la sección [Sintaxis literal](../../../odbc/reference/appendixes/interval-literal-syntax.md) de intervalo más adelante en este apéndice.  
  
 La secuencia de escape literal de intervalo se admite si el origen de datos admite los tipos de datos de intervalo. Una aplicación debe llamar a **SQLGetTypeInfo** para determinar si se admiten estos tipos de datos.
