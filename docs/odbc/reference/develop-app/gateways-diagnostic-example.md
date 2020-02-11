---
title: Ejemplo de diagnóstico de puertas de enlace | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], examples
- gateway diagnostic [ODBC]
- error messages [ODBC], diagnostic messages
ms.assetid: e0695fac-4593-4b3d-8675-cb8f73dab966
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 50476cb92d477bb9a72ac8d4311d24572b0368e9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68069683"
---
# <a name="gateways-diagnostic-example"></a>Ejemplo de diagnóstico de las puertas de enlace
En una arquitectura de puerta de enlace, un controlador envía las solicitudes a una puerta de enlace compatible con ODBC. La puerta de enlace envía las solicitudes a un DBMS. Dado que es el componente que interactúa con el administrador de controladores, el controlador da formato y devuelve argumentos para **SQLGetDiagRec**.  
  
 Por ejemplo, si Oracle basa una puerta de enlace a RDB en Microsoft Open Data Services y si RDB no encuentra la tabla EMPLOYEe, la puerta de enlace podría generar este mensaje de diagnóstico:  
  
```  
"[42S02][-1][DEC][ODS Gateway][Rdb]%SQL-F-RELNOTDEF, Table EMPLOYEE is not defined "  
   "in schema."  
```  
  
 Dado que el error se produjo en el origen de datos, la puerta de enlace agregó un prefijo para el identificador de origen de datos ([RDB]) al mensaje de diagnóstico. Dado que la puerta de enlace era el componente que se intercesó con el origen de datos, agregó prefijos para su proveedor ([DEC]) e identificador ([puerta de enlace de ODS]) al mensaje de diagnóstico. También agregó el valor SQLSTATE y el código de error RDB al principio del mensaje de diagnóstico. Esto permitió conservar la semántica de su propia estructura de mensajes y seguir proporcionando la información de diagnóstico de ODBC al controlador. El controlador analiza la información de error adjunta a la instrucción de error por la puerta de enlace.  
  
 Dado que el controlador de puerta de enlace es el componente que interactúa con el administrador de controladores, usaría el mensaje de diagnóstico anterior para dar formato y devolver los valores siguientes de **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1  
Diagnostic Msg:   "[DEC][ODS Gateway][Rdb]%SQL-F-RELNOTDEF, Table EMPLOYEE is not "  
                  "defined in schema."  
```
