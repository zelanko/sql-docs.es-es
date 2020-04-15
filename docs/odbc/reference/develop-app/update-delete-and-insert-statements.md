---
title: Actualizar, ELIMINAR e INSERTAR Instrucciones ( UPDATE, DELETE, and INSERT Statements) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], about updating data
- DELETE [ODBC]
- UPDATE [ODBC]
- INSERT [ODBC]
- data updates [ODBC], about data updates
ms.assetid: 5004ea72-4c49-4064-9752-f7032ba7f133
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f12682a5d012d6981afce0085e9c920ed2f2ffbc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284265"
---
# <a name="update-delete-and-insert-statements"></a>Las instrucciones INSERT, DELETE y UPDATE
Las aplicaciones basadas en SQL realizan cambios en las tablas ejecutando las instrucciones **UPDATE**, **DELETE**e **INSERT.** Estas instrucciones forman parte del nivel de conformidad de gramática SQL mínima y deben ser compatibles con todos los controladores y orígenes de datos.  
  
 La sintaxis de estas sentencias es:  
  
 **ACTUALIZAR** _nombre-tabla_  
  
 **SET** _column-identifier_ **=** -*expresión* &#124; **NULL**?  
  
 [**,** _identificador de columna_ **=** ,*expresión* &#124; **NULL]...**  
  
 [**DONDE estado** _de búsqueda_]  
  
 **ELIMINAR EL** _nombre de la tabla_[**WHERE** _search-condition_]  
  
 **INSERT INTO** _nombre-tabla_[**(** identificador _de columna_ [**,** identificador _de columna_]... **)**]  
  
 •*especificación de consulta* &#124; VALUES **(** _insert-value_ [**,** _insert-value_]... **)**}  
  
 Tenga en cuenta que el elemento *query-specification* solo es válido en las gramáticas Core y Extended SQL, y que los elementos *expression* y *search-condition* se vuelven más complejos en las gramáticas Core y Extended SQL.  
  
 Al igual que otras instrucciones SQL, las instrucciones **UPDATE**, **DELETE**e **INSERT** suelen ser más eficaces cuando utilizan parámetros. Por ejemplo, la siguiente instrucción se puede preparar y ejecutar repetidamente para insertar varias filas en la tabla Orders:  
  
```  
INSERT INTO Orders (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 Esta eficiencia se puede aumentar pasando matrices de valores de parámetro. Para obtener más información acerca de los parámetros de instrucción y matrices de valores de parámetro, vea Parámetros de [instrucción](../../../odbc/reference/develop-app/statement-parameters.md).
