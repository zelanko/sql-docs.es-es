---
title: Secuencia de escape de llamada de procedimiento ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1194efe6a21c456a722ccd4352661c998f0316d9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298225"
---
# <a name="procedure-call-escape-sequence"></a>Secuencia de Escape de llamada de procedimiento
ODBC usa secuencias de escape para las llamadas a procedimientos. La sintaxis de esta secuencia de escape es la siguiente:  
  
 **•** *nombre-procedimiento*de**llamada** [**(***[ parámetro*][,[*parámetro*]]... **)**]**}**  
  
 En la notación BNF, la sintaxis es la siguiente:  
  
 *ODBC-procedimiento-escape* ::  
  
 &#124; *odbc-esc-iniciador* [?-] llama al *procedimiento ODBC-esc-terminator*  
  
 *procedimiento* ::- *nombre-procedimiento* &#124; *nombre-procedimiento* *(procedimiento-parámetro-lista*)  
  
 *procedimiento-identificador* ::- *nombre definido por* el usuario  
  
 *nombre-procedimiento* ::- *identificador de procedimiento*  
  
 &#124; *nombre-propietario*. *procedimiento-identificador*  
  
 &#124; *identificador de procedimiento* de separador de catálogo de nombre de *catálogo*  
  
 &#124; *catalog-name catalog-separator* [*owner-name*]. *procedimiento-identificador*  
  
 (La tercera sintaxis solo es válida si el origen de datos no admite propietarios.)  
  
 *nombre-propietario* ::- *nombre definido por el usuario*  
  
 *nombre-catálogo* ::- *nombre definido por* el usuario  
  
 *separador de catálogos* ::- -*definido por la implementación*?  
  
 (El separador de catálogo se devuelve a través de **SQLGetInfo** con la opción de información SQL_CATALOG_NAME_SEPARATOR.)  
  
 *procedimiento-parámetro-lista* ::- *parámetro-procedimiento*  
  
 &#124; *parámetro de procedimiento*, *procedimiento-parámetro-lista*  
  
 *parámetro-procedimiento* ::- *parámetro dinámico* &#124; *literal* &#124; *cadena vacía*  
  
 *cadena vacía* ::  
  
 *ODBC-esc-iniciador* ::-  
  
 *ODBC-esc-terminator* ::-  
  
 (Si un parámetro de procedimiento es una cadena vacía, el procedimiento utiliza el valor predeterminado para ese parámetro.)  
  
 Para determinar si el origen de datos admite procedimientos y el controlador admite la sintaxis de invocación de procedimiento ODBC, una aplicación puede llamar a **SQLGetInfo** con el tipo de información SQL_PROCEDURES.
