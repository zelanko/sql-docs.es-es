---
title: Ejemplo de diagnóstico de controladorbasado en archivos ( File-Based Driver Diagnostic Example ? Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305643"
---
# <a name="file-based-driver-diagnostic-example"></a>Ejemplo de diagnóstico de controlador basados en archivos
Un controlador basado en archivos actúa como un controlador ODBC y como un origen de datos. Por lo tanto, puede generar errores y advertencias como un componente en una conexión ODBC y como un origen de datos. Dado que también es el componente que interactúa con el Administrador de controladores, da formato y devuelve argumentos para **SQLGetDiagRec**.  
  
 Por ejemplo, si un controlador de Microsoft® para dBASE no pudo asignar suficiente memoria, podría devolver los siguientes valores de **SQLGetDiagRec:**  
  
```  
SQLSTATE:         "HY001"  
Native Error:      42052  
Diagnostic Msg:   "[Microsoft][ODBC dBASE Driver]Unable to allocate sufficient memory."  
```  
  
 Dado que este error no estaba relacionado con el origen de datos, el controlador solo agregó prefijos al mensaje de diagnóstico para el proveedor ([Microsoft]) y el controlador ([CONTROLADOR ODBC dBASE]).  
  
 Si el controlador no pudo encontrar el archivo Employee.dbf, podría devolver los siguientes valores de **SQLGetDiagRec:**  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1305  
Diagnostic Msg:   "[Microsoft][ODBC dBASE Driver][dBASE]No such table or object"  
```  
  
 Dado que este error estaba relacionado con el origen de datos, el controlador agregó el formato de archivo del origen de datos ([dBASE]) como prefijo para el mensaje de diagnóstico. Dado que el controlador también era el componente que interconectaba con el origen de datos, agregaba prefijos para el proveedor ([Microsoft]) y el controlador ([ODBC dBASE Driver]).
