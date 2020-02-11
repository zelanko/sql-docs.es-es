---
title: Ejemplo de diagnóstico de controladores basados en DBMS | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ef42fe2ab881a7e24d680e0dd941cbea0d95488f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68076894"
---
# <a name="dbms-based-driver-diagnostic-example"></a>Ejemplo de diagnóstico de controladores basados en DBMS
Los controladores basados en DBMS envían solicitudes a un DBMS y devuelven información a la aplicación a través del administrador de controladores. Dado que el controlador es el componente que interactúa con el administrador de controladores, da formato y devuelve los argumentos de **SQLGetDiagRec**.  
  
 Por ejemplo, si usa SQL/Services, un controlador de Microsoft para Oracle Rdb encontró un nombre de cursor no válido, podría devolver los valores siguientes de **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "34000"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Rdb Driver]Invalid cursor name: EMPLOYEE_CURSOR."  
```  
  
 Debido a que el error se produjo en el controlador, se han agregado prefijos al mensaje de diagnóstico para el proveedor ([Microsoft]) y el controlador ([ODBC RDB driver]).  
  
 Si el DBMS no encontró la tabla EMPLOYEe, el controlador podría dar formato y devolver los valores siguientes de **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1  
Diagnostic Msg:   "[Microsoft][ODBC Rdb Driver][Rdb] %SQL-F-RELNOTDEF, Table EMPLOYEE "  
                  "is not defined in schema."  
```  
  
 Dado que el error se produjo en el origen de datos, el controlador agregó un prefijo para el identificador de origen de datos ([RDB]) al mensaje de diagnóstico. Dado que el controlador era el componente que se intercesó con el origen de datos, agregó prefijos para su proveedor ([Microsoft]) e identificador ([ODBC RDB driver]) al mensaje de diagnóstico.
