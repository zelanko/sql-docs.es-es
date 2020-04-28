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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 35d43ca7cf6e603d7dabca9eacf1e026daa753b7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306966"
---
# <a name="procedure-parameters"></a>Parámetros de procedimiento
Los parámetros de las llamadas a procedimientos pueden ser de entrada, de entrada/salida o de salida. Esto es diferente de los parámetros en todas las demás instrucciones SQL, que siempre son parámetros de entrada.  
  
 Los parámetros de entrada se utilizan para enviar valores al procedimiento. Por ejemplo, supongamos que la tabla Parts tiene columnas de campo de campo, Descripción y precio. El procedimiento InsertPart puede tener un parámetro de entrada para cada columna de la tabla. Por ejemplo:  
  
```  
{call InsertPart(?, ?, ?)}  
```  
  
 Un controlador no debe modificar el contenido de un búfer de entrada hasta que **SQLExecDirect** o **SQLExecute** devuelva SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE o SQL_NO_DATA. No se debe modificar el contenido del búfer de entrada, mientras que **SQLExecDirect** o **SQLExecute** devuelve SQL_NEED_DATA o SQL_STILL_EXECUTING.  
  
 Los parámetros de entrada y salida se usan para enviar valores a los procedimientos y recuperar los valores de los procedimientos. Usar el mismo parámetro como entrada y un parámetro de salida tiende a ser confuso y debe evitarse. Por ejemplo, supongamos que un procedimiento acepta un identificador de pedido y devuelve el identificador del cliente. Se puede definir con un solo parámetro de entrada/salida:  
  
```  
{call GetCustID(?)}  
```  
  
 Podría ser mejor usar dos parámetros: un parámetro de entrada para el identificador de pedido y un parámetro de salida o de entrada/salida para el ID. de cliente:  
  
```  
{call GetCustID(?, ?)}  
```  
  
 Los parámetros de salida se usan para recuperar el valor devuelto del procedimiento y recuperar los valores de los argumentos de procedimiento. los procedimientos que devuelven valores a veces se conocen como *funciones*. Por ejemplo, supongamos que el procedimiento **GetCustID** que acaba de mencionar devuelve un valor que indica si se ha podido encontrar el pedido. En la siguiente llamada, el primer parámetro es un parámetro de salida que se usa para recuperar el valor devuelto por el procedimiento, el segundo parámetro es un parámetro de entrada que se usa para especificar el identificador de pedido y el tercer parámetro es un parámetro de salida que se usa para recuperar el ID. de cliente:  
  
```  
{? = call GetCustID(?, ?)}  
```  
  
 Los controladores controlan los valores de los parámetros de entrada y de entrada/salida de los procedimientos de forma distinta a los parámetros de entrada en otras instrucciones SQL. Cuando se ejecuta la instrucción, recupera los valores de las variables enlazadas a estos parámetros y los envía al origen de datos.  
  
 Una vez ejecutada la instrucción, los controladores almacenan los valores devueltos de los parámetros de entrada/salida y de salida en las variables enlazadas a esos parámetros. No se garantiza que estos valores devueltos se establezcan hasta que se hayan recuperado todos los resultados devueltos por el procedimiento y **SQLMoreResults** haya devuelto SQL_NO_DATA. Si la ejecución de la instrucción produce un error, el contenido del búfer de parámetros de entrada/salida o del búfer de parámetros de salida no está definido.  
  
 Una aplicación llama a **SQLProcedure** para determinar si un procedimiento tiene un valor devuelto. Llama a **SQLProcedureColumns** para determinar el tipo (valor devuelto, entrada, entrada/salida o salida) de cada parámetro de procedimiento.
