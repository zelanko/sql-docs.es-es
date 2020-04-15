---
title: Compatibilidad con SQLGetInfo ( SQLGetInfo Support) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- compatibility [ODBC], SQLGetInfo
- backward compatibility [ODBC], SQLGetInfo
- SQLGetInfo function [ODBC], support
ms.assetid: 57326f57-daba-46b6-b0be-6c97213b9ef1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a21c035a14814f51d4344894ef253b2cc844f4c2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307806"
---
# <a name="sqlgetinfo-support"></a>Compatibilidad con SQLGetInfo
Cuando un ODBC 2. *x* aplicación llama **sqlGetInfo** a un controlador ODBC 3 *.x,* se deben admitir los argumentos *InfoType* de la tabla siguiente.  
  
|*InfoType*|Devuelve|  
|----------------|-------------|  
|SQL_ALTER_TABLE (ODBC 2.0) **Nota:** Este tipo de información no está en desuso; las máscaras de bits en la columna de la derecha están en desuso.|Una máscara de bits SQLINTEGER enumerar las cláusulas de la instrucción **ALTER TABLE** admitida por el origen de datos.<br /><br /> Las siguientes máscaras de bits se utilizan para determinar qué cláusulas se admiten:<br /><br /> SQL_AT_DROP_COLUMN: se admite la capacidad de quitar columnas. Si esto da como resultado un comportamiento en cascada o restricción está definido por el controlador. (ODBC 2.0)<br /><br /> SQL_AT_ADD_COLUMN: se admite la capacidad de agregar varias columnas en una sola instrucción ALTER TABLE. Este bit no se combina con otros bits SQL_AT_ADD_COLUMN_XXX o bits SQL_AT_CONSTRAINT_XXX. (ODBC 2.0)|  
|SQL_FETCH_DIRECTION (ODBC 1.0)<br /><br /> El tipo de información se introdujo en ODBC 1.0; cada máscara de bits está etiquetada con la versión en la que se introdujo.|Una máscara de bits SQLINTEGER que enumera las opciones de dirección de captura admitidas.<br /><br /> Las siguientes máscaras de bits se utilizan junto con la marca para determinar qué opciones se admiten:<br /><br /> SQL_FD_FETCH_NEXT (ODBC 1.0) SQL_FD_FETCH_FIRST (ODBC 1.0) SQL_FD_FETCH_LAST SQL_FD_FETCH_PRIOR (ODBC 1.0) SQL_FD_FETCH_PRIOR (ODBC 1.0) SQL_FD_FETCH_ABSOLUTE (ODBC 1.0) SQL_FD_FETCH_RELATIVE (ODBC 1.0) SQL_FD_FETCH_BOOKMARK (ODBC 2.0)|  
|SQL_LOCK_TYPES (ODBC 2.0)|Una máscara de bits SQLINTEGER enumerar los tipos de bloqueo admitidos para el *fLock* argumento en **SQLSetPos**.<br /><br /> Las siguientes máscaras de bits se utilizan junto con la marca para determinar qué tipos de bloqueo se admiten:<br /><br /> SQL_LCK_NO_CHANGE SQL_LCK_EXCLUSIVE SQL_LCK_UNLOCK|  
|SQL_ODBC_API_CONFORMANCE (ODBC 1.0)|Un valor SQLSMALLINT que indica el nivel de conformidad ODBC.<br /><br /> SQL_OAC_NONE- Ninguno<br /><br /> SQL_OAC_LEVEL1: Nivel 1 soportado<br /><br /> SQL_OAC_LEVEL2: nivel 2 admitido|  
|SQL_ODBC_SQL_CONFORMANCE (ODBC 1.0)|Un valor SQLSMALLINT que indica la gramática SQL admitida por el controlador. Consulte [Apéndice C: Gramática SQL](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md) para obtener una definición de los niveles de conformidad de SQL.<br /><br /> SQL_OSC_MINIMUM- Gramática mínima soportada<br /><br /> SQL_OSC_CORE: gramática básica soportada<br /><br /> SQL_OSC_EXTENDED- Gramática extendida soportada|  
|SQL_POS_OPERATIONS (ODBC 2.0)|Una máscara de bits SQLINTEGER enumerar las operaciones admitidas en **SQLSetPos**.<br /><br /> Las siguientes máscaras de bits se utilizan junto con la marca para determinar qué opciones se admiten:<br /><br /> SQL_POS_POSITION (ODBC 2.0) SQL_POS_REFRESH (ODBC 2.0) SQL_POS_UPDATE (ODBC 2.0) SQL_POS_DELETE (ODBC 2.0) SQL_POS_ADD (ODBC 2.0)|  
|SQL_POSITIONED_STATEMENTS (ODBC 2.0)|Una máscara de bits SQLINTEGER enumerar las instrucciones SQL posicionadas admitidas.<br /><br /> Las siguientes máscaras de bits se utilizan para determinar qué instrucciones se admiten:<br /><br /> SQL_PS_POSITIONED_DELETE SQL_PS_POSITIONED_UPDATE SQL_PS_SELECT_FOR_UPDATE|  
|SQL_SCROLL_CONCURRENCY (ODBC 1.0)|Una máscara de bits SQLINTEGER enumerar las opciones de control de simultaneidad admitidas para el cursor.<br /><br /> Las siguientes máscaras de bits se utilizan para determinar qué opciones son compatibles:<br /><br /> SQL_SCCO_READ_ONLY - El cursor es de solo lectura. No se permiten actualizaciones.<br /><br /> SQL_SCCO_LOCK - Cursor utiliza el nivel más bajo de bloqueo suficiente para asegurarse de que la fila se puede actualizar.<br /><br /> SQL_SCCO_OPT_ROWVER: cursor utiliza un control de simultaneidad optimista, comparando versiones de fila, como SQLBase ROWID o Sybase TIMESTAMP.<br /><br /> SQL_SCCO_OPT_VALUES : cursor utiliza un control de simultaneidad optimista, comparando valores.|  
|SQL_STATIC_SENSITIVITY (ODBC 2.0)|Una máscara de bits SQLINTEGER que enumera si los cambios realizados por una aplicación en un cursor estático o controlado por conjunto de claves a través de **SQLSetPos** o las instrucciones de actualización o eliminación posicionadas pueden ser detectados por esa aplicación.<br /><br /> SQL_SS_ADDITIONS: las filas agregadas son visibles para el cursor; el cursor puede desplazarse a estas filas. Cuando estas filas se agregan al cursor depende del controlador.<br /><br /> SQL_SS_DELETIONS - Las filas eliminadas ya no están disponibles para el cursor y no dejan un "agujero" en el conjunto de resultados; después de que el cursor se desplaza de una fila eliminada, no puede volver a esa fila.<br /><br /> SQL_SS_UPDATES: las actualizaciones de las filas son visibles para el cursor; si el cursor se desplaza y vuelve a una fila actualizada, los datos devueltos por el cursor son los datos actualizados, no los datos originales. Esta opción solo se aplica a cursores estáticos o actualizaciones en cursores controlados por conjuntos de claves que no actualizan la clave. Esta opción no se aplica a un cursor dinámico ni en el caso en el que se cambia una clave en un cursor mixto.<br /><br /> Si una aplicación puede detectar los cambios realizados en el conjunto de resultados por otros usuarios, incluidos otros cursores en la misma aplicación, depende del tipo de cursor.|  
  
 Una aplicación ODBC 3 *.x* que trabaja con un controlador ODBC 3 *.x* no debe llamar a **SQLGetInfo** con los argumentos *InfoType* descritos en la tabla anterior, pero debe usar los argumentos ODBC 3 *.x* *InfoType* enumerados en el párrafo siguiente. No hay una correspondencia uno a uno entre los argumentos *InfoType* utilizados en ODBC 2. *x* y los utilizados en ODBC 3 *.x*. Una aplicación ODBC 3 *.x* que trabaja con un ODBC 2. *x* controlador, por otro lado, debe usar el *InfoType* argumentos descritos anteriormente.  
  
 Algunos de los tipos de información de la tabla anterior están en desuso en favor de los tipos de información de atributos de cursor. Estos tipos de información en desuso son SQL_FETCH_DIRECTION, SQL_LOCK_TYPES, SQL_POS_OPERATIONS, SQL_POSITIONED_STATEMENTS, SQL_SCROLL_CONCURRENCY y SQL_STATIC_SENSITIVITY. Los nuevos tipos de atributos de cursor se SQL_XXX_CURSOR_ATTRIBUTES1and SQL_XXX_CURSOR_ATTRIBUTES2, donde XXX es igual a DYNAMIC, FORWARD_ONLY, KEYSET_DRIVEN o STATIC. Cada uno de los nuevos tipos indica las capacidades del controlador para un único tipo de cursor. Para obtener más información acerca de estas opciones, vea la descripción de la función [SQLGetInfo.](../../../odbc/reference/syntax/sqlgetinfo-function.md)
