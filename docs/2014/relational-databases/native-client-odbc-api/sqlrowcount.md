---
title: SQLRowCount | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLRowCount function
ms.assetid: 967ed3d4-3d31-4485-ac92-027076ebc829
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4ff2a744f68cf6152330179eb8dcab1f33911914
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/13/2018
ms.locfileid: "53354743"
---
# <a name="sqlrowcount"></a>SQLRowCount
  Cuando las matrices de valores de parámetro se enlazan para la ejecución de la instrucción, `SQLRowCount` devuelve SQL_ERROR si cualquier fila de valores de parámetro genera una condición de error en la ejecución de la instrucción. Ningún valor se devuelve a través del argumento *RowCountPtr* de la función.  
  
 La aplicación puede beneficiarse del atributo de instrucciones SQL_ATTR_PARAMS_PROCESSED_PTR para capturar el número de parámetros procesados antes de que se produzca el error.  
  
 Además, la aplicación puede usar una matriz de valores de estado, enlazada mediante el atributo de instrucciones SQL_ATTR_PARAM_STATUS_PTR, para capturar los desplazamientos de la matriz de filas de parámetros incorrectos. La aplicación puede recorrer la matriz de estado para determinar el número real de filas procesadas.  
  
 Cuando un [!INCLUDE[tsql](../../includes/tsql-md.md)] se ejecuta una instrucción INSERT, UPDATE, DELETE o MERGE con una cláusula OUTPUT, SQLRowCount no devolverá el recuento de filas afectadas hasta que se hayan consumido todas las filas del conjunto de resultados generado por la cláusula OUTPUT. Para consumir estas filas, llamar a SQLFetch o SQLFetchScroll. SQLResultCols devolverá -1 hasta que se hayan consumido todas las filas del resultado. Una vez SQLFetch o SQLFetchScroll devuelve SQL_NO_DATA, la aplicación debe llamar a SQLRowCount para determinar el número de filas afectadas antes de llamar a SQLMoreResults para desplazarse al siguiente resultado.  
  
## <a name="see-also"></a>Vea también  
 [Función SQLRowCount](https://go.microsoft.com/fwlink/?LinkId=59367)   
 [Detalles de implementación de la API de ODBC](odbc-api-implementation-details.md)  
  
  
