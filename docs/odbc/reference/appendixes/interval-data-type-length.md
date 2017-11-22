---
title: Longitud de tipo de datos de intervalo | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data types [ODBC], interval data types
- length of data types [ODBC]
- interval data type [ODBC], length
ms.assetid: e9eb38d8-f9db-4401-8c62-aa394054cbbf
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c3435106f53d791646a16e1ba9c1a55b75c73a79
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="interval-data-type-length"></a>Longitud del tipo de datos de intervalo
Las reglas siguientes se utilizan para determinar la longitud de un tipo de datos del intervalo de caracteres. Longitud se expresa en número de caracteres. El número de bytes depende del juego de caracteres. La longitud incluye los siguientes valores suman:  
  
-   Dos caracteres para cada campo en el intervalo que no sea el campo inicial.  
  
-   En el campo inicial, el número de caracteres que es la precisión inicial expresa o implícita. Si no se especifica la precisión inicial, el valor predeterminado es 2.  
  
-   Un carácter para el separador entre los campos.  
  
-   Uno más la precisión de segundos expresas o implícitas. Si no se especifica la precisión de segundos, el valor predeterminado es 6.  
  
 Valores de longitud de columna específicos para cada tipo de datos del intervalo están incluidos en [tamaño de la columna](../../../odbc/reference/appendixes/column-size.md).
