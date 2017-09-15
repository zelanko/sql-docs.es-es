---
title: Valor de la lista argumentos | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], value list
- value list arguments [ODBC]
ms.assetid: 863837be-603b-4c7a-8b96-b71014037ee5
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a8386d5ffbb4d492bc8489272596fb9f6d58d245
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="value-list-arguments"></a>Argumentos de la lista de valores
Un argumento de valor de la lista está formada por una lista de valores separados por comas que se usarán para la coincidencia. Hay un argumento de la lista de un solo valor en las funciones de catálogo ODBC: la *TableType* argumento en **SQLTables**. Establecer *TableType* a un puntero null es el mismo que si se establece en SQL_ALL_TABLE_TYPES, que enumera todos los miembros posibles de la lista de valores. Este argumento no se ve afectado por el atributo de instrucción SQL_ATTR_METADATA_ID. Para obtener más información, consulte el [SQLTables](../../../odbc/reference/syntax/sqltables-function.md) descripción de la función.
