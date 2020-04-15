---
title: Parámetros de procedimiento ? Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306966"
---
# <a name="procedure-parameters"></a>Parámetros de procedimiento
Los parámetros de las llamadas a procedimientos pueden ser parámetros de entrada, entrada/salida o salida. Esto es diferente de los parámetros de todas las demás instrucciones SQL, que siempre son parámetros de entrada.  
  
 Los parámetros de entrada se utilizan para enviar valores al procedimiento. Por ejemplo, supongamos que la tabla Parts tiene columnas PartID, Description y Price. El InsertPart procedimiento puede tener un parámetro de entrada para cada columna de la tabla. Por ejemplo:  
  
```  
{call InsertPart(?, ?, ?)}  
```  
  
 Un controlador no debe modificar el contenido de un búfer de entrada hasta que **SQLExecDirect** o **SQLExecute** devuelve SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_INVALID_HANDLE o SQL_NO_DATA. El contenido del búfer de entrada no se debe modificar mientras **SQLExecDirect** o **SQLExecute** devuelve SQL_NEED_DATA o SQL_STILL_EXECUTING.  
  
 Los parámetros de entrada/salida se utilizan tanto para enviar valores a procedimientos como para recuperar valores de procedimientos. El uso del mismo parámetro que un parámetro de entrada y un parámetro de salida tiende a ser confuso y debe evitarse. Por ejemplo, supongamos que un procedimiento acepta un identificador de pedido y devuelve el identificador del cliente. Esto se puede definir con un único parámetro de entrada/salida:  
  
```  
{call GetCustID(?)}  
```  
  
 Podría ser mejor utilizar dos parámetros: un parámetro de entrada para el ID de pedido y un parámetro de salida o entrada/salida para el ID de cliente:  
  
```  
{call GetCustID(?, ?)}  
```  
  
 Los parámetros de salida se utilizan para recuperar el valor devuelto del procedimiento y para recuperar valores de argumentos de procedimiento; los procedimientos que devuelven valores a veces se conocen como *funciones.* Por ejemplo, supongamos que el procedimiento **GetCustID** que acaba de mencionar devuelve un valor que indica si pudo encontrar el pedido. En la siguiente llamada, el primer parámetro es un parámetro de salida utilizado para recuperar el valor devuelto por el procedimiento, el segundo parámetro es un parámetro de entrada utilizado para especificar el ID de pedido y el tercer parámetro es un parámetro de salida utilizado para recuperar el ID de cliente:  
  
```  
{? = call GetCustID(?, ?)}  
```  
  
 Los controladores controlan los valores de los parámetros de entrada y entrada/salida en procedimientos no de forma diferente a los parámetros de entrada de otras instrucciones SQL. Cuando se ejecuta la instrucción, recuperan los valores de las variables enlazadas a estos parámetros y los envían al origen de datos.  
  
 Una vez ejecutada la instrucción, los controladores almacenan los valores devueltos de los parámetros de entrada/salida y salida en las variables enlazadas a esos parámetros. No se garantiza que estos valores devueltos se establezcan hasta que se hayan capturado todos los resultados devueltos por el procedimiento y **SQLMoreResults** haya devuelto SQL_NO_DATA. Si la ejecución de la instrucción produce un error, el contenido del búfer de parámetros de entrada/salida o del búfer de parámetros de salida no está definido.  
  
 Una aplicación llama a **SQLProcedure** para determinar si un procedimiento tiene un valor devuelto. Llama a **SQLProcedureColumns** para determinar el tipo (valor de retorno, entrada, entrada/salida o salida) de cada parámetro de procedimiento.
