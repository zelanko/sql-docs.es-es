---
title: "Ejemplo de diagnóstico de controladores basados en DBMS | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- DBMS-based driver diagnostic [ODBC]
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: a80d54b0-43ff-4dfd-b6cb-f4694a5ed765
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c0a20af8dc2a35ba451890472ad1af73e01d8688
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="dbms-based-driver-diagnostic-example"></a>Ejemplo de diagnóstico de controladores basados en DBMS
Un controlador basados en DBMS envía solicitudes a un DBMS y devuelve información a la aplicación a través del Administrador de controladores. Dado que el controlador es el componente que interactúa con el Administrador de controladores, da formato y devuelve los argumentos para **SQLGetDiagRec**.  
  
 Por ejemplo, si utiliza SQL/servicios, un controlador de Microsoft para Oracle Rdb ha encontrado un nombre de cursor no válido, podrían devolver los siguientes valores de **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "34000"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Rdb Driver]Invalid cursor name: EMPLOYEE_CURSOR."  
```  
  
 Porque se produjo el error en el controlador, agregar los prefijos para el mensaje de diagnóstico para el proveedor ([Microsoft]) y el controlador ([controlador ODBC para Rdb]).  
  
 Si el DBMS no encontró la tabla EMPLOYEE, el controlador podría dar formato y devolver los valores siguientes de **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1  
Diagnostic Msg:   "[Microsoft][ODBC Rdb Driver][Rdb] %SQL-F-RELNOTDEF, Table EMPLOYEE "  
                  "is not defined in schema."  
```  
  
 Porque se produjo el error en el origen de datos, el controlador agrega un prefijo para el identificador de origen de datos ([Rdb]) para el mensaje de diagnóstico. Dado que el controlador es el componente de interfaz con el origen de datos, agrega los prefijos de su proveedor ([Microsoft]) e identificador ([controlador ODBC para Rdb]) para el mensaje de diagnóstico.

