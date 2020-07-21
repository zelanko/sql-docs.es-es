---
title: Matriz de estado de fila | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- row status array [ODBC]
- cursors [ODBC], block
- result sets [ODBC], row status array
- block cursors [ODBC]
- result sets [ODBC], block cursors
- rowset status [ODBC]
ms.assetid: 4b69f189-2722-4314-8a02-f4ffecd6dabd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 60dead23fe0051c05698e094f37ddad96b2b337d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304296"
---
# <a name="row-status-array"></a>Matriz de Estados de fila
Además de los datos, **SQLFetch** y **SQLFetchScroll** pueden devolver una matriz que proporciona el estado de cada fila del conjunto de filas. Esta matriz se especifica mediante el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR. La aplicación asigna esta matriz y debe tener tantos elementos como especifique el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE. Los valores de la matriz se establecen mediante **SQLBulkOperations**, **SQLFetch**, **SQLFetchScroll**y **SQLSetPos.** Los valores describen el estado de la fila y si el estado ha cambiado desde que se capturó por última vez.  
  
|Valor de la matriz de estado de fila|Descripción|  
|----------------------------|-----------------|  
|SQL_ROW_SUCCESS|La fila se ha recuperado correctamente y no ha cambiado desde que se capturó por última vez.|  
|SQL_ROW_SUCCESS_WITH_INFO|La fila se ha recuperado correctamente y no ha cambiado desde que se capturó por última vez. Sin embargo, se devolvió una advertencia sobre la fila.|  
|SQL_ROW_ERROR|Se produjo un error al capturar la fila.|  
|SQL_ROW_UPDATED|La fila se ha recuperado correctamente y se ha actualizado desde que se capturó por última vez. Si la fila se recupera de nuevo o se actualiza mediante **SQLSetPos**, su estado cambia al nuevo estado.<br /><br /> Algunos controladores no pueden detectar cambios en los datos y, por lo tanto, no pueden devolver este valor. Para determinar si un controlador puede detectar actualizaciones de filas recuperadas, una aplicación llama a **SQLGetInfo** con la opción SQL_ROW_UPDATES.|  
|SQL_ROW_DELETED|La fila se ha eliminado desde la última vez que se recuperó.|  
|SQL_ROW_ADDED|**SQLBulkOperations**insertó la fila. Si la fila se recupera de nuevo o se actualiza mediante **SQLSetPos**, su estado es SQL_ROW_SUCCESS.<br /><br /> **SQLFetch** o **SQLFetchScroll**no establece este valor.|  
|SQL_ROW_NOROW|El conjunto de filas se superpone al final del conjunto de resultados y no se devolvió ninguna fila que corresponda a este elemento de la matriz de estado de fila.|
