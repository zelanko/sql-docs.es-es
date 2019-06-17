---
title: Secuencias de Escape GUID | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC escape sequences [ODBC], GUID
- escape sequences [ODBC], guid
- guid escape sequence [ODBC]
ms.assetid: 71d43ef9-4a31-493e-b9e0-f864e9ef3ce6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bf41671abc6393a18fad06e1debd297fed1f04c5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63188956"
---
# <a name="guid-escape-sequences"></a>Secuencias de escape GUID
ODBC utiliza secuencias de escape para literales GUID. La sintaxis de esta secuencia de escape es como sigue:  
  
```  
{guid 'nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn'}  
```  
  
## <a name="remarks"></a>Comentarios  
 En la notación de BNF, la sintaxis es como sigue:  
  
 *ODBC-guid-escape* ::=  
     *Guid del iniciador de esc de ODBC* '*valor de guid*' *terminador de esc de ODBC*  
  
 *ODBC-esc-initiator* ::= {  
  
 *ODBC-esc-terminator* ::= }  
  
 *valor de GUID* :: = *separador de guid de reloj de gran valor guid clock-seq-value-separador nodo-valor del separador de guid de reloj poco valor separador de guid de valor medio de reloj*  
  
 *guid-separator* ::= -  
  
 *valor bajo de reloj* :: = *hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit*  
  
 *clock-middle-value* ::= *hex_digit hex_digit hex_digit hex_digit*  
  
 *valor del alto de reloj* :: = *hex_digit hex_digit hex_digit hex_digit*  
  
 *clock-seq-value* ::= *hex_digit hex_digit hex_digit hex_digit*  
  
 *clock-node-value* ::= *hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit*  
  
 *hex_digit* ::= 0 &#124; 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9 &#124; A &#124; B &#124; C &#124; D &#124; E &#124; F  
  
 Si el tipo de datos GUID es compatible con el origen de datos, se admite la secuencia de escape literal de GUID. Una aplicación debe llamar a **SQLGetTypeInfo** para determinar si se admite este tipo de datos.
