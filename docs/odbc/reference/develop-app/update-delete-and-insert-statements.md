---
title: Las instrucciones INSERT, DELETE y UPDATE | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- updating data [ODBC], about updating data
- DELETE [ODBC]
- UPDATE [ODBC]
- INSERT [ODBC]
- data updates [ODBC], about data updates
ms.assetid: 5004ea72-4c49-4064-9752-f7032ba7f133
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1b590f45a6cb7bb3e80b5b52835bd7fd65ba27af
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="update-delete-and-insert-statements"></a>Las instrucciones INSERT, DELETE y UPDATE
Las aplicaciones basadas en SQL realizan cambios en las tablas mediante la ejecución de la **actualización**, **eliminar**, y **insertar** instrucciones. Estas instrucciones son parte del nivel de conformidad de gramática mínima de SQL y deben ser compatibles con todos los controladores y orígenes de datos.  
  
 Es la sintaxis de estas instrucciones:  
  
 **ACTUALIZACIÓN***nombre de la tabla*  
  
 **ESTABLECER** *identificador de la columna* **=** {*expresión* &#124; **NULL**}  
  
 [**,** *identificador de la columna* **=** {*expresión* &#124; **NULL**}]...  
  
 [**Donde** *condición de búsqueda*]  
  
 **DELETE FROM** *nombre de la tabla*[**donde** *condición de búsqueda*]  
  
 **INSERT INTO** *nombre de la tabla*[**(*** identificador de la columna* [**,** *identificador de la columna*]... **)**]  
  
 {*especificación de consulta* &#124;  **valores (*** insert valor* [**,** *valor de inserción*]... **)**}  
  
 Tenga en cuenta que la *especificación de consulta* elemento solo es válido en las gramáticas extendida de SQL y Core y que la *expresión* y *condición de búsqueda* elementos se convierten en más complejo de las gramáticas principal y extendida de SQL.  
  
 Al igual que otras instrucciones SQL, **actualización**, **eliminar**, y **insertar** instrucciones suelen ser más eficaces cuando se usan parámetros. Por ejemplo, la siguiente instrucción puede preparada y se ejecuta varias veces para insertar varias filas en la tabla Orders:  
  
```  
INSERT INTO Orders (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 Esta eficacia, basta con pasar matrices de valores de parámetro. Para obtener más información acerca de los parámetros de la instrucción y matrices de valores de parámetros, vea [parámetros de la instrucción](../../../odbc/reference/develop-app/statement-parameters.md).
