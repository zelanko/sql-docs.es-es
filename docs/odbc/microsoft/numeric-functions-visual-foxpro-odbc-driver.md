---
title: "Funciones numéricas (controlador ODBC de Visual FoxPro) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC numeric functions [ODBC]
- Visual FoxPro ODBC driver [ODBC], numeric functions
- numeric functions [ODBC]
- FoxPro ODBC driver [ODBC], numeric functions
ms.assetid: 7caab48e-cbb5-4bbc-a09b-5cf902e5bc45
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: af884148535018c19a2a7375f3bfc90d73aa5f78
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="numeric-functions-visual-foxpro-odbc-driver"></a>Funciones numéricas (controlador ODBC de Visual FoxPro)
La tabla siguiente describen las funciones numéricas de ODBC compatibles con el controlador ODBC de Visual FoxPro; Cuando la gramática de Visual FoxPro para la misma función difiere de la sintaxis ODBC, se muestra el equivalente de Visual FoxPro.  
  
|Gramática ODBC|Gramática Visual FoxPro|  
|------------------|---------------------------|  
|ABS *(numeric_exp)*||  
|ACOS *(float_exp)*||  
|ASIN *(float_exp)*||  
|ATAN *(float_exp)*||  
|ATAN2 *(float_exp1, float_exp2)*|ATN2 (*float_exp1, float_exp2*)|  
|CEILING *(numeric_exp)*||  
|COS *(float_exp)*||  
|COT *(float_exp)*||  
|GRADOS *(numeric_exp)*|RTOD *(numeric_exp)*|  
|EXP *(float_exp)*||  
|FLOOR *(numeric_exp)*||  
|Registro *(float_exp)*||  
|LOG10 *(float_exp)*||  
|MOD *(integer_exp1, integer_exp2)*||  
|PI *)*||  
|RADIANES *(numeric_exp)*|Destructor *(numeric_exp)*|  
|RAND *([integer_exp])*||  
|REDONDEAR *(numeric_exp, integer_exp)*||  
|Inicio de sesión *(numeric_exp)*||  
|SEN *(float_exp)*||  
|SQRT *(float_exp)*||  
|TAN *(float_exp)*||  
  
 No se admiten las funciones numéricas siguientes:  
  
 POWER *(numeric_exp, integer_exp)*  
  
 TRUNCAR *(numeric_exp, integer_exp)*
