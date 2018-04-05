---
title: Parámetros de procedimiento | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- procedure parameters [ODBC]
ms.assetid: 54fd857e-d2cb-467d-bb72-121e67a8e88d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ea30d30d66761e245a89fadd4bea37d6503c458b
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="procedure-parameters"></a>Parámetros de procedimiento
Los parámetros en las llamadas a procedimiento pueden usar como entrados, entrada/salida o parámetros de salida. Esto es diferente de parámetros en las demás instrucciones SQL, que siempre son parámetros de entrada.  
  
 Parámetros de entrada se utilizan para enviar los valores para el procedimiento. Por ejemplo, suponga que la tabla Parts tiene columnas PartID, descripción y el precio. El procedimiento InsertPart podría tener un parámetro de entrada para cada columna en la tabla. Por ejemplo:  
  
```  
{call InsertPart(?, ?, ?)}  
```  
  
 Un controlador no debe modificar el contenido de un búfer de entrada hasta **SQLExecDirect** o **SQLExecute** devuelve SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE o SQL_NO_DATA. No se debe modificar el contenido del búfer de entrada mientras **SQLExecDirect** o **SQLExecute** devuelve SQL_NEED_DATA o SQL_STILL_EXECUTING.  
  
 Parámetros de entrada/salida se usan para enviar valores a los procedimientos y recuperar los valores de los procedimientos. Con el mismo parámetro como entrada y un parámetro de salida tiende a ser confuso y debe evitarse. Por ejemplo, suponga que un procedimiento acepta un identificador de pedido y devuelve el identificador del cliente. Esto se puede definir con un solo parámetro de entrada/salida:  
  
```  
{call GetCustID(?)}  
```  
  
 Puede que sea mejor usar dos parámetros: un parámetro de entrada para el identificador de pedido y un parámetro de entrada/salida para el identificador de cliente o salida:  
  
```  
{call GetCustID(?, ?)}  
```  
  
 Parámetros de salida se utilizan para recuperar el valor devuelto del procedimiento y para recuperar valores de argumentos de procedimiento; los procedimientos que devuelven valores se conocen a veces como *funciones*. Por ejemplo, suponga que la **GetCustID** acaban de mencionar el procedimiento devuelve un valor que indica si se puede encontrar el pedido. En la siguiente llamada, el primer parámetro es un parámetro de salida que se usa para recuperar el valor devuelto del procedimiento, el segundo parámetro es un parámetro de entrada que se utiliza para especificar el identificador de pedido y el tercer parámetro es un parámetro de salida que se usa para recuperar el identificador de cliente:  
  
```  
{? = call GetCustID(?, ?)}  
```  
  
 Controladores de tratar los valores de entrada y entrada/salida los parámetros de procedimientos no forma diferente a los parámetros de entrada en otras instrucciones SQL. Cuando se ejecuta la instrucción, recuperan los valores de las variables enlazadas a estos parámetros y enviarlos al origen de datos.  
  
 Una vez ejecutada la instrucción, controladores de almacenarán los valores devueltos de entrada/salida y los parámetros de salida en las variables enlazadas a esos parámetros. Estos devuelven valores no se garantizan que se establezca hasta después de que todos los resultados devueltos por el procedimiento que se han capturado y **SQLMoreResults** devuelva SQL_NO_DATA. Si se ejecuta la instrucción produce un error, el contenido del búfer de parámetro de entrada/salida o búfer del parámetro de salida es indefinido.  
  
 Una aplicación llama **SQLProcedure** para determinar si un procedimiento tiene un valor devuelto. Llama **SQLProcedureColumns** para determinar el tipo (valor devuelto, entrada, entrada/salida o de salida) de cada parámetro de procedimiento.
