---
title: Las instrucciones INSERT, DELETE y UPDATE | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 92fb7b0e9722c52c7f1e9fc071d434f531b2fc46
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47721913"
---
# <a name="update-delete-and-insert-statements"></a>Las instrucciones INSERT, DELETE y UPDATE
Las aplicaciones basadas en SQL realizar cambios en las tablas mediante la ejecución de la **actualización**, **eliminar**, y **insertar** instrucciones. Estas instrucciones forman parte del nivel de conformidad de gramática mínima de SQL y deben ser compatibles con todos los controladores y orígenes de datos.  
  
 Es la sintaxis de estas instrucciones:  
  
 **ACTUALIZACIÓN***nombre de tabla*   
  
 **ESTABLECER** *identificador de columna* **=** {*expresión* &#124; **NULL**}  
  
 [**,** *identificador de columna* **=** {*expresión* &#124; **NULL**}]...  
  
 [**Donde** *condición de búsqueda*]  
  
 **DELETE FROM** *nombre-tabla*[**donde** *condición de búsqueda*]  
  
 **INSERT INTO** *nombre-tabla*[**(*** identificador de columna* [**,** *identificador de columna*]... **)**]  
  
 {*especificación de consulta* &#124;  **valores (*** Insertar valor* [**,** *Insertar valor*]... **)**}  
  
 Tenga en cuenta que el *especificación de consulta* elemento es válido solo en las gramáticas de Core y SQL extendido y que la *expresión* y *condición de búsqueda* elementos se convierten en más complejas en las gramáticas de Core y SQL extendido.  
  
 Al igual que otras instrucciones SQL, **actualización**, **eliminar**, y **insertar** instrucciones suelen ser más eficaces cuando se usan parámetros. Por ejemplo, la siguiente instrucción puede preparada y se ejecuta varias veces para insertar varias filas en la tabla Orders:  
  
```  
INSERT INTO Orders (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 Esta eficiencia puede aumentarse al pasar matrices de valores de parámetro. Para obtener más información acerca de los parámetros de la instrucción y matrices de valores de parámetros, vea [parámetros de la instrucción](../../../odbc/reference/develop-app/statement-parameters.md).
