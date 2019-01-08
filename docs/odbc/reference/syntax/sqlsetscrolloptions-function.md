---
title: Función SQLSetScrollOptions | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetScrollOptions
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetScrollOptions
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC]
ms.assetid: 2a825ba7-7942-4c23-bcdb-c80dc12f8c86
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: dbdd2038bc217a7ca2a2efe08940c03c5da5d8f0
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/11/2018
ms.locfileid: "53206754"
---
# <a name="sqlsetscrolloptions-function"></a>Función SQLSetScrollOptions
**Conformidad**  
 Versión de introducción: Cumplimiento de estándares 1.0 de ODBC: Obsoleto  
  
 **Resumen**  
 En ODBC 3 *.x*, la función ODBC 2.0 **SQLSetScrollOptions** ha sido reemplazado por las llamadas a **SQLGetInfo** y **SQLSetStmtAttr**.  
  
> [!NOTE]
>  Para obtener más información sobre lo que el Administrador de controladores se asigna esta función cuando un ODBC 2 *.x* aplicación funciona con una aplicación ODBC 3 *.x* controladores, consulte [asignación de funciones en desuso](../../../odbc/reference/appendixes/mapping-deprecated-functions.md)en el apéndice G: Directrices de controlador para la compatibilidad con versiones anteriores.  
> 
> [!NOTE]
>  Cuando se asigna el Administrador de controladores **SQLSetScrollOptions** para una aplicación que funciona con una aplicación ODBC 3 *.x* controlador que no es compatible con **SQLSetScrollOptions**, el controlador El administrador establece la opción de instrucción SQL_ROWSET_SIZE, no el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE, a la *RowsetSize* argumento en **SQLSetScrollOption**. Como resultado, **SQLSetScrollOptions** no se puede usar una aplicación al recuperar varias filas mediante una llamada a **SQLFetch** o **SQLFetchScroll**. Puede usarse solo cuando al capturar varias filas mediante una llamada a **SQLExtendedFetch**.  
  
## <a name="remarks"></a>Comentarios  
 Si la aplicación se ejecutará en un sistema operativo de 64 bits, consulte [información ODBC 64-Bit](../../../odbc/reference/odbc-64-bit-information.md).  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
