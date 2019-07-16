---
title: Códigos de Error de biblioteca de cursores ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursor library [ODBC], error codes
- error codes [ODBC], cursor library
- ODBC cursor library [ODBC], error codes
ms.assetid: 9713480e-8744-4f37-a630-20871590d4a1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a3fb86e1332e3b7e4d89003ccf6421151e5d9cec
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68100667"
---
# <a name="odbc-cursor-library-error-codes"></a>Códigos de error de la biblioteca de cursores ODBC
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Microsoft Data Access Components. Evite usar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. En su lugar, utilice los cursores de servidor y el controlador.  
  
 La biblioteca de cursores ODBC devuelve el siguientes SQLSTATEs además de los enumerados en [referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md).  
  
> [!NOTE]  
>  La biblioteca de cursores no ordena los registros de estado; el Administrador de controladores y ODBC 3. *x* controladores son responsables de registros de estado de ordenación.  
  
|SQLSTATE|Descripción|Pueden devolverse desde|  
|--------------|-----------------|--------------------------|  
|01000|Cursor no es actualizable.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|01000|No utilizada la biblioteca de cursores. Error de carga.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|No utilizada la biblioteca de cursores. Soporte de controlador insuficiente.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|No utilizada la biblioteca de cursores. Discrepancia de versiones con el Administrador de controladores.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|Controlador devuelve SQL_SUCCESS_WITH_INFO. Se ha perdido el mensaje de advertencia.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|S1000|Error general: No se puede crear el búfer de archivo.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|Error general: No se puede leer desde el búfer de archivo.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|Error general: No se puede escribir en el búfer de archivo.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|Error general: No se puede cerrar o eliminar el búfer de archivo.|**SQLFreeHandle**<br /><br /> **SQLFreeStmt**|  
|SL001|Solicitud posicionada no se puede realizar porque no hay columnas de búsqueda se enlazaron.|**SQLExecDirect**<br /><br /> **SQLGetData**<br /><br /> **SQLPrepare**|  
|SL002|No se pudo realizar la solicitud posicionada porque se creó el conjunto de resultados por una condición de combinación.|**SQLExecute**<br /><br /> **SQLExecDirect**<br /><br /> **SQLGetData**|  
|SL003|Dependiente búfer supera el tamaño máximo de segmento.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|SL004|No se generó el conjunto de resultados por un **seleccione** instrucción.|**SQLGetData**|  
|SL005|**Seleccione** instrucción contiene una cláusula GROUP BY.|**SQLGetData**|  
|SL006|No se admiten las matrices de parámetros con las solicitudes de posición.|**SQLPrepare**<br /><br /> **SQLExecDirect**|  
|SL008|**SQLGetData** no se permite en un cursor de solo avance (sin almacenamiento en búfer).|**SQLGetData**|  
|SL009|No se enlazaron columnas antes de llamar a **SQLFetch** o **SQLFetchScroll**.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|SL010|**SQLBindCol** devuelve SQL_ERROR durante un intento de enlazar a un búfer interno.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|SL011|La opción de instrucción es válida sólo después de llamar a **SQLFetch** o **SQLFetchScroll**.|**SQLGetStmtAttr**|  
|SL012|Enlaces de instrucción no se pueden cambiar mientras el cursor está abierto.|**SQLBindCol**<br /><br /> **SQLFreeHandle**<br /><br /> **SQLFreeStmt**<br /><br /> **SQLSetStmtAttr**|  
|SL014|Se ha emitido una solicitud de posición y no todos los campos de número de columna se almacenan en búfer.|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLPrepare**|  
|SL015|**SQLFetch** y **SQLFetchScroll** no se pueden mezclar.|**SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**|
