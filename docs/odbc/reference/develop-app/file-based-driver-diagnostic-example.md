---
title: Ejemplo de diagnóstico de controlador basados en archivos | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: decb09098cee4b9ab6473e3c622b9917a89e9b09
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63061534"
---
# <a name="file-based-driver-diagnostic-example"></a>Ejemplo de diagnóstico de controlador basados en archivos
Un controlador basado en archivos actúa como un controlador ODBC y como un origen de datos. Por lo tanto, puede generar errores y advertencias tanto como un componente en una conexión ODBC y como un origen de datos. Dado que también es el componente que interactúa con el Administrador de controladores, da formato y devuelve los argumentos para **SQLGetDiagRec**.  
  
 Por ejemplo, si un controlador Microsoft® para dBASE no pudo asignar suficiente memoria, podría devolver los valores siguientes de **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "HY001"  
Native Error:      42052  
Diagnostic Msg:   "[Microsoft][ODBC dBASE Driver]Unable to allocate sufficient memory."  
```  
  
 Porque este error no estaba relacionada con el origen de datos, el controlador agrega solo los prefijos para el mensaje de diagnóstico para el proveedor ([Microsoft]) y el controlador ([ODBC dBASE controlador]).  
  
 Si el controlador no pudo encontrar el archivo Employee.dbf, podría devolver los valores siguientes de **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1305  
Diagnostic Msg:   "[Microsoft][ODBC dBASE Driver][dBASE]No such table or object"  
```  
  
 Dado que este error se ha relacionado con el origen de datos, el controlador agrega el formato de archivo del origen de datos ([dBASE]) como prefijo para el mensaje de diagnóstico. Debido a que el controlador también era el componente que se relacionó con el origen de datos, agregar los prefijos de proveedor ([Microsoft]) y el controlador ([ODBC dBASE controlador]).
