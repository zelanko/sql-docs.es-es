---
title: Parámetros de procedimiento | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- procedure parameters [ODBC]
ms.assetid: 54fd857e-d2cb-467d-bb72-121e67a8e88d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1cab0fea9c39e4946122698f2476668464e556c1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62861535"
---
# <a name="procedure-parameters"></a>Parámetros de procedimiento
Parámetros en las llamadas a procedimiento pueden ser de entrada, entrada/salida o los parámetros de salida. Esto es diferente de parámetros en las demás instrucciones SQL, que siempre son parámetros de entrada.  
  
 Parámetros de entrada se usan para enviar los valores para el procedimiento. Por ejemplo, suponga que la tabla Parts tiene columnas PartID, descripción y precio. El procedimiento InsertPart podría tener un parámetro de entrada para cada columna en la tabla. Por ejemplo:  
  
```  
{call InsertPart(?, ?, ?)}  
```  
  
 Un controlador no debe modificar el contenido de un búfer de entrada hasta **SQLExecDirect** o **SQLExecute** devuelve SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE o SQL_NO_DATA. No se debe modificar el contenido del búfer de entrada mientras **SQLExecDirect** o **SQLExecute** devuelve SQL_NEED_DATA o SQL_STILL_EXECUTING.  
  
 Parámetros de entrada/salida se usan para enviar valores a los procedimientos y recuperar los valores de los procedimientos. Con el mismo parámetro como entrada y un parámetro de salida tiende a ser confuso y debe evitarse. Por ejemplo, suponga que un procedimiento acepta un identificador de pedido y devuelve el identificador del cliente. Esto puede definirse con un solo parámetro de entrada y salida:  
  
```  
{call GetCustID(?)}  
```  
  
 Podría ser mejor usar los dos parámetros: un parámetro de entrada para el identificador de pedido y un parámetro de entrada y salida para el identificador de cliente o salida:  
  
```  
{call GetCustID(?, ?)}  
```  
  
 Los parámetros de salida se usan para recuperar el valor devuelto del procedimiento y para recuperar valores de argumentos de procedimiento; los procedimientos que devuelven valores a veces se conocen como *funciones*. Por ejemplo, suponga que el **GetCustID** acabo de mencionar el procedimiento devuelve un valor que indica si ha podido encontrar el pedido. En la siguiente llamada, el primer parámetro es un parámetro de salida que se usa para recuperar el valor devuelto del procedimiento, el segundo parámetro es un parámetro de entrada que se utiliza para especificar el identificador de pedido y el tercer parámetro es un parámetro de salida que se usa para recuperar el identificador de cliente:  
  
```  
{? = call GetCustID(?, ?)}  
```  
  
 Controladores de controlan los valores de entrada y entrada y salida parámetros de procedimientos no forma diferente a los parámetros de entrada en otras instrucciones SQL. Cuando se ejecuta la instrucción, recuperan los valores de las variables enlazado a estos parámetros y los envían al origen de datos.  
  
 Una vez ejecutada la instrucción, los controladores de almacenan los valores devueltos de entrada/salida y parámetros de salida en las variables enlazadas a esos parámetros. Estos se devuelven los valores no se garantiza que se establece hasta que una vez que se han capturado todos los resultados devueltos por el procedimiento y **SQLMoreResults** devuelva SQL_NO_DATA. Si ejecuta la instrucción produce un error, el contenido del búfer de parámetro de entrada/salida o búfer del parámetro de salida es indefinido.  
  
 Una aplicación llama a **SQLProcedure** para determinar si un procedimiento tiene un valor devuelto. Llama a **SQLProcedureColumns** para determinar el tipo (valor devuelto, entrada, entrada/salida o de salida) de cada parámetro de procedimiento.
