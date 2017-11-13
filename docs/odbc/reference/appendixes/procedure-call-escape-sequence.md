---
title: Secuencia de Escape de llamada de procedimiento | Documentos de Microsoft
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
- escape sequences [ODBC], procedure call
- procedure call escape sequence [ODBC]
- ODBC escape sequences [ODBC], procedure call
ms.assetid: 269fbab0-e5f2-4a98-86c0-2d7b647acaae
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0ba89ae47d223ea17f02cb07976510d78ff3660e
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="procedure-call-escape-sequence"></a>Secuencia de Escape de llamada de procedimiento
ODBC utiliza secuencias de escape para las llamadas de procedimiento. La sintaxis de esta secuencia de escape es como sigue:  
  
 **{**[? =]**llamar a** *nombre del procedimiento*[**(**[*parámetro*] [, [*parámetro*]] ... **)**]**}**  
  
 En la notación de BNF, la sintaxis es la siguiente:  
  
 *Escape de procedimiento de ODBC* :: =  
  
 &#124; *Iniciador de esc de ODBC* [? =] llamar *procedimiento terminador de esc de ODBC*  
  
 *procedimiento* :: = *nombre del procedimiento* &#124; *nombre del procedimiento* (*lista de parámetros de procedimiento*)  
  
 *identificador de procedimiento* :: = *nombre definido por el usuario*  
  
 *nombre del procedimiento* :: = *identificador de procedimiento*  
  
 &#124; *nombre del propietario*. *identificador de procedimiento*  
  
 &#124; *separador del catálogo de nombre del catálogo* *identificador de procedimiento*  
  
 &#124; *separador del catálogo de nombre del catálogo* [*nombre del propietario*]. *identificador de procedimiento*  
  
 (La sintaxis de la tercera es válida únicamente si el origen de datos no es compatible con los propietarios).  
  
 *nombre del propietario* :: = *nombre definido por el usuario*  
  
 *nombre del catálogo* :: = *nombre definido por el usuario*  
  
 *separador de catálogo* :: = {*definido por la implementación*}  
  
 (El separador del catálogo se devuelve a través de **SQLGetInfo** con la opción de información de SQL_CATALOG_NAME_SEPARATOR.)  
  
 *lista de parámetros de procedimiento* :: = *parámetro de procedimiento*  
  
 &#124; *parámetro de procedimiento*, *lista de parámetros de procedimiento*  
  
 *parámetro de procedimiento* :: = *parámetro dinámico* &#124; *literal* &#124; *cadena vacía*  
  
 *cadena vacía* :: =  
  
 *Iniciador de esc de ODBC* :: = {  
  
 *Terminador de esc de ODBC* :: =}  
  
 (Si un parámetro de procedimiento es una cadena vacía, el procedimiento utiliza el valor predeterminado para ese parámetro).  
  
 Para determinar si el origen de datos es compatible con los procedimientos y el controlador es compatible con la sintaxis de invocación de procedimiento ODBC, una aplicación puede llamar a **SQLGetInfo** con el tipo de información de SQL_PROCEDURES.

