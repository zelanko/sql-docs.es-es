---
title: SQLSTATEs | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], sqlstates
- SQLSTATE [ODBC]
ms.assetid: f29fff2e-3d09-4a8c-a2f9-2059062cbebf
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8213c08e6844003d880129dda4b441a5592bbc86
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68107345"
---
# <a name="sqlstates"></a>SQLSTATE
SQLSTATE proporciona información detallada sobre la causa de una advertencia o error. El SQLSTATE en este manual se basa en los que se encuentran en la especificación ISO/IEF CLI, aunque esos SQLSTATE que comienzan con la mensajería instantánea es específica de ODBC.  
  
 A diferencia de los códigos de retorno, el SQLSTATE en este manual es directrices y no se requieren controladores para devolverlos. Por lo tanto, mientras que los controladores deben devolver el valor de SQLSTATE adecuado para cualquier error o advertencia son capaces de detectar, las aplicaciones no deben contar con siempre que se produzca este. Los motivos para esta situación son dos:  
  
-   **Estado incompleto** aunque este manual muestra un gran número de errores y advertencias y posibles causas de dichos errores y advertencias, no está completo y probablemente nunca será; las implementaciones de controladores simplemente varían demasiado. Cualquier controlador determinado probablemente no devolverá todos los SQLSTATEs enumeran en este manual y podrían devolverse SQLState no aparece en este manual.  
  
-   **Complejidad** algunos motores de base de datos - motores de base de datos relacional especialmente - devuelvan literalmente miles de errores y advertencias. Los controladores de estos motores están poco probable que se asignan todos estos errores y advertencias para SQLSTATE debido a los esfuerzos implicados, la inexactness de las asignaciones, el gran tamaño del código resultante y el valor bajo del código resultante, que a menudo devuelve la programación errores que nunca deben encontrarse en tiempo de ejecución. Por lo tanto, los controladores deben asignar todos los errores y advertencias como parece razonable y asegúrese de asignar esos errores y advertencias en la lógica de aplicación que podrían basarse, como SQLSTATE 01004 (datos truncados).  
  
 Dado que SQLState no se devuelve de forma confiable, mayoría de las aplicaciones simplemente mostrarlos al usuario junto con su mensaje de diagnóstico asociado, que a menudo se adapta para el error o advertencia que se produjeron y el código de error nativo. No hay rara vez ninguna pérdida de funcionalidad en hacerlo, porque las aplicaciones no pueden basar la lógica de programación en la mayoría de SQLSTATE de todos modos. Por ejemplo, supongamos que **SQLExecDirect** devuelve SQLSTATE 42000 (sintaxis o infracción de acceso). Si la instrucción SQL que causó este error está codificado de forma rígida o generada por la aplicación, se trata de un error de programación y el código debe solucionarse. Si la instrucción SQL escrita por el usuario, se trata de un error de usuario y la aplicación se ha realizado todo lo que es posible si se informa al usuario del problema.  
  
 Cuando las aplicaciones basar la lógica de programación en SQLSTATE, debe estar preparados para el valor de SQLSTATE no va a devolver o para un valor de SQLSTATE diferentes va a devolver. Exactamente qué SQLSTATE se devuelve de forma confiable puede basarse solo en la experiencia con varios controladores. Sin embargo, la norma general es que SqlState para errores que se producen en el controlador o el Administrador de controladores, en lugar de origen de datos, es más probable que se va a devolver de forma confiable. Por ejemplo, la mayoría de los controladores probablemente devolverá SQLSTATE HYC00 (característica opcional no implementada), mientras que los controladores menos probablemente devuelven SQLSTATE 42021 (columna ya existe).  
  
 El SQLSTATE siguiente indica errores de tiempo de ejecución o las advertencias y es buenos candidatos en los que se va a basar la lógica de programación. Sin embargo, no hay ninguna garantía de que todos los controladores de devuelven.  
  
-   01004 (datos truncados)  
  
-   01S02 de SQLState (valor de opción cambiado)  
  
-   HY008 (operación cancelada)  
  
-   HYC00 (característica opcional no implementada)  
  
-   HYT00 (tiempo de espera expirado)  
  
 SQLSTATE HYC00 (característica opcional no implementada) es especialmente importante porque es la única manera en que una aplicación puede determinar si un controlador es compatible con un atributo de instrucción o de conexión determinado.  
  
 Para obtener una lista completa de códigos SQLState y las funciones que devuelven, consulte [Apéndice A: Códigos de Error ODBC](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md). Para obtener una explicación detallada de las condiciones en las que cada función puede devolver un determinado valor de SQLSTATE, consulte esa función.
