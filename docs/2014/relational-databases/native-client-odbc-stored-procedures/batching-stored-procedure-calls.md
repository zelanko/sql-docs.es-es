---
title: Llamadas a procedimientos almacenados de procesamiento por lotes | Documentos de Microsoft
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
- stored procedures [ODBC], batching
- ODBC, stored procedures
- SQL Server Native Client ODBC driver, stored procedures
- batches [ODBC]
- ODBC CALL escape sequence
ms.assetid: b7f53e11-15f0-4602-8134-b166160888f0
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: fd3d7fca3dc22d20c9aeadfc3b60fa41fa64f895
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36111780"
---
# <a name="batching-stored-procedure-calls"></a>Procesar por lotes las llamadas a procedimientos almacenados
  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC Native Client procesa automáticamente por lotes las llamadas a procedimientos almacenados en el servidor cuando sea apropiado. El controlador solamente hace esto cuando se usa la secuencia de escape ODBC CALL; no lo hace para la instrucción EXECUTE de [!INCLUDE[tsql](../../includes/tsql-md.md)]. El procesamiento por lotes de las llamadas de procedimiento almacenado puede reducir el número de ciclos de ida y vuelta del servidor y aumentar de forma significativa el rendimiento.  
  
 El controlador procesa por lotes las llamadas de procedimiento al servidor al ejecutar un lote que contiene varias secuencias de escape ODBC CALL. También procesa por lotes las llamadas a procedimiento cuando se usan las matrices de parámetros enlazadas con una secuencia de escape ODBC CALL. Por ejemplo, si utiliza cualquier enlace de parámetros de modo de fila o columna para enlazar una matriz con cinco elementos a los parámetros de una instrucción ODBC CALL de SQL, cuando **SQLExecute** o **SQLExecDirect** se llama, el controlador envía un lote único con cinco llamadas de procedimiento en el servidor.  
  
## <a name="see-also"></a>Vea también  
 [Ejecutar procedimientos almacenados](running-stored-procedures.md)  
  
  