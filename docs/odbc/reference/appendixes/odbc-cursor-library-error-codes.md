---
title: Códigos de error de la biblioteca de cursores ODBC ( ODBC Cursor Library) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c263ce53c41546e63dc2a830d3db3b903e2e3515
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301436"
---
# <a name="odbc-cursor-library-error-codes"></a>Códigos de error de la biblioteca de cursores ODBC
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura del componente de acceso a datos de Microsoft. Evite usar esta característica en el nuevo trabajo de desarrollo y planee modificar las aplicaciones que actualmente utilizan esta característica. En su lugar, utilice cursores de controlador y servidor.  
  
 La biblioteca de cursores ODBC devuelve los siguientes SQLSTATEs además de los enumerados en Referencia de [la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md).  
  
> [!NOTE]  
>  La biblioteca de cursores no ordena registros de estado; el Administrador de controladores y ODBC 3. *x* los controladores son responsables de ordenar los registros de estado.  
  
|SQLSTATE|Descripción|Puede ser devuelto de|  
|--------------|-----------------|--------------------------|  
|01000|El cursor no se puede actualiza.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|01000|No se utiliza la biblioteca de cursores. Error de carga.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|No se utiliza la biblioteca de cursores. Soporte insuficiente del controlador.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|No se utiliza la biblioteca de cursores. No coincidencia de versión con el Administrador de controladores.|**SQLBrowseConnect**<br /><br /> **SQLConnect**<br /><br /> **SQLDriverConnect**|  
|01000|El conductor SQL_SUCCESS_WITH_INFO devolvió. Se ha perdido el mensaje de advertencia.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|S1000|Error general: No se puede crear el búfer de archivos.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|Error general: No se puede leer desde el búfer de archivos.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|Error general: No se puede escribir en el búfer de archivos.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|S1000|Error general: No se puede cerrar o quitar el búfer de archivos.|**SQLFreeHandle**<br /><br /> **SQLFreeStmt**|  
|SL001|La solicitud posicionada no se puede realizar porque no se enlaza ninguna columna que se pueda buscar.|**SQLExecDirect**<br /><br /> **SQLGetData**<br /><br /> **SQLPrepare**|  
|SL002|No se pudo realizar la solicitud posicionada porque el conjunto de resultados se creó mediante una condición de combinación.|**SQLExecute**<br /><br /> **SQLExecDirect**<br /><br /> **SQLGetData**|  
|SL003|El búfer enlazado supera el tamaño máximo del segmento.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|SL004|El conjunto de resultados no se generó mediante una instrucción **SELECT.**|**SQLGetData**|  
|SL005|**La** instrucción SELECT contiene una cláusula GROUP BY.|**SQLGetData**|  
|SL006|Las matrices de parámetros no se admiten con solicitudes posicionadas.|**SQLPrepare**<br /><br /> **SQLExecDirect**|  
|SL008|**SQLGetData** no se permite en un cursor de solo avance (sin búfer).|**SQLGetData**|  
|SL009|No se enlazaba ninguna columna antes de llamar a **SQLFetch** o **SQLFetchScroll**.|**SQLFetch**<br /><br /> **SQLFetchScroll**|  
|SL010|**SQLBindCol** devuelto SQL_ERROR durante un intento de enlazar a un búfer interno.|**SQLFetch**<br /><br /> **SQLFetchScroll**<br /><br /> **SQLGetData**|  
|SL011|La opción de instrucción solo es válida después de llamar a **SQLFetch** o **SQLFetchScroll**.|**SQLGetStmtAttr**|  
|SL012|Los enlaces de instrucción no se pueden cambiar mientras un cursor está abierto.|**SQLBindCol**<br /><br /> **SQLFreeHandle**<br /><br /> **SQLFreeStmt**<br /><br /> **SQLSetStmtAttr**|  
|SL014|Se emitió una solicitud posicionada y no se almacenaron en búfer todos los campos de recuento de columnas.|**SQLExecDirect**<br /><br /> **SQLExecute**<br /><br /> **SQLPrepare**|  
|SL015|**SQLFetch** y **SQLFetchScroll** no se pueden mezclar.|**SQLExtendedFetch**<br /><br /> **SQLFetch**<br /><br /> **SQLFetchScroll**|
