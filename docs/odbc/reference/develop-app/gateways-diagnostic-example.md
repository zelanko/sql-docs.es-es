---
title: "Ejemplo de diagnóstico de las puertas de enlace | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- diagnostic information [ODBC], examples
- gateway diagnostic [ODBC]
- error messages [ODBC], diagnostic messages
ms.assetid: e0695fac-4593-4b3d-8675-cb8f73dab966
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f31f5f97bafc7cd53972f83fa39ac10ea2554de5
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="gateways-diagnostic-example"></a>Ejemplo de diagnóstico de las puertas de enlace
En una arquitectura de puerta de enlace, un controlador envía solicitudes a una puerta de enlace que admita ODBC. La puerta de enlace envía las solicitudes a un DBMS. Dado que es el componente que interactúa con el Administrador de controladores, el controlador da formato y devuelve los argumentos para **SQLGetDiagRec**.  
  
 Por ejemplo, si Oracle según una puerta de enlace de Rdb servicios abiertos de datos de Microsoft y si Rdb no encontró la tabla EMPLOYEE, la puerta de enlace puede generar este mensaje de diagnóstico:  
  
```  
"[42S02][-1][DEC][ODS Gateway][Rdb]%SQL-F-RELNOTDEF, Table EMPLOYEE is not defined "  
   "in schema."  
```  
  
 Porque se produjo el error en el origen de datos, la puerta de enlace había agregado un prefijo para el identificador de origen de datos ([Rdb]) para el mensaje de diagnóstico. Dado que la puerta de enlace es el componente de interfaz con el origen de datos, agregar prefijos para su proveedor ([DEC]) e identificador ([ODS puerta de enlace]) para el mensaje de diagnóstico. También agrega el valor SQLSTATE y el código de error de Rdb al principio del mensaje de diagnóstico. Esto permite conservar la semántica de su propia estructura de los mensajes y aún proporcione la información de diagnóstico de ODBC para el controlador. El controlador analiza la información de error asociada a la instrucción de error por la puerta de enlace.  
  
 Dado que el controlador de la puerta de enlace es el componente que interactúa con el Administrador de controladores, utilizaría el mensaje de diagnóstico anterior para dar formato y devolver los valores siguientes de **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1  
Diagnostic Msg:   "[DEC][ODS Gateway][Rdb]%SQL-F-RELNOTDEF, Table EMPLOYEE is not "  
                  "defined in schema."  
```
