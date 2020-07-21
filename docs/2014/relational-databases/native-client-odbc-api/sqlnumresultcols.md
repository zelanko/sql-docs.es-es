---
title: SQLNumResultCols | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLNumResultCols function
ms.assetid: f79d8b3c-521e-4e50-a564-21d73ae5767b
author: rothja
ms.author: jroth
ms.openlocfilehash: 45e72165eef621dc377b02ed3d2e7e1e3cf7ab8e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85021870"
---
# <a name="sqlnumresultcols"></a>SQLNumResultCols
  Para las instrucciones ejecutadas, el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client no tiene acceso al servidor para notificar el número de columnas de un conjunto de resultados. En este caso, `SQLNumResultCols` no produce un viaje de ida y vuelta al servidor. Como [SQLDescribeCol](sqldescribecol.md) y [SQLColAttribute](sqlcolattribute.md), al llamar a `SQLNumResultCols` en instrucciones preparadas pero no ejecutadas se genera un viaje de ida y vuelta al servidor.  
  
 Cuando una instrucción o un lote de instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] devuelve varios conjuntos de filas de resultados, es posible que el número de columnas del conjunto de resultados cambie de un conjunto a otro. `SQLNumResultCols`se debe llamar a para cada conjunto. Cuando el número de columnas cambia, la aplicación debe volver a enlazar los valores de datos antes de capturar los resultados de la fila. Para obtener más información sobre cómo administrar la devolución de varios conjuntos de resultados, vea [SQLMoreResults](sqlmoreresults.md).  
  
 Las mejoras en el motor de base de datos a partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] permiten a SQLNumResultCols obtener descripciones más precisas de los resultados esperados. Estos resultados más precisos pueden diferir de los valores devueltos por SQLNumResultCols en versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obtener más información, vea [Detección de metadatos](../native-client/features/metadata-discovery.md).  
  
## <a name="see-also"></a>Consulte también  
 [SQLNumResultCols función)](https://go.microsoft.com/fwlink/?LinkId=59359)   
 [ODBC API Implementation Details](odbc-api-implementation-details.md)  
  
  
