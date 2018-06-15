---
title: Códigos de Error de biblioteca de cursores ODBC | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- cursor library [ODBC], error codes
- error codes [ODBC], cursor library
- ODBC cursor library [ODBC], error codes
ms.assetid: 9713480e-8744-4f37-a630-20871590d4a1
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 26469f2d439c032b1d4f5f377cc9aab4a4189fae
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32913910"
---
# <a name="odbc-cursor-library-error-codes"></a>Códigos de Error de biblioteca de cursores ODBC
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Microsoft Data Access Components. Evite utilizar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. En su lugar, utilice los cursores de servidor y el controlador.  
  
 La biblioteca de cursores ODBC devuelve el siguiente SQLSTATE además de los enumerados en [referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md).  
  
> [!NOTE]  
>  La biblioteca de cursores no ordena los registros de estado; el Administrador de controladores y ODBC 3. *x* controladores están responsables de ordenar los registros de estado.  
  
|SQLSTATE|Description|Se puede devolver desde|  
|--------------|-----------------|--------------------------|  
|01000|Cursor no es actualizable.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|01000|No utiliza la biblioteca de cursores. No se pudo cargar.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|No utiliza la biblioteca de cursores. Soporte de controlador insuficiente.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|No utiliza la biblioteca de cursores. Discrepancia de versiones con el Administrador de controladores.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|Controlador devuelve SQL_SUCCESS_WITH_INFO. Se ha perdido el mensaje de advertencia.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|S1000|Error general: no se puede crear el búfer de archivos.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|Error general: no se puede leer desde el búfer de archivos.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|Error general: no se puede escribir en el búfer del archivo.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|Error general: no se puede cerrar o quitar el búfer de archivos.|**SQLFreeHandle**<br /><br /> **SQLFreeStmt**|  
|SL001|La petición ubicada no se puede realizar porque no hay columnas de búsqueda se enlazaron.|**SQLExecDirect**<br /><br /> **SQLGetData**<br /><br /> **SQLPrepare**|  
|SL002|La petición ubicada no se pudo realizar porque se creó el conjunto de resultados por una condición de combinación.|**SQLExecute**<br /><br /> **SQLExecDirect**<br /><br /> **SQLGetData**|  
|SL003|Dependiente búfer supera el tamaño máximo de segmento.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|SL004|Conjunto de resultados no fue generado por una **seleccione** instrucción.|**SQLGetData**|  
|SL005|**Seleccione** instrucción contiene una cláusula GROUP BY.|**SQLGetData**|  
|SL006|Matrices de parámetros no se admiten las peticiones posicionadas.|**SQLPrepare**<br /><br /> **SQLExecDirect**|  
|SL008|**SQLGetData** no está permitida en un cursor de solo avance (sin almacenamiento en búfer).|**SQLGetData**|  
|SL009|No se enlazaron columnas antes de llamar a **SQLFetch** o **SQLFetchScroll**.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|SL010|**SQLBindCol** devuelve SQL_ERROR durante un intento de enlazar a un búfer interno.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|SL011|Opción de instrucción es válida sólo después de llamar a **SQLFetch** o **SQLFetchScroll**.|**SQLGetStmtAttr**|  
|SL012|Enlaces de instrucción no se pueden cambiar mientras el cursor está abierto.|**SQLBindCol**<br /><br /> **SQLFreeHandle**<br /><br /> **SQLFreeStmt**<br /><br /> **SQLSetStmtAttr**|  
|SL014|Se emitió una petición posicionada y no todos los campos de número de columna se almacena en búfer.|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLPrepare**|  
|SL015|**SQLFetch** y **SQLFetchScroll** no se pueden mezclar.|**SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**|
