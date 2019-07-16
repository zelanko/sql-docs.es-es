---
title: Valor de argumentos de la lista | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], value list
- value list arguments [ODBC]
ms.assetid: 863837be-603b-4c7a-8b96-b71014037ee5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 646d2724489140080a673f31e22429cc7ca39d4e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68022102"
---
# <a name="value-list-arguments"></a>Argumentos de la lista de valores
Un argumento de valor de la lista consta de una lista de valores separados por comas que se usará para la coincidencia. Hay un argumento de la lista de un solo valor en las funciones de catálogo ODBC: el *TableType* argumento en **SQLTables**. Establecer *TableType* a un puntero null es el mismo que si se establece en SQL_ALL_TABLE_TYPES, que enumera todos los posibles miembros de la lista de valores. Este argumento no se ve afectado por el atributo de instrucción SQL_ATTR_METADATA_ID. Para obtener más información, consulte el [SQLTables](../../../odbc/reference/syntax/sqltables-function.md) descripción de la función.
