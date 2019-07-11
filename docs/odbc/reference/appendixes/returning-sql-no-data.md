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
ms.openlocfilehash: e2f731589dcbc10d24ff42d895db60f9f8c054de
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2019
ms.locfileid: "67794182"
---
# <a name="returning-sqlnodata"></a>Devuelve SQL_NO_DATA
Cuando un ODBC *2.x* aplicación se trabaja con un ODBC *3.x* controlador llama a **SQLExecDirect**, **SQLExecute**, o  **SQLParamData**, y se ha ejecutado una instrucción de eliminación o actualización por búsqueda, pero no afectó a ninguna fila en el origen de datos ODBC *3.x* controlador debería devolver SQL_SUCCESS. Cuando un ODBC *3.x* la aplicación funciona con un ODBC *3.x* controlador llama a **SQLExecDirect**, **SQLExecute**, o  **SQLParamData** con el mismo resultado, ODBC *3.x* controlador debería devolver SQL_NO_DATA.  
  
 Si una búsqueda instrucción update o delete en un lote de instrucciones no afecta a todas las filas en el origen de datos, **SQLMoreResults** devuelve SQL_SUCCESS. No se devuelve SQL_NO_DATA, ya que eso significaría que no hay ningún resultado más, no que hay es el resultado de una búsqueda, update o delete que no hay filas afectadas.
