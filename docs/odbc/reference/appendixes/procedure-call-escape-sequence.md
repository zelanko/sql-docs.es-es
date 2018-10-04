---
title: Secuencia de Escape de llamada de procedimiento | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], procedure call
- procedure call escape sequence [ODBC]
- ODBC escape sequences [ODBC], procedure call
ms.assetid: 269fbab0-e5f2-4a98-86c0-2d7b647acaae
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 914bd4759552680a57c345dc3a7c3bc1bcc103a6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47806564"
---
# <a name="procedure-call-escape-sequence"></a>Secuencia de Escape de llamada de procedimiento
ODBC utiliza secuencias de escape para las llamadas a procedimiento. La sintaxis de esta secuencia de escape es como sigue:  
  
 **{**[? =]**llamar** *nombre del procedimiento*[**(**[*parámetro*] [, [*parámetro*]]... **)**]**}**  
  
 En la notación de BNF, la sintaxis es como sigue:  
  
 *Escape de ODBC procedimiento* :: =  
  
 &#124;*Esc-ODBC-iniciador* [? =] llamar *procedimiento terminador de esc de ODBC*  
  
 *procedimiento* :: = *nombre del procedimiento* &#124; *nombre del procedimiento* (*lista de parámetros de procedimiento*)  
  
 *identificador de procedimiento* :: = *nombre definido por el usuario*  
  
 *nombre del procedimiento* :: = *identificador de procedimiento*  
  
 &#124;*nombre del propietario*. *identificador de procedimiento*  
  
 &#124;*separador del catálogo: catalog-name* *identificador de procedimiento*  
  
 &#124;*separador del catálogo: catalog-name* [*nombre del propietario*]. *identificador de procedimiento*  
  
 (La sintaxis de la tercera es válida únicamente si el origen de datos no es compatible con los propietarios).  
  
 *nombre del propietario* :: = *nombre definido por el usuario*  
  
 *nombre del catálogo* :: = *nombre definido por el usuario*  
  
 *separador de catálogo* :: = {*definido por la implementación*}  
  
 (Se devuelve el separador del catálogo a través de **SQLGetInfo** con la opción de información SQL_CATALOG_NAME_SEPARATOR.)  
  
 *lista de parámetros de procedimiento* :: = *parámetro de procedimiento*  
  
 &#124;*parámetro de procedimiento*, *lista de parámetros de procedimiento*  
  
 *parámetro de procedimiento* :: = *parámetros dinámicos* &#124; *literal* &#124; *cadena vacía*  
  
 *cadena vacía* :: =  
  
 *Iniciador de esc de ODBC* :: = {  
  
 *Terminador de esc de ODBC* :: =}  
  
 (Si un parámetro de procedimiento es una cadena vacía, el procedimiento utiliza el valor predeterminado para ese parámetro).  
  
 Para determinar si el origen de datos es compatible con los procedimientos y el controlador admite la sintaxis de invocación del procedimiento ODBC, una aplicación puede llamar a **SQLGetInfo** con el tipo de información SQL_PROCEDURES.
