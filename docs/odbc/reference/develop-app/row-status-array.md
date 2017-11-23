---
title: Matriz de Estados de fila | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- row status array [ODBC]
- cursors [ODBC], block
- result sets [ODBC], row status array
- block cursors [ODBC]
- result sets [ODBC], block cursors
- rowset status [ODBC]
ms.assetid: 4b69f189-2722-4314-8a02-f4ffecd6dabd
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f4451ccb74ca19a02c352c2e7361d0ec8e84c87d
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="row-status-array"></a>Matriz de Estados de fila
Además de los datos, **SQLFetch** y **SQLFetchScroll** puede devolver una matriz que proporciona el estado de cada fila del conjunto de filas. Esta matriz se especifica mediante el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR. Esta matriz asignada por la aplicación y debe tener tantos elementos como se especifican mediante el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE. Los valores de la matriz se establecen **SQLBulkOperations**, **SQLFetch**, **SQLFetchScroll**, y **SQLSetPos.** Los valores describen el estado de la fila y si ese estado ha cambiado desde que se capturó en último lugar.  
  
|Valor de matriz de estado de fila|Description|  
|----------------------------|-----------------|  
|SQL_ROW_SUCCESS|La fila se ha obtenido correctamente y no ha cambiado desde que se capturó en último lugar.|  
|SQL_ROW_SUCCESS_WITH_INFO|La fila se ha obtenido correctamente y no ha cambiado desde que se capturó en último lugar. Sin embargo, se devuelve una advertencia acerca de la fila.|  
|SQL_ROW_ERROR|Se produjo un error al capturar la fila.|  
|SQL_ROW_UPDATED|La fila se ha obtenido correctamente y se ha actualizado desde que se capturó en último lugar. Si la fila se recopila de nuevo o actualizada en **SQLSetPos**, su estado se cambia para el nuevo estado.<br /><br /> Algunos controladores no pueden detectar cambios en los datos y, por tanto, no pueden devolver este valor. Para determinar si un controlador puede detectar las actualizaciones para volver a capturar filas, llama a una aplicación **SQLGetInfo** con la opción SQL_ROW_UPDATES.|  
|SQL_ROW_DELETED|Se ha eliminado la fila se capturó en último lugar.|  
|SQL_ROW_ADDED|La fila se ha insertado por **SQLBulkOperations**. Si la fila se vuelve a recopilar o se actualiza de forma **SQLSetPos**, su estado es SQL_ROW_SUCCESS.<br /><br /> Este valor no se establece **SQLFetch** o **SQLFetchScroll**.|  
|SQL_ROW_NOROW|El conjunto de filas había superpuesta al final del conjunto de resultados y se devuelve ninguna fila que correspondía a este elemento de la matriz de estado de fila.|
