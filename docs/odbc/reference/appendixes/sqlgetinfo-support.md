---
title: Compatibilidad con SQLGetInfo | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- compatibility [ODBC], SQLGetInfo
- backward compatibility [ODBC], SQLGetInfo
- SQLGetInfo function [ODBC], support
ms.assetid: 57326f57-daba-46b6-b0be-6c97213b9ef1
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c276373e01ab45c8c0464869296a121f8388884f
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="sqlgetinfo-support"></a>Compatibilidad con SQLGetInfo
Cuando un ODBC 2. *x* aplicación llama **SQLGetInfo** a una aplicación ODBC 3*.x* controlador, el *tipo de información* argumentos en la tabla siguiente deben ser compatibles.  
  
|*Tipo de información*|Devuelve|  
|----------------|-------------|  
|SQL_ALTER_TABLE (ODBC 2.0) **Nota:** este tipo de información no está en desuso; las máscaras de bits en la columna a la derecha están en desuso.|Una máscara de bits SQLINTEGER enumerar las cláusulas de la **ALTER TABLE** instrucción admitida por el origen de datos.<br /><br /> La máscara de bits siguiente se utiliza para determinar qué cláusulas son compatibles:<br /><br /> SQL_AT_DROP_COLUMN = se admite la posibilidad de quitar columnas. Si esto da como resultado cascade o limitar el comportamiento es definido por el controlador. (ODBC 2.0)<br /><br /> SQL_AT_ADD_COLUMN = la capacidad para agregar varias columnas en una sola instrucción ALTER TABLE se admite. Este bit no combinar con otros SQL_AT_ADD_COLUMN_XXX ó SQL_AT_CONSTRAINT_XXX bits. (ODBC 2.0)|  
|SQL_FETCH_DIRECTION (ODBC 1.0)<br /><br /> El tipo de información introducido en ODBC 1.0; Cada máscara de bits se etiqueta con la versión en la que se introdujo.|Una máscara de bits SQLINTEGER enumerar las opciones de dirección de recopilación compatibles.<br /><br /> La máscara de bits siguiente se utiliza junto con la marca para determinar qué opciones son compatibles:<br /><br /> SQL_FD_FETCH_NEXT (ODBC 1.0) SQL_FD_FETCH_FIRST (ODBC 1.0) SQL_FD_FETCH_LAST (ODBC 1.0) SQL_FD_FETCH_PRIOR (ODBC 1.0) SQL_FD_FETCH_ABSOLUTE (ODBC 1.0) SQL_FD_FETCH_RELATIVE (ODBC 1.0) SQL_FD_FETCH_BOOKMARK (ODBC 2.0)|  
|SQL_LOCK_TYPES (ODBC 2.0)|Los tipos de una máscara de bits SQLINTEGER enumerando el bloqueo admitido para la *genealógico* argumento en **SQLSetPos**.<br /><br /> La máscara de bits siguiente se utiliza junto con la marca para determinar qué tipos de bloqueo son compatibles:<br /><br /> SQL_LCK_NO_CHANGE SQL_LCK_EXCLUSIVE SQL_LCK_UNLOCK|  
|SQL_ODBC_API_CONFORMANCE (ODBC 1.0)|Un valor SQLSMALLINT que indica el nivel de conformidad de ODBC.<br /><br /> SQL_OAC_NONE = ninguno<br /><br /> SQL_OAC_LEVEL1 = 1 nivel compatibles<br /><br /> SQL_OAC_LEVEL2 = admitidas el nivel 2|  
|SQL_ODBC_SQL_CONFORMANCE (ODBC 1.0)|Un valor SQLSMALLINT que indica la gramática SQL admitida por el controlador. Vea [Apéndice C: SQL gramática](../../../odbc/reference/appendixes/appendix-c-sql-grammar.md) para una definición de los niveles de compatibilidad de SQL.<br /><br /> SQL_OSC_MINIMUM = gramática mínimo compatible<br /><br /> SQL_OSC_CORE = gramática básica de compatibles<br /><br /> SQL_OSC_EXTENDED = gramática extendida compatibles|  
|SQL_POS_OPERATIONS (ODBC 2.0)|Una máscara de bits SQLINTEGER enumerar las operaciones admitidas en **SQLSetPos**.<br /><br /> La máscara de bits siguiente sirven para junto con la marca para determinar qué opciones son compatibles:<br /><br /> SQL_POS_POSITION (ODBC 2.0) SQL_POS_REFRESH (ODBC 2.0) SQL_POS_UPDATE (ODBC 2.0) SQL_POS_DELETE (ODBC 2.0) SQL_POS_ADD (ODBC 2.0)|  
|SQL_POSITIONED_STATEMENTS (ODBC 2.0)|Una máscara de bits SQLINTEGER enumerar admiten coloca las instrucciones SQL.<br /><br /> La máscara de bits siguiente se utiliza para determinar qué instrucciones se admiten:<br /><br /> SQL_PS_POSITIONED_DELETE SQL_PS_POSITIONED_UPDATE SQL_PS_SELECT_FOR_UPDATE|  
|SQL_SCROLL_CONCURRENCY (ODBC 1.0)|Una máscara de bits SQLINTEGER enumerar las opciones de control de simultaneidad admitidas para el cursor.<br /><br /> La máscara de bits siguiente se utiliza para determinar qué opciones son compatibles:<br /><br /> SQL_SCCO_READ_ONLY = Cursor es de solo lectura. No se permiten actualizaciones.<br /><br /> SQL_SCCO_LOCK = Cursor usará el nivel más bajo de bloqueo suficiente para asegurarse de que se puede actualizar la fila.<br /><br /> SQL_SCCO_OPT_ROWVER = Cursor utiliza control de simultaneidad optimista, comparar las versiones de fila, como SQLBase ROWID o Sybase TIMESTAMP.<br /><br /> SQL_SCCO_OPT_VALUES = Cursor utiliza control de simultaneidad optimista, comparar los valores.|  
|SQL_STATIC_SENSITIVITY (ODBC 2.0)|Una máscara de bits SQLINTEGER enumerar si los cambios realizados por una aplicación a un cursor estático o controlado por conjunto de claves a través de **SQLSetPos** o actualización por posición o las instrucciones delete se pueden detectar mediante esa aplicación.<br /><br /> SQL_SS_ADDITIONS = Added filas son visibles para el cursor; se puede desplazar el cursor a estas filas. En estas filas se agregan al cursor depende del controlador.<br /><br /> SQL_SS_DELETIONS = Deleted filas ya no están disponibles para el cursor y no dejan a un "agujero" en el conjunto de resultados; Después de que el cursor se desplaza de una fila eliminada, éste no se puede volver a esa fila.<br /><br /> SQL_SS_UPDATES = las actualizaciones a las filas son visibles hasta el cursor; Si el cursor se desplaza desde y devuelve a la fila actualizada, los datos devueltos por el cursor están los datos actualizados, no los datos originales. Esta opción aplica a los cursores estáticos solo a o actualizaciones en los cursores dinámicos que no se actualizan la clave. Esta opción no se aplica para un cursor dinámico o en el caso en el que se cambia una clave en un cursor mixto.<br /><br /> Si una aplicación puede detectar los cambios realizados en el conjunto de resultados por otros usuarios, incluidos otros cursores en la misma aplicación, depende del tipo de cursor.|  
  
 Una aplicación ODBC 3*.x* aplicación trabajar con una aplicación ODBC 3*.x* controlador no debe llamar a **SQLGetInfo** con el *tipo de información* argumentos describen en anterior a la tabla sino que debe utilizar ODBC 3*.x* *tipo de información* los argumentos se muestran en el párrafo siguiente. No hay una correspondencia exacta entre *tipo de información* argumentos que se usan en ODBC 2. *x* y los que se usan en ODBC 3*.x*. Una aplicación ODBC 3*.x* aplicación trabajar con una API ODBC 2. *x* controlador, por otro lado, debe usar el *tipo de información* argumentos se ha descrito anteriormente.  
  
 Algunos de los tipos de información en la tabla anterior se ha sustituido por los tipos de información de atributos de cursor. Estos tipos son SQL_FETCH_DIRECTION, SQL_LOCK_TYPES, SQL_POS_OPERATIONS, SQL_POSITIONED_STATEMENTS, SQL_SCROLL_CONCURRENCY y SQL_STATIC_SENSITIVITY de información en desuso. Los nuevos tipos de atributos de cursor son SQL_XXX_CURSOR_ATTRIBUTES1and SQL_XXX_CURSOR_ATTRIBUTES2, donde XXX es igual a DYNAMIC, FORWARD_ONLY, KEYSET_DRIVEN o STATIC. Cada uno de los nuevos tipos de indica las capacidades de controlador para un tipo de cursor simple. Para obtener más información acerca de estas opciones, consulte la [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descripción de la función.
