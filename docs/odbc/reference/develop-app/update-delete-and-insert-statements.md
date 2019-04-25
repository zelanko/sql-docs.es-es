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
ms.openlocfilehash: 00732de7eca32dc8b2984fdda14163c77c66ad43
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62632483"
---
# <a name="update-delete-and-insert-statements"></a>Las instrucciones INSERT, DELETE y UPDATE
Las aplicaciones basadas en SQL realizar cambios en las tablas mediante la ejecución de la **actualización**, **eliminar**, y **insertar** instrucciones. Estas instrucciones forman parte del nivel de conformidad de gramática mínima de SQL y deben ser compatibles con todos los controladores y orígenes de datos.  
  
 Es la sintaxis de estas instrucciones:  
  
 **ACTUALIZACIÓN** _nombre de tabla_  
  
 **SET** _column-identifier_ **=** {*expression* &#124; **NULL**}  
  
 [**,** _column-identifier_ **=** {*expression* &#124; **NULL**}]...  
  
 [**Donde** _condición de búsqueda_]  
  
 **DELETE FROM** _nombre-tabla_[**donde** _condición de búsqueda_]  
  
 **INSERT INTO** _nombre-tabla_[**(** _identificador de columna_ [**,** _deidentificadordecolumna_]... **)**]  
  
 {*especificación de consulta* &#124; **valores (** _Insertar valor_ [**,** _Insertar valor_]... **)**}  
  
 Tenga en cuenta que el *especificación de consulta* elemento es válido solo en las gramáticas de Core y SQL extendido y que la *expresión* y *condición de búsqueda* elementos se convierten en más complejas en las gramáticas de Core y SQL extendido.  
  
 Al igual que otras instrucciones SQL, **actualización**, **eliminar**, y **insertar** instrucciones suelen ser más eficaces cuando se usan parámetros. Por ejemplo, la siguiente instrucción puede preparada y se ejecuta varias veces para insertar varias filas en la tabla Orders:  
  
```  
INSERT INTO Orders (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 Esta eficiencia puede aumentarse al pasar matrices de valores de parámetro. Para obtener más información acerca de los parámetros de la instrucción y matrices de valores de parámetros, vea [parámetros de la instrucción](../../../odbc/reference/develop-app/statement-parameters.md).
