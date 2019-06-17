---
title: Devuelve SQL_NO_DATA | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL_NO_DATA [ODBC]
- backward compatibility [ODBC], SQL_NO_DATA
- compatibility [ODBC], SQL_NO_DATA
ms.assetid: deed0163-9d1a-4e9b-9342-3f82e64477d2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 74c122819980abaa328db5ad46f240cae24b92d3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63280588"
---
# <a name="returning-sqlnodata"></a>Devuelve SQL_NO_DATA
Cuando un ODBC 2. *x* aplicación se trabaja con una aplicación ODBC 3 *.x* controlador llama a **SQLExecDirect**, **SQLExecute**, o **SQLParamData**, y se ha ejecutado una instrucción de eliminación o actualización por búsqueda, pero no afectó a ninguna fila en el origen de datos, el 3 de ODBC *.x* controlador debería devolver SQL_SUCCESS. Cuando una aplicación ODBC 3 *.x* la aplicación funciona con una aplicación ODBC 3 *.x* controlador llama a **SQLExecDirect**, **SQLExecute**, o  **SQLParamData** con el mismo resultado, el 3 de ODBC *.x* controlador debería devolver SQL_NO_DATA.  
  
 Si una búsqueda instrucción update o delete en un lote de instrucciones no afecta a todas las filas en el origen de datos, **SQLMoreResults** devuelve SQL_SUCCESS. No se devuelve SQL_NO_DATA, ya que eso significaría que no hay ningún resultado más, no que hay es el resultado de una búsqueda, update o delete que no hay filas afectadas.
