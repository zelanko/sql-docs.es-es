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
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63188498"
---
# <a name="procedure-call-escape-sequence"></a>Secuencia de Escape de llamada de procedimiento
ODBC utiliza secuencias de escape para las llamadas a procedimiento. La sintaxis de esta secuencia de escape es como sigue:  
  
 **{** [?=]**call** *procedure-name*[ **(** [*parameter*][,[*parameter*]]... **)** ] **}**  
  
 En la notación de BNF, la sintaxis es como sigue:  
  
 *Escape de ODBC procedimiento* :: =  
  
 &#124;*Esc-ODBC-iniciador* [? =] llamar *procedimiento terminador de esc de ODBC*  
  
 *procedure* ::= *procedure-name* &#124; *procedure-name* (*procedure-parameter-list*)  
  
 *procedure-identifier* ::= *user-defined-name*  
  
 *procedure-name* ::= *procedure-identifier*  
  
 &#124; *owner-name*.*procedure-identifier*  
  
 &#124;*separador del catálogo: catalog-name* *identificador de procedimiento*  
  
 &#124;*separador del catálogo: catalog-name* [*nombre del propietario*]. *identificador de procedimiento*  
  
 (La sintaxis de la tercera es válida únicamente si el origen de datos no es compatible con los propietarios).  
  
 *owner-name* ::= *user-defined-name*  
  
 *catalog-name* ::= *user-defined-name*  
  
 *catalog-separator* ::= {*implementation-defined*}  
  
 (Se devuelve el separador del catálogo a través de **SQLGetInfo** con la opción de información SQL_CATALOG_NAME_SEPARATOR.)  
  
 *procedure-parameter-list* ::= *procedure-parameter*  
  
 &#124; *procedure-parameter*, *procedure-parameter-list*  
  
 *procedure-parameter* ::= *dynamic-parameter* &#124; *literal* &#124; *empty-string*  
  
 *empty-string* ::=  
  
 *ODBC-esc-initiator* ::= {  
  
 *ODBC-esc-terminator* ::= }  
  
 (Si un parámetro de procedimiento es una cadena vacía, el procedimiento utiliza el valor predeterminado para ese parámetro).  
  
 Para determinar si el origen de datos es compatible con los procedimientos y el controlador admite la sintaxis de invocación del procedimiento ODBC, una aplicación puede llamar a **SQLGetInfo** con el tipo de información SQL_PROCEDURES.
