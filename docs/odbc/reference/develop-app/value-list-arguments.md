---
description: Argumentos de la lista de valores
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fd2f2e970ea94635cda0b43b741abfda1130645b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421419"
---
# <a name="value-list-arguments"></a>Argumentos de la lista de valores
Un argumento de lista de valores se compone de una lista de valores separados por comas que se usarán para la búsqueda de coincidencias. Solo hay un argumento de lista de valores en las funciones de catálogo de ODBC: el argumento *TableType* en **SQLTables**. Establecer *TableType* en un puntero nulo es el mismo que si se establece en SQL_ALL_TABLE_TYPES, que enumera todos los miembros posibles de la lista de valores. Este argumento no se ve afectado por el atributo de instrucción SQL_ATTR_METADATA_ID. Para obtener más información, vea la descripción de la función [SQLTables](../../../odbc/reference/syntax/sqltables-function.md) .
