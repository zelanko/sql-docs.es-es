---
title: Ejecutar procedimientos | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: ff234d1d8e099611c8718eac5ae3b584e926a2bd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63061973"
---
# <a name="executing-procedures"></a>Ejecución de procedimientos
ODBC define una secuencia de escape estándar para la ejecución de procedimientos. Para obtener la sintaxis de esta secuencia y un ejemplo de código que lo utiliza, consulte [las llamadas a procedimiento](../../../odbc/reference/develop-app/procedure-calls.md).  
  
 Para ejecutar un procedimiento, una aplicación realiza las acciones siguientes:  
  
1.  Establece los valores de los parámetros. Para obtener más información, consulte [parámetros de la instrucción](../../../odbc/reference/develop-app/statement-parameters.md), más adelante en esta sección.  
  
2.  Las llamadas **SQLExecDirect** y le pasa una cadena que contiene la instrucción SQL que ejecuta el procedimiento. Esta instrucción puede utilizar la secuencia de escape definida por la sintaxis ODBC o específicos para DBMS; las instrucciones que utilizan la sintaxis específicos para DBMS no son interoperables.  
  
3.  Cuando **SQLExecDirect** se llama, el controlador:  
  
    -   Recupera los valores de parámetro actuales y los convierte según sea necesario. Para obtener más información, consulte [parámetros de la instrucción](../../../odbc/reference/develop-app/statement-parameters.md), más adelante en esta sección.  
  
    -   Llama al procedimiento en el origen de datos y lo envía los valores de parámetro convertido. Cómo el controlador llama al procedimiento es específico del controlador. Por ejemplo, puede modificar la instrucción SQL para usar la gramática SQL del origen de datos y enviar esta instrucción para ejecutarla o podría llamar al procedimiento directamente mediante un mecanismo de llamada a procedimiento remoto (RPC) que se define en el protocolo de flujo de datos del DBMS.  
  
    -   Devuelve los valores de parámetros de salida o de cualquier entrada y salida o el valor devuelto del procedimiento, suponiendo que el procedimiento se realiza correctamente. Estos valores no esté disponibles hasta después de que se han procesado todos los demás resultados (conjuntos de resultados y recuentos de filas) generados por el procedimiento. Si se produce un error en el procedimiento, el controlador devuelve los errores.
