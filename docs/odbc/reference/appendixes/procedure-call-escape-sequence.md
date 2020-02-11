---
title: Secuencia de escape de llamada de procedimiento | Microsoft Docs
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
ms.openlocfilehash: aa936eb9f8ef3328945d4ece63fb36432a5fd618
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68100589"
---
# <a name="procedure-call-escape-sequence"></a>Secuencia de Escape de llamada de procedimiento
ODBC utiliza secuencias de escape para las llamadas a procedimientos. La sintaxis de esta secuencia de escape es la siguiente:  
  
 **{**[? =]**Call** *procedure-Name*[**(**[*parámetro*] [, [*parámetro*]]... **)**]**}**  
  
 En la notación BNF, la sintaxis es la siguiente:  
  
 *ODBC-procedure-escape* :: =  
  
 &#124; *ODBC-ESC-Initiator* [? =] Call *procedure ODBC-ESC-Terminator*  
  
 *procedure* :: = *procedure-Name* &#124; *procedure-Name* (*procedure-parameter-list*)  
  
 *procedure-Identifier* :: = *nombre definido por el usuario*  
  
 *procedure-Name* :: = *procedure-Identifier*  
  
 *Nombre del propietario de*&#124;. *procedimiento: identificador*  
  
 &#124; el *identificador de procedimiento* del *separador de catálogos de nombre de catálogo*  
  
 &#124; *el separador de catálogos de nombre de catálogo* [*Owner-Name*]. *procedimiento: identificador*  
  
 (La tercera sintaxis solo es válida si el origen de datos no admite propietarios).  
  
 *Owner-Name* :: = *nombre definido por el usuario*  
  
 *Catalog-Name* :: = *nombre definido por el usuario*  
  
 *el separador de catálogo* :: = {*definido por la implementación*}  
  
 (El separador de catálogo se devuelve a través de **SQLGetInfo** con la opción de información de SQL_CATALOG_NAME_SEPARATOR).  
  
 *procedure-parameter-list* :: = *procedure-parámetro*  
  
 &#124; *procedimiento: Parameter*-Parameter- *List*  
  
 *procedure-Parameter* :: = *parámetro dinámico* &#124; *literal* &#124; *Empty-String*  
  
 *Empty-String* :: =  
  
 *ODBC-ESC-Initiator* :: = {  
  
 *ODBC-ESC-Terminator* :: =}  
  
 (Si un parámetro de procedimiento es una cadena vacía, el procedimiento usa el valor predeterminado para ese parámetro).  
  
 Para determinar si el origen de datos admite procedimientos y el controlador admite la sintaxis de invocación de procedimiento ODBC, una aplicación puede llamar a **SQLGetInfo** con el tipo de información SQL_PROCEDURES.
