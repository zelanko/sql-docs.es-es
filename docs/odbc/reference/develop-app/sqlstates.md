---
title: SQLSTATEs (SQLSTATEs) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: be4bca929b8d48c301c6e71917503387004a6ec5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299732"
---
# <a name="sqlstates"></a>SQLSTATE
SQLSTATEs proporcionan información detallada sobre la causa de una advertencia o error. Los SQLSTATEs de este manual se basan en los que se encuentran en la especificación de la CLI ISO/IEF, aunque los SQLSTATEs que comienzan con IM son específicos de ODBC.  
  
 A diferencia de los códigos de retorno, los SQLSTATEs de este manual son directrices y los controladores no son necesarios para devolverlos. Por lo tanto, mientras que los controladores deben devolver el SQLSTATE adecuado para cualquier error o advertencia que son capaces de detectar, las aplicaciones no deben contar con que esto siempre se produzca. Las razones de esta situación son dobles:  
  
-   **Incompleta** Aunque este manual enumera un gran número de errores y advertencias y posibles causas para esos errores y advertencias, no está completo y probablemente nunca lo será; implementaciones de conductores simplemente varían demasiado. Cualquier controlador determinado probablemente no devolverá todos los SQLSTATEs enumerados en este manual y podría devolver SQLSTATEs no enumerados en este manual.  
  
-   **Complejidad** Algunos motores de base de datos, especialmente los motores de base de datos relacionales, devuelven literalmente miles de errores y advertencias. Es poco probable que los controladores de estos motores de estos motores asignen todos estos errores y advertencias a SQLSTATEs debido al esfuerzo implicado, la inexactitud de las asignaciones, el gran tamaño del código resultante y el bajo valor del código resultante, que a menudo devuelve errores de programación que nunca deben encontrarse en tiempo de ejecución. Por lo tanto, los controladores deben asignar tantos errores y advertencias como parezca razonable y asegúrese de asignar esos errores y advertencias en los que se puede basar la lógica de la aplicación, como SQLSTATE 01004 (datos truncados).  
  
 Dado que los SQLSTATEs no se devuelven de forma fiable, la mayoría de las aplicaciones solo se muestran al usuario junto con su mensaje de diagnóstico asociado, que a menudo se adapta al error o advertencia específico que se produjo y al código de error nativo. Rara vez hay ninguna pérdida de funcionalidad al hacer esto, porque las aplicaciones no pueden basar la lógica de programación en la mayoría de los SQLSTATEs de todos modos. Por ejemplo, supongamos que **SQLExecDirect** devuelve SQLSTATE 42000 (error de sintaxis o infracción de acceso). Si la instrucción SQL que causó este error está codificada de forma rígida o compilada por la aplicación, se trata de un error de programación y el código debe corregirse. Si el usuario introduce la instrucción SQL, se trata de un error de usuario y la aplicación ha hecho todo lo posible informando al usuario del problema.  
  
 Cuando las aplicaciones realizan la lógica de programación base en SQLSTATEs, deben estar preparadas para que SQLSTATE no se devuelva o para que se devuelva un SQLSTATE diferente. Exactamente qué SQLSTATEs se devuelven de forma fiable sólo se puede basar en la experiencia con numerosos controladores. Sin embargo, una directriz general es que sqlSTATEs para los errores que se producen en el controlador o administrador de controladores, a diferencia del origen de datos, es más probable que se devuelva de forma fiable. Por ejemplo, la mayoría de los controladores probablemente devuelven SQLSTATE HYC00 (característica opcional no implementada), mientras que menos controladores probablemente devuelven SQLSTATE 42021 (la columna ya existe).  
  
 Los siguientes SQLSTATEs indican errores o advertencias en tiempo de ejecución y son buenos candidatos en los que basar la lógica de programación. Sin embargo, no hay garantía de que todos los conductores los devuelvan.  
  
-   01004 (Datos truncados)  
  
-   01S02 (valor de opción cambiado)  
  
-   HY008 (Operación cancelada)  
  
-   HYC00 (característica opcional no implementada)  
  
-   HYT00 (tiempo de espera expirado)  
  
 SQLSTATE HYC00 (característica opcional no implementada) es particularmente importante porque es la única manera en que una aplicación puede determinar si un controlador admite una instrucción determinada o un atributo de conexión.  
  
 Para obtener una lista completa de SQLSTATEs y qué funciones los [devuelven, vea Apéndice A: Códigos](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md)de error ODBC . Para obtener una explicación detallada de las condiciones en las que cada función puede devolver un SQLSTATE determinado, vea esa función.
