---
title: Secuencias de Escape de GUID | Documentos de Microsoft
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
- ODBC escape sequences [ODBC], GUID
- escape sequences [ODBC], guid
- guid escape sequence [ODBC]
ms.assetid: 71d43ef9-4a31-493e-b9e0-f864e9ef3ce6
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 40e4761c271c6ba143864d38b95440d5ac13aa43
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="guid-escape-sequences"></a>Secuencias de Escape GUID
ODBC utiliza secuencias de escape para literales GUID. La sintaxis de esta secuencia de escape es como sigue:  
  
```  
{guid 'nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn'}  
```  
  
## <a name="remarks"></a>Comentarios  
 En la notación de BNF, la sintaxis es la siguiente:  
  
 *Guid de ODBC de escape* :: =  
     *Guid de iniciador de esc de ODBC* '*valor de guid*' *terminador de esc de ODBC*  
  
 *Iniciador de esc de ODBC* :: = {  
  
 *Terminador de esc de ODBC* :: =}  
  
 *valor de GUID* :: = *separador de guid de reloj de gran valor separador de guid de reloj-seq-value nodo-valor del separador de guid de reloj poco valor separador de guid de valor medio de reloj*  
  
 *separador de GUID* :: = -  
  
 *valor del bajo de reloj* :: = *hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit*  
  
 *valor de reloj intermedio* :: = *hex_digit hex_digit hex_digit hex_digit*  
  
 *valor de alto de reloj* :: = *hex_digit hex_digit hex_digit hex_digit*  
  
 *valor de reloj-seq* :: = *hex_digit hex_digit hex_digit hex_digit*  
  
 *valor de nodo de reloj* :: = *hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit*  
  
 *hex_digit* :: = 0 &#124; 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9 &#124; A &#124; B &#124; C &#124; d. &#124; E &#124; F  
  
 Si el tipo de datos GUID es compatible con el origen de datos, se admite la secuencia de escape de literales de GUID. Una aplicación debe llamar a **SQLGetTypeInfo** para determinar si se admite este tipo de datos.
