---
title: Ejemplo de diagnóstico de puertas de enlace ( Gateways) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b18fd78be7be2eb79316339cbdf3d315deb194fb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305576"
---
# <a name="gateways-diagnostic-example"></a>Ejemplo de diagnóstico de las puertas de enlace
En una arquitectura de puerta de enlace, un controlador envía solicitudes a una puerta de enlace que admite ODBC. La puerta de enlace envía las solicitudes a un DBMS. Dado que es el componente que interactúa con el Administrador de controladores, el controlador da formato y devuelve argumentos para **SQLGetDiagRec**.  
  
 Por ejemplo, si Oracle basó una puerta de enlace a Rdb en Microsoft Open Data Services y si Rdb no pudo encontrar la tabla EMPLOYEE, la puerta de enlace podría generar este mensaje de diagnóstico:  
  
```  
"[42S02][-1][DEC][ODS Gateway][Rdb]%SQL-F-RELNOTDEF, Table EMPLOYEE is not defined "  
   "in schema."  
```  
  
 Dado que el error se produjo en el origen de datos, la puerta de enlace agregó un prefijo para el identificador del origen de datos ([Rdb]) al mensaje de diagnóstico. Dado que la puerta de enlace era el componente que interconectaba con el origen de datos, agregó prefijos para su proveedor ([DEC]) e identificador ([Puerta de enlace de ODS]) al mensaje de diagnóstico. También agregó el valor SQLSTATE y el código de error Rdb al principio del mensaje de diagnóstico. Esto le permitió conservar la semántica de su propia estructura de mensajes y seguir proporcionando la información de diagnóstico ODBC al controlador. El controlador analiza la información de error adjunta a la instrucción de error por la puerta de enlace.  
  
 Dado que el controlador de puerta de enlace es el componente que interactúa con el Administrador de controladores, usaría el mensaje de diagnóstico anterior para dar formato y devolver los siguientes valores de **SQLGetDiagRec:**  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1  
Diagnostic Msg:   "[DEC][ODS Gateway][Rdb]%SQL-F-RELNOTDEF, Table EMPLOYEE is not "  
                  "defined in schema."  
```
