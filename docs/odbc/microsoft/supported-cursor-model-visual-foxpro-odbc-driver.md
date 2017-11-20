---
title: Admite el modelo de Cursor (controlador ODBC de Visual FoxPro) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], cursors
- cursors [ODBC], Visual FoxPro ODBC driver
- FoxPro ODBC driver [ODBC], cursors
- static cursors [ODBC]
- block cursors [ODBC]
- rowset cursors [ODBC]
ms.assetid: be95bbb2-6886-491e-a5a7-f58028d19c1e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b80cb7cbbea13dbc6d491d757f28d44d5fda1ea6
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="supported-cursor-model-visual-foxpro-odbc-driver"></a>Modelo de Cursor compatibles (el controlador ODBC de Visual FoxPro)
El controlador de Visual FoxPro ODBC admite tanto *bloque* (*conjunto de filas*) y *estático* cursores. Los cursores estáticos son compatibles con cualquier controlador que se ajusta a la compatibilidad ODBC de nivel 1. El controlador no admite dinámicos, cursores controlados por o mixto (keyset y dynamic) cursores.  
  
 La aplicación puede llamar a [SQLSetStmtOption](../../odbc/microsoft/sqlsetstmtoption-visual-foxpro-odbc-driver.md) con una opción SQL_CURSOR_TYPE de SQL_CURSOR_FORWARD_ONLY (cursor de bloque) o SQL_CURSOR_STATIC (cursor estático).  
  
> [!NOTE]  
>  Si se llama a **SQLSetStmtOption** con una opción SQL_CURSOR_TYPE que no sean SQL_CURSOR_FORWARD_ONLY o SQL_CURSOR_STATIC, la función devuelve SQL_SUCCESS_WITH_INFO con un valor de SQLSTATE de 01S02 de SQLState (valor de opción cambiado). El controlador establece todos los modos de cursor no compatible en SQL_CURSOR_STATIC.  
  
 Para obtener más información acerca de los tipos de cursor y sobre **SQLSetStmtOption**, consulte el [referencia del programador de ODBC](../../odbc/reference/odbc-programmer-s-reference.md).  
  
## <a name="block-cursor"></a>cursor de bloque  
 Un conjunto de resultados de desplazamiento hacia delante, de solo lectura que se devuelve al cliente, que es responsable de mantener el almacenamiento para los datos.  
  
## <a name="static-cursor"></a>cursor estático  
 Una instantánea de un conjunto de datos definido por la consulta. Los cursores estáticos no reflejan los cambios en tiempo real de los datos subyacentes otros usuarios. Búfer de memoria del cursor es mantenido por la biblioteca de cursores ODBC, lo que permite el desplazamiento hacia delante y hacia atrás.  
  
## <a name="rowset"></a>conjunto de filas  
 Bloques de datos almacenados en un cursor, que representan filas recuperadas con un origen de datos.

