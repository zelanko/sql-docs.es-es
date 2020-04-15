---
title: Regreso SQL_NO_DATA Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3e2c806edd5d5647e09c00975ad7207ee5c2c876
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305116"
---
# <a name="returning-sql_no_data"></a>Devuelve SQL_NO_DATA
Cuando se ejecuta una aplicación ODBC *2.x* que funciona con un controlador ODBC *3.x* llama a **SQLExecDirect**, **SQLExecute**o **SQLParamData**y se ha ejecutado una instrucción de actualización o eliminación buscada, pero no afecta a ninguna fila del origen de datos, el controlador ODBC *3.x* debe devolver SQL_SUCCESS. Cuando una aplicación ODBC *3.x* que trabaja con un controlador ODBC *3.x* llama a **SQLExecDirect**, **SQLExecute**o **SQLParamData** con el mismo resultado, el controlador ODBC *3.x* debe devolver SQL_NO_DATA.  
  
 Si una instrucción de actualización o eliminación buscada en un lote de instrucciones no afecta a ninguna fila del origen de datos, **SQLMoreResults** devuelve SQL_SUCCESS. No puede devolver SQL_NO_DATA, porque eso significaría que no hay más resultados, no es que haya un resultado de una actualización o eliminación buscada que no afectara a ninguna fila.
