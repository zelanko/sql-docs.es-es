---
title: Ejemplo de diagnóstico de las puertas de enlace | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 5f4e17074616111ee93ce87c04036d1fc3fd48dd
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47607854"
---
# <a name="gateways-diagnostic-example"></a>Ejemplo de diagnóstico de las puertas de enlace
En una arquitectura de puerta de enlace, un controlador envía solicitudes a una puerta de enlace que admite ODBC. La puerta de enlace envía las solicitudes a un DBMS. Dado que es el componente que interactúa con el Administrador de controladores, el controlador da formato y devuelve los argumentos para **SQLGetDiagRec**.  
  
 Por ejemplo, si Oracle según una puerta de enlace de Rdb servicios abiertos de datos de Microsoft y si Rdb no encontró la tabla EMPLOYEE, la puerta de enlace puede generar este mensaje de diagnóstico:  
  
```  
"[42S02][-1][DEC][ODS Gateway][Rdb]%SQL-F-RELNOTDEF, Table EMPLOYEE is not defined "  
   "in schema."  
```  
  
 Porque se produjo el error en el origen de datos, la puerta de enlace agrega un prefijo para el identificador de origen de datos ([Rdb]) para el mensaje de diagnóstico. Debido a que la puerta de enlace era el componente que se relacionó con el origen de datos, agregar los prefijos de su proveedor ([DEC]) e identificador ([ODS puerta de enlace]) para el mensaje de diagnóstico. También agrega el valor SQLSTATE y el código de error de Rdb al principio del mensaje de diagnóstico. Esto permite conservar la semántica de su propia estructura de mensaje y todavía proporcionar la información de diagnóstico ODBC con el controlador. El controlador analiza la información de error asociada a la instrucción de error por la puerta de enlace.  
  
 Dado que el controlador de la puerta de enlace es el componente que interactúa con el Administrador de controladores, usaría el mensaje de diagnóstico anterior para dar formato y devolver los valores siguientes de **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1  
Diagnostic Msg:   "[DEC][ODS Gateway][Rdb]%SQL-F-RELNOTDEF, Table EMPLOYEE is not "  
                  "defined in schema."  
```
