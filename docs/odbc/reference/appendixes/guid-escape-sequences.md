---
title: Secuencias de escape GUID (GUID Escape Sequences) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 44907bfbd884bf361ce5f2ab8b3f6d8a247aba44
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306976"
---
# <a name="guid-escape-sequences"></a>Secuencias de escape GUID
ODBC usa secuencias de escape para literales GUID. La sintaxis de esta secuencia de escape es la siguiente:  
  
```  
{guid 'nnnnnnnn-nnnn-nnnn-nnnn-nnnnnnnnnnnn'}  
```  
  
## <a name="remarks"></a>Observaciones  
 En la notación BNF, la sintaxis es la siguiente:  
  
 *ODBC-guid-escape* ::  
     *GUID ODBC-esc-iniciador* '*guid-value*' *ODBC-esc-terminator*  
  
 *ODBC-esc-iniciador* ::-  
  
 *ODBC-esc-terminator* ::-  
  
 *guid-value* ::- *clock-low-value guid-separator clock-middle-value guid-separator clock-high-value guid-separator clock-seq-value guid-separator node-value*  
  
 *guid-separador* :: -  
  
 *valor bajo* del reloj ::- hex_digit hex_digit hex_digit hex_digit hex_digit *hex_digit hex_digit hex_digit* de hex_digit  
  
 *valor medio del reloj* ::- *hex_digit hex_digit hex_digit hex_digit*  
  
 *valor máximo del reloj* ::- *hex_digit hex_digit hex_digit hex_digit*  
  
 *valor del reloj* ::- *hex_digit hex_digit hex_digit hex_digit*  
  
 *valor del nodo de reloj* ::- hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit hex_digit *hex_digit* hex_digit hex_digit de hex_digit de hex_digit hex_digit  
  
 *hex_digit* :: 0 &#124; 1 &#124; 2 &#124; 3 &#124; 4 &#124; 5 &#124; 6 &#124; 7 &#124; 8 &#124; 9 &#124; A &#124; B &#124; C &#124; D &#124; E &#124; F F  
  
 La secuencia de escape literal GUID se admite si el origen de datos admite el tipo de datos GUID. Una aplicación debe llamar a **SQLGetTypeInfo** para determinar si se admite este tipo de datos.
