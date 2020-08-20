---
description: SQLSTATE
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b32a965779da1669452e9361e38723e29cfb11ca
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476397"
---
# <a name="sqlstates"></a>SQLSTATE
SQLSTATEs proporcionan información detallada sobre la causa de una advertencia o un error. El SQLSTATEs de este manual se basa en los que se encuentran en la especificación de la CLI ISO/IEF, aunque los SQLSTATEs que empiezan por IM son específicos de ODBC.  
  
 A diferencia de los códigos de retorno, el SQLSTATEs de este manual son instrucciones y no es necesario que los controladores los devuelvan. Por lo tanto, si bien los controladores deben devolver el valor de SQLSTATE adecuado para cualquier error o advertencia que sean capaces de detectar, las aplicaciones no deben contar en esto siempre que se produzca. Los motivos de esta situación son dobles:  
  
-   **Integridad** Aunque este manual muestra un gran número de errores y advertencias, así como las posibles causas de los errores y advertencias, no se completa y probablemente nunca será; las implementaciones de controladores simplemente varían demasiado. Probablemente, cualquier controlador determinado no devolverá todos los SQLSTATEs enumerados en este manual y podría devolver SQLSTATEs no incluido en este manual.  
  
-   **Complejidad** Algunos motores de base de datos, especialmente los motores de base de datos relacional, devuelven literalmente miles de errores y advertencias. No es probable que los controladores de estos motores asignen todos estos errores y advertencias a SQLSTATEs debido al esfuerzo implicado, la inexactitud de las asignaciones, el gran tamaño del código resultante y el valor bajo del código resultante, que a menudo devuelve errores de programación que nunca se deben encontrar en tiempo de ejecución. Por lo tanto, los controladores deben asignar todos los errores y advertencias que parezcan razonables y asegurarse de asignar esos errores y advertencias en los que se podría basar la lógica de la aplicación, como SQLSTATE 01004 (datos truncados).  
  
 Dado que SQLSTATEs no se devuelven de forma confiable, la mayoría de las aplicaciones solo las muestran al usuario junto con su mensaje de diagnóstico asociado, que a menudo se adapta a la advertencia o error específico que se ha producido, y código de error nativo. No suele haber ninguna pérdida de funcionalidad al hacerlo, porque las aplicaciones no pueden basar la lógica de programación en la mayoría de los SQLSTATEs de todos modos. Por ejemplo, suponga que **SQLExecDirect** devuelve SQLSTATE 42000 (error de sintaxis o infracción de acceso). Si la instrucción SQL que causó este error está codificada o generada por la aplicación, se trata de un error de programación y debe corregirse el código. Si el usuario escribe la instrucción SQL, se trata de un error de usuario y la aplicación ha hecho todo lo posible informando al usuario del problema.  
  
 Cuando las aplicaciones realizan la lógica de programación base en SQLSTATEs, deben estar preparadas para que no se devuelvan los SQLSTATE o para que se devuelva un SQLSTATE diferente. Exactamente qué SQLSTATEs se devuelven de forma confiable solo se pueden basar en la experiencia con numerosos controladores. Sin embargo, una directriz general es que SQLSTATEs para los errores que se producen en el controlador o en el administrador de controladores, en lugar del origen de datos, es más probable que se devuelvan de forma confiable. Por ejemplo, es probable que la mayoría de los controladores devuelvan SQLSTATE HYC00 (característica opcional no implementada), pero es probable que haya menos controladores que devuelvan SQLSTATE 42021 (la columna ya existe).  
  
 Los siguientes SQLSTATEs indican errores en tiempo de ejecución o advertencias y son buenos candidatos en los que basar la lógica de programación. Sin embargo, no hay ninguna garantía de que todos los controladores los devuelvan.  
  
-   01004 (datos truncados)  
  
-   01S02 (valor de opción cambiado)  
  
-   HY008 (operación cancelada)  
  
-   HYC00 (característica opcional no implementada)  
  
-   HYT00 (tiempo de espera agotado)  
  
 SQLSTATE HYC00 (característica opcional no implementada) es especialmente importante, ya que es la única manera en que una aplicación puede determinar si un controlador admite una instrucción o un atributo de conexión determinados.  
  
 Para obtener una lista completa de SQLSTATEs y las funciones que devuelven, consulte el [apéndice a: códigos de error ODBC](../../../odbc/reference/appendixes/appendix-a-odbc-error-codes.md). Para obtener una explicación detallada de las condiciones en las que cada función puede devolver un SQLSTATE determinado, vea esa función.
