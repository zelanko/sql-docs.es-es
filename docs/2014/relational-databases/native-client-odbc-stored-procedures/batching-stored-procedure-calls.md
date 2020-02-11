---
title: Procesar por lotes las llamadas a procedimientos almacenados | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- stored procedures [ODBC], batching
- ODBC, stored procedures
- SQL Server Native Client ODBC driver, stored procedures
- batches [ODBC]
- ODBC CALL escape sequence
ms.assetid: b7f53e11-15f0-4602-8134-b166160888f0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b50350006abba5085b11010f26aa88a89b07393f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68205497"
---
# <a name="batching-stored-procedure-calls"></a>Procesar por lotes las llamadas a procedimientos almacenados
  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client procesa automáticamente las llamadas a procedimientos almacenados en el servidor cuando sea necesario. El controlador solamente hace esto cuando se usa la secuencia de escape ODBC CALL; no lo hace para la instrucción EXECUTE de [!INCLUDE[tsql](../../includes/tsql-md.md)]. El procesamiento por lotes de las llamadas de procedimiento almacenado puede reducir el número de ciclos de ida y vuelta del servidor y aumentar de forma significativa el rendimiento.  
  
 El controlador procesa por lotes las llamadas de procedimiento al servidor al ejecutar un lote que contiene varias secuencias de escape ODBC CALL. También procesa por lotes las llamadas a procedimiento cuando se usan las matrices de parámetros enlazadas con una secuencia de escape ODBC CALL. Por ejemplo, si utiliza el enlace de parámetro de modo de fila o de modo de columna para enlazar una matriz de cinco elementos a los parámetros de una instrucción SQL CALL de ODBC, cuando se llama a **SQLExecute** o **SQLExecDirect** , el controlador envía un único lote con cinco llamadas de procedimiento al servidor.  
  
## <a name="see-also"></a>Consulte también  
 [Ejecutar procedimientos almacenados](running-stored-procedures.md)  
  
  
