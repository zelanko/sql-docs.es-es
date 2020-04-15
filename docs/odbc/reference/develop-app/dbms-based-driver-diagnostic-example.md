---
title: Ejemplo de diagnóstico de controladores basados en DBMS ( DBMS-Based Driver Diagnostic Example ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DBMS-based driver diagnostic [ODBC]
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: a80d54b0-43ff-4dfd-b6cb-f4694a5ed765
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 117f43548d2b57233dea6f7423e6bad67b6233b0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304356"
---
# <a name="dbms-based-driver-diagnostic-example"></a>Ejemplo de diagnóstico de controladores basados en DBMS
Un controlador basado en DBMS envía solicitudes a un DBMS y devuelve información a la aplicación a través del Administrador de controladores. Dado que el controlador es el componente que interactúa con el Administrador de controladores, da formato y devuelve argumentos para **SQLGetDiagRec**.  
  
 Por ejemplo, si, mediante SQL/Services, un controlador de Microsoft para Oracle Rdb encuentra un nombre de cursor no válido, podría devolver los siguientes valores de **SQLGetDiagRec:**  
  
```  
SQLSTATE:         "34000"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Rdb Driver]Invalid cursor name: EMPLOYEE_CURSOR."  
```  
  
 Dado que el error se produjo en el controlador, agregó prefijos al mensaje de diagnóstico para el proveedor ([Microsoft]) y el controlador ([CONTROLADOR Rdb ODBC]).  
  
 Si el DBMS no pudo encontrar la tabla EMPLOYEE, el controlador podría dar formato y devolver los siguientes valores de **SQLGetDiagRec:**  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1  
Diagnostic Msg:   "[Microsoft][ODBC Rdb Driver][Rdb] %SQL-F-RELNOTDEF, Table EMPLOYEE "  
                  "is not defined in schema."  
```  
  
 Dado que el error se produjo en el origen de datos, el controlador agregó un prefijo para el identificador del origen de datos ([Rdb]) al mensaje de diagnóstico. Dado que el controlador era el componente que interconectaba con el origen de datos, agregaba prefijos para su proveedor ([Microsoft]) e identificador ([CONTROLADOR Rdb ODBC]) al mensaje de diagnóstico.
