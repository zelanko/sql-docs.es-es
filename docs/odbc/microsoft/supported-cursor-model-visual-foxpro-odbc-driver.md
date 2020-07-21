---
title: Modelo de cursor compatible (controlador ODBC de Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], cursors
- cursors [ODBC], Visual FoxPro ODBC driver
- FoxPro ODBC driver [ODBC], cursors
- static cursors [ODBC]
- block cursors [ODBC]
- rowset cursors [ODBC]
ms.assetid: be95bbb2-6886-491e-a5a7-f58028d19c1e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cf3400f24e20a8fa864404612bf07ea44efce49e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301131"
---
# <a name="supported-cursor-model-visual-foxpro-odbc-driver"></a>Modelo de Cursor compatibles (el controlador ODBC de Visual FoxPro)
El controlador ODBC de Visual FoxPro es compatible con los cursores de *bloque* (*conjunto de filas*) y *estáticos* . Los cursores estáticos son compatibles con cualquier controlador que se ajuste al cumplimiento de ODBC de nivel 1. El controlador no es compatible con los cursores dinámicos, controlados por conjunto de claves o mixtos (Keyset y dinámicos).  
  
 La aplicación puede llamar a [SQLSetStmtOption](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md) con una opción SQL_CURSOR_TYPE de SQL_CURSOR_FORWARD_ONLY (cursor de bloque) o SQL_CURSOR_STATIC (cursor estático).  
  
> [!NOTE]  
>  Si llama a **SQLSetStmtOption** con una opción SQL_CURSOR_TYPE distinta de SQL_CURSOR_FORWARD_ONLY o SQL_CURSOR_STATIC, la función devuelve SQL_SUCCESS_WITH_INFO con un SQLSTATE de 01S02 (valor de opción cambiado). El controlador establece todos los modos de cursor no admitidos en SQL_CURSOR_STATIC.  
  
 Para obtener más información sobre los tipos de cursor y sobre **SQLSetStmtOption**, vea la [Referencia del programador de ODBC](../../odbc/reference/odbc-programmer-s-reference.md).  
  
## <a name="block-cursor"></a>cursor de bloque  
 Un conjunto de resultados de desplazamiento hacia delante y de solo lectura devuelto al cliente, que es responsable de mantener el almacenamiento de los datos.  
  
## <a name="static-cursor"></a>cursor estático  
 Una instantánea de un conjunto de datos definido por la consulta. Los cursores estáticos no reflejan los cambios en tiempo real de los datos subyacentes de otros usuarios. La biblioteca de cursores ODBC mantiene el búfer de memoria del cursor, que permite el desplazamiento hacia delante y hacia atrás.  
  
## <a name="rowset"></a>conjunto de filas  
 Bloques de datos almacenados en un cursor, que representan las filas recuperadas de un origen de datos.
