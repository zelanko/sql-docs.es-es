---
title: Llamar a procedimientos almacenados (ODBC) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- stored procedures [ODBC], calling
ms.assetid: 31176be8-d40e-4f93-8d44-a46e804a3e2d
caps.latest.revision: 12
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 0846567d803eadf4364159fc01fdb8a7853e8a4f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36112484"
---
# <a name="call-stored-procedures-odbc"></a>Llamar a procedimientos almacenados (ODBC)
  Cuando una instrucción SQL llama a un procedimiento almacenado mediante la cláusula de escape ODBC CALL, el controlador de Microsoft® SQL Server™ envía el procedimiento a SQL Server usando el mecanismo de llamada a un procedimiento almacenado remoto (RPC). Las solicitudes de RPC omiten gran parte del análisis de la instrucción y del procesamiento del parámetro en SQL Server, y es más rápido que usar la instrucción Transact-SQL EXECUTE.  
  
 Para una aplicación de ejemplo que muestra esta característica, consulte [proceso códigos de retorno y parámetros de salida &#40;ODBC&#41;](running-stored-procedures-process-return-codes-and-output-parameters.md).  
  
### <a name="to-run-a-procedure-as-an-rpc"></a>Para ejecutar un procedimiento como una RPC  
  
1.  Cree una instrucción SQL que use la secuencia de escape ODBC CALL. La instrucción usa marcadores de parámetros para cada parámetro de entrada, de entrada/salida y de salida, así como para el valor devuelto por el procedimiento (si existe):  
  
    ```  
    {? = CALL procname (?,?)}  
    ```  
  
2.  Llame a [SQLBindParameter](../native-client-odbc-api/sqlbindparameter.md) para cada entrada, entrada/salida y el parámetro de salida y para el procedimiento de valor devuelto (si existe).  
  
3.  Ejecute la instrucción con [SQLExecDirect](http://go.microsoft.com/fwlink/?LinkId=58399).  
  
> [!NOTE]  
>  Si una aplicación envía un procedimiento con la sintaxis de Transact-SQL EXECUTE (en contraposición al flujo de escape ODBC CALL), el controlador ODBC de SQL Server pasa la llamada al procedimiento a SQL Server como una instrucción SQL en lugar de como una RPC. Además, los parámetros de salida no se devuelven si se usa la instrucción Transact-SQL EXECUTE.  
  
## <a name="see-also"></a>Vea también  
 [Temas de procedimientos almacenados de ejecución &#40;ODBC&#41;](../../database-engine/dev-guide/running-stored-procedures-how-to-topics-odbc.md)   
 [Procesamiento por lotes llamadas a procedimientos almacenados](../native-client-odbc-stored-procedures/batching-stored-procedure-calls.md)   
 [Ejecutar procedimientos almacenados](../native-client-odbc-stored-procedures/running-stored-procedures.md)   
 [Llamar a un procedimiento almacenado](../native-client-odbc-stored-procedures/calling-a-stored-procedure.md)   
 [Procedimientos](../native-client-odbc-queries/executing-statements/procedures.md)  
  
  