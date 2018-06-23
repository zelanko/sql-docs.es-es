---
title: SQLRowCount | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLRowCount function
ms.assetid: 967ed3d4-3d31-4485-ac92-027076ebc829
caps.latest.revision: 32
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: ae4c2fa55f5975357d94eaecb2f92e9468fee98f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198432"
---
# <a name="sqlrowcount"></a>SQLRowCount
  Cuando se enlazan las matrices de valores de parámetros de ejecución de la instrucción, `SQLRowCount` devuelve SQL_ERROR si cualquier fila de valores de parámetro genera una condición de error en la ejecución de la instrucción. Ningún valor se devuelve a través del argumento *RowCountPtr* de la función.  
  
 La aplicación puede beneficiarse del atributo de instrucciones SQL_ATTR_PARAMS_PROCESSED_PTR para capturar el número de parámetros procesados antes de que se produzca el error.  
  
 Además, la aplicación puede usar una matriz de valores de estado, enlazada mediante el atributo de instrucciones SQL_ATTR_PARAM_STATUS_PTR, para capturar los desplazamientos de la matriz de filas de parámetros incorrectos. La aplicación puede recorrer la matriz de estado para determinar el número real de filas procesadas.  
  
 Cuando un [!INCLUDE[tsql](../../includes/tsql-md.md)] se ejecuta una instrucción INSERT, UPDATE, DELETE o MERGE con una cláusula OUTPUT, SQLRowCount no devolverá el número de filas afectadas hasta que se hayan consumido todas las filas del conjunto de resultados generado por la cláusula OUTPUT. Para consumir estas filas, llame a SQLFetch o SQLFetchScroll. SQLResultCols devolverá -1 hasta que se hayan consumido todas las filas de resultados. Después de que SQLFetch o SQLFetchScroll devuelva SQL_NO_DATA, la aplicación debe llamar a SQLRowCount para determinar el número de filas afectadas antes de llamar a SQLMoreResults para desplazarse al siguiente resultado.  
  
## <a name="see-also"></a>Vea también  
 [SQLRowCount, función](http://go.microsoft.com/fwlink/?LinkId=59367)   
 [Detalles de implementación de la API de ODBC](odbc-api-implementation-details.md)  
  
  