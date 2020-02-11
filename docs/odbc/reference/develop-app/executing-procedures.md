---
title: Ejecutando procedimientos | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], procedures
- procedures [ODBC], executing
ms.assetid: a75e497a-4661-438a-a10e-f598c65f81be
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 98c36f02bde63862748eef14a8cbae063ca4e472
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68069955"
---
# <a name="executing-procedures"></a>Ejecución de procedimientos
ODBC define una secuencia de escape estándar para ejecutar procedimientos. Para obtener la sintaxis de esta secuencia y un ejemplo de código que la usa, vea [llamadas a procedimientos](../../../odbc/reference/develop-app/procedure-calls.md).  
  
 Para ejecutar un procedimiento, una aplicación realiza las siguientes acciones:  
  
1.  Establece los valores de los parámetros. Para obtener más información, vea [parámetros de instrucción](../../../odbc/reference/develop-app/statement-parameters.md), más adelante en esta sección.  
  
2.  Llama a **SQLExecDirect** y le pasa una cadena que contiene la instrucción SQL que ejecuta el procedimiento. Esta instrucción puede utilizar la secuencia de escape definida por la sintaxis específica de ODBC o DBMS; las instrucciones que usan la sintaxis específica de DBMS no son interoperables.  
  
3.  Cuando se llama a **SQLExecDirect** , el controlador:  
  
    -   Recupera los valores de parámetro actuales y los convierte según sea necesario. Para obtener más información, vea [parámetros de instrucción](../../../odbc/reference/develop-app/statement-parameters.md), más adelante en esta sección.  
  
    -   Llama al procedimiento en el origen de datos y le envía los valores de parámetro convertidos. La forma en que el controlador llama al procedimiento es específica del controlador. Por ejemplo, puede modificar la instrucción SQL para utilizar la gramática de SQL del origen de datos y enviar esta instrucción para su ejecución, o puede llamar al procedimiento directamente mediante un mecanismo de llamada a procedimiento remoto (RPC) que se define en el protocolo de flujo de datos del DBMS.  
  
    -   Devuelve los valores de cualquier parámetro de entrada/salida o de salida o el valor devuelto del procedimiento, suponiendo que el procedimiento se realiza correctamente. Es posible que estos valores no estén disponibles hasta que se hayan procesado todos los demás resultados (recuentos de filas y conjuntos de resultados) generados por el procedimiento. Si se produce un error en el procedimiento, el controlador devuelve los errores.
