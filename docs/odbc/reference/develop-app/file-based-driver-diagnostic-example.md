---
title: Ejemplo de diagnóstico de controladores basados en archivos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- file-based driver diagnostic [ODBC]
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: 0575fccd-4641-478d-a3cc-5a764e35bae2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6f09e4f4758b6276836b08f02b24fb31dd1fadc7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305643"
---
# <a name="file-based-driver-diagnostic-example"></a>Ejemplo de diagnóstico de controlador basados en archivos
Un controlador basado en archivos actúa como un controlador ODBC y como un origen de datos. Por lo tanto, puede generar errores y advertencias como un componente de una conexión ODBC y como un origen de datos. Dado que también es el componente que interactúa con el administrador de controladores, da formato y devuelve los argumentos de **SQLGetDiagRec**.  
  
 Por ejemplo, si un controlador de Microsoft® para dBASE no pudo asignar memoria suficiente, podría devolver los valores siguientes de **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "HY001"  
Native Error:      42052  
Diagnostic Msg:   "[Microsoft][ODBC dBASE Driver]Unable to allocate sufficient memory."  
```  
  
 Dado que este error no está relacionado con el origen de datos, el controlador solo agregó prefijos al mensaje de diagnóstico para el proveedor ([Microsoft]) y el controlador ([ODBC dBASE driver]).  
  
 Si el controlador no pudo encontrar el archivo Employee. DBF, podría devolver los valores siguientes de **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1305  
Diagnostic Msg:   "[Microsoft][ODBC dBASE Driver][dBASE]No such table or object"  
```  
  
 Dado que este error estaba relacionado con el origen de datos, el controlador agregó el formato de archivo del origen de datos ([dBASE]) como prefijo del mensaje de diagnóstico. Dado que el controlador también era el componente que se intercesó con el origen de datos, agregó prefijos para el proveedor ([Microsoft]) y el controlador ([ODBC dBASE driver]).
