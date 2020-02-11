---
title: Instrucciones UPDATE, DELETE e INSERT | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c2a2787be1bf44e1f214d396444a73b938acf7ce
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67942839"
---
# <a name="update-delete-and-insert-statements"></a>Las instrucciones INSERT, DELETE y UPDATE
Las aplicaciones basadas en SQL realizan cambios en las tablas mediante la ejecución de las instrucciones **Update**, **Delete**e **Insert** . Estas instrucciones forman parte del nivel mínimo de cumplimiento de la gramática de SQL y deben ser compatibles con todos los controladores y orígenes de datos.  
  
 La sintaxis de estas instrucciones es:  
  
 **Actualizar** _tabla-nombre_  
  
 **Establecer** _el identificador de columna_ **=** {*expresión* &#124; **null**}  
  
 [**,** _identificador de columna_ **=** {*expresión* &#124; **null**}]...  
  
 [**Where** _-condición de búsqueda_]  
  
 **Eliminar de** _TABLE-Name_[**Where** _Search-Condition_]  
  
 **Inserte en** _el nombre de tabla_[**(** _columna-identificador_ [**,** _columna-identificador_]... **)**]  
  
 {*especificación de consulta* &#124; **valores (** _Insert-Value_ [**,** _Insert-Value_]... **)**}  
  
 Tenga en cuenta que el elemento de *especificación de consultas* solo es válido en las gramáticas SQL básicas y extendidas, y que los elementos de la *expresión* y la *condición de búsqueda* son más complejos en las gramáticas de SQL básicas y extendidas.  
  
 Al igual que otras instrucciones SQL, las instrucciones **Update**, **Delete**e **Insert** suelen ser más eficaces cuando utilizan parámetros. Por ejemplo, la instrucción siguiente se puede preparar y ejecutar repetidamente para insertar varias filas en la tabla Orders:  
  
```  
INSERT INTO Orders (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 Esta eficacia se puede aumentar pasando matrices de valores de parámetro. Para obtener más información sobre los parámetros de instrucciones y las matrices de valores de parámetro, vea [parámetros de instrucción](../../../odbc/reference/develop-app/statement-parameters.md).
