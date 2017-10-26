---
title: "Marcadores de parámetros | Documentos de Microsoft"
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
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
- parameter markers [ODBC]
ms.assetid: 07213d04-cd31-45fd-a8c8-2e16e09eeaf4
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c2c8708c18abee3609fc0b01f6ccd2e0362e5706
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="parameter-markers"></a>Marcadores de parámetros
Según la especificación de SQL-92, una aplicación no puede colocar los marcadores de parámetros en las siguientes ubicaciones. Para obtener una lista más completa, vea la especificación de SQL-92.  
  
-   En un **seleccione** lista  
  
-   Como ambos *expresiones* en un *predicado de comparación*  
  
-   Como ambos operandos de un operador binario  
  
-   Como los operandos primeros y segundo de un **BETWEEN** operación  
  
-   Como el primer y el tercer operandos de una **BETWEEN** operación  
  
-   Como la expresión y el primer valor de un **IN** operación  
  
-   Como el operando de una unaria + o – operación  
  
-   Como el argumento de un *referencia de funciones de conjunto*  
  
 Para obtener más información acerca de los marcadores de parámetros, vea la especificación de SQL-92. Para obtener más información acerca de los parámetros, vea [parámetros de la instrucción](../../../odbc/reference/develop-app/statement-parameters.md).

