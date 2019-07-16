---
title: Matriz de Estados de fila | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 57b187bf4f14bd5c05f91a433fa331e954fa0fb9
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020371"
---
# <a name="row-status-array"></a>Matriz de Estados de fila
Además de los datos, **SQLFetch** y **SQLFetchScroll** puede devolver una matriz que muestra el estado de cada fila del conjunto de filas. Esta matriz se especifica mediante el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR. Esta matriz se asigna por la aplicación y debe tener tantos elementos como se especifican mediante el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE. Los valores de la matriz se establecen **SQLBulkOperations**, **SQLFetch**, **SQLFetchScroll**, y **SQLSetPos.** Los valores describen el estado de la fila y si ese estado ha cambiado desde que se capturó por última vez.  
  
|Valor de matriz de estado de fila|Descripción|  
|----------------------------|-----------------|  
|SQL_ROW_SUCCESS|La fila se capturó correctamente y no ha cambiado desde que se capturó en último lugar.|  
|SQL_ROW_SUCCESS_WITH_INFO|La fila se capturó correctamente y no ha cambiado desde que se capturó en último lugar. Sin embargo, se devuelve una advertencia acerca de la fila.|  
|SQL_ROW_ERROR|Se produjo un error al capturar la fila.|  
|SQL_ROW_UPDATED|La fila se capturó correctamente y se ha actualizado desde que se capturó en último lugar. Si la fila se recopila de nuevo o actualizada en **SQLSetPos**, su estado se cambia el estado nueva.<br /><br /> Algunos controladores no pueden detectar cambios en los datos y, por tanto, no pueden devolver este valor. Para determinar si un controlador puede detectar las actualizaciones para volver a capturar filas, una aplicación llama a **SQLGetInfo** con la opción SQL_ROW_UPDATES.|  
|SQL_ROW_DELETED|Se eliminó la fila se capturó en último lugar.|  
|SQL_ROW_ADDED|La fila se insertó por **SQLBulkOperations**. Si la fila se vuelve a recopilar o se actualiza de forma **SQLSetPos**, su estado es SQL_ROW_SUCCESS.<br /><br /> No se establece este valor **SQLFetch** o **SQLFetchScroll**.|  
|SQL_ROW_NOROW|El conjunto de filas había superpuesto al final del conjunto de resultados y no se devolvió ninguna fila que correspondía a este elemento de la matriz de Estados de fila.|
