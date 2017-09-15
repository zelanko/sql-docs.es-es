---
title: SQLSTATE | Documentos de Microsoft
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
- diagnostic information [ODBC], sqlstates
- SQLSTATE [ODBC]
ms.assetid: f29fff2e-3d09-4a8c-a2f9-2059062cbebf
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0c99959fac35ac1cd312ab3d434f607c3f256dd8
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlstates"></a>SQLSTATE
SQLSTATE proporciona información detallada sobre la causa de un error o advertencia. El SQLSTATE en este manual se basa en las que se encuentran en la especificación ISO/IEF CLI, aunque esos SQLSTATE que empiezan por mensajería instantánea es específico de ODBC.  
  
 A diferencia de los códigos de retorno, el SQLSTATE en este manual es directrices, y no se requieren controladores para devolverlos. Por lo tanto, mientras controladores deben devolver el valor de SQLSTATE adecuado para cualquier error o advertencia son capaces de detectar, no deben depender de las aplicaciones siempre que se produzca este. Las razones para esta situación tienen dos aspectos:  
  
-   **Estado incompleto** aunque este manual muestra un gran número de errores y advertencias y las posibles causas de los errores y advertencias, no está completo y que probablemente nunca será; las implementaciones de controladores simplemente varían demasiado. Cualquier controlador determinado probablemente no devolverá todos lo SQLSTATE enumeran en este manual y devuelvan SQLState no aparece en este manual.  
  
-   **Complejidad** algunos motores de base de datos, los motores de base de datos relacional especialmente: devolver miles de los errores y advertencias. Los controladores de estos motores no vayan a asignar todos estos errores y advertencias para SQLSTATE debido a la intervención implicados, la inexactness de las asignaciones, el gran tamaño del código resultante y el valor bajo del código resultante, que a menudo devuelve programación errores que nunca deben encontrarse en tiempo de ejecución. Por lo tanto, los controladores deben asignar todos los errores y advertencias como parece razonable y asegúrese de asignar los errores y advertencias en qué lógica de la aplicación podrían basarse, como SQLSTATE 01004 (datos truncados).  
  
 Dado que SQLState no se devuelve de forma confiable, mayoría de las aplicaciones solo los muestran al usuario junto con su mensaje de diagnóstico asociado, que a menudo se adapta para el error o advertencia que se produjeron y código de error nativo. Hay rara vez ninguna pérdida de funcionalidad al hacerlo así, porque las aplicaciones no pueden basar la lógica de programación en SQLSTATE mayoría todos modos. Por ejemplo, suponga que **SQLExecDirect** devuelve SQLSTATE 42000 (sintaxis o infracción de acceso). Si la instrucción SQL que causó este error está codificado de forma rígida o generada por la aplicación, se trata de un error de programación y el código debe corregirse. Si la instrucción SQL es especificada por el usuario, se trata de un error de usuario y la aplicación haya todo lo que es posible que informa al usuario del problema.  
  
 Cuando las aplicaciones basar la lógica de programación en SQLSTATE, debe estar preparados para el valor de SQLSTATE no va a devolver o para un valor de SQLSTATE diferentes va a devolver. Exactamente qué SQLSTATE se devuelve de forma confiable puede basarse solo en la experiencia con numerosos controladores. Sin embargo, una regla general es que SqlState para errores que se producen en el controlador o el Administrador de controladores, en lugar de origen de datos, es más probable que se devuelve de forma confiable. Por ejemplo, la mayoría de los controladores probablemente devolverá SQLSTATE HYC00 (característica opcional no implementada), mientras que los controladores menos probablemente devuelven SQLSTATE 42021 (ya existe una columna).  
  
 El SQLSTATE siguiente indica errores de tiempo de ejecución o advertencias y es buenos candidatos en los que se va a basar la lógica de programación. Sin embargo, no hay ninguna garantía de que todos los controladores de estos valores.  
  
-   01004 (datos truncados)  
  
-   01S02 de SQLState (valor de opción cambiado)  
  
-   HY008 (operación cancelada)  
  
-   HYC00 (característica opcional no implementada)  
  
-   HYT00 (tiempo de espera expiró)  
  
 SQLSTATE HYC00 (característica opcional no implementada) es especialmente importante porque es la única manera en que una aplicación puede determinar si un controlador es compatible con un determinado atributo de conexión o instrucción.  
  
 Para obtener una lista completa de códigos SQLState y qué funciones de estos valores, consulte [Apéndice A: códigos de Error de ODBC](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md). Para obtener una explicación detallada de las condiciones en las que cada función podría devolver un valor de SQLSTATE determinado, consulte esa función.
