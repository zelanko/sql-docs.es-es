---
title: Argumentos de lista de valores | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68022102"
---
# <a name="value-list-arguments"></a>Argumentos de la lista de valores
Un argumento de lista de valores se compone de una lista de valores separados por comas que se usarán para la búsqueda de coincidencias. Solo hay un argumento de lista de valores en las funciones de catálogo de ODBC: el argumento *TableType* en **SQLTables**. Establecer *TableType* en un puntero nulo es el mismo que si se establece en SQL_ALL_TABLE_TYPES, que enumera todos los miembros posibles de la lista de valores. Este argumento no se ve afectado por el atributo de instrucción SQL_ATTR_METADATA_ID. Para obtener más información, vea la descripción de la función [SQLTables](../../../odbc/reference/syntax/sqltables-function.md) .
