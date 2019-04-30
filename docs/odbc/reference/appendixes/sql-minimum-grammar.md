---
title: Gramática mínima de SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
ms.assetid: 4f36d785-104f-4fec-93be-f201203bc7c7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 26cf76200010edae7f85993ec33eb3722f35e94e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63270496"
---
# <a name="sql-minimum-grammar"></a>Gramática mínima de SQL
Esta sección describe la sintaxis SQL mínima que debe admitir un controlador ODBC. La sintaxis descrita en esta sección es un subconjunto de la sintaxis de nivel de entrada de SQL-92.  
  
 Una aplicación puede usar cualquiera de la sintaxis de esta sección y estar seguro de que los controladores compatibles con ODBC admitirá esa sintaxis. Para determinar si se admiten las características adicionales de SQL-92 no en esta sección, la aplicación debe llamar a **SQLGetInfo** con el tipo de información SQL_SQL_CONFORMANCE. Incluso si el controlador no se ajusta a cualquier nivel de conformidad con SQL-92, una aplicación todavía puede usar la sintaxis descrita en esta sección. Si un controlador es compatible con un nivel de SQL-92, por otro lado, admite toda la sintaxis incluida en ese nivel. Esto incluye la sintaxis de esta sección porque la gramática mínima que se describe aquí es un subconjunto puro del nivel más bajo de conformidad de SQL-92. Una vez que la aplicación sepa el nivel de SQL-92 admitido, puede determinar si una característica de nivel superior se admite (si existe) mediante una llamada a **SQLGetInfo** con el tipo de información individual correspondiente a esa característica.  
  
 Los controladores que solo funcionan con orígenes de datos de solo lectura podrían no admitir aquellas partes de la gramática que se incluyen en esta sección que tratan con datos que cambian. Una aplicación puede determinar si un origen de datos es de solo lectura mediante una llamada a **SQLGetInfo** con el tipo de información SQL_DATA_SOURCE_READ_ONLY.  
  
## <a name="statement"></a>.  
 *create-table-statement* ::=  
  
 CREATE TABLE *nombre de la tabla de base*  
  
 (*identificador de la columna de tipo de datos* [*, identificador de la columna de tipo de datos*]...)  
  
> [!IMPORTANT]  
>  Como un *tipo de datos* en un *instrucción create table*, las aplicaciones deben usar un tipo de datos de la columna TYPE_NAME del conjunto de resultados devuelto por **SQLGetTypeInfo**.  
  
 *delete-statement-searched* ::=  
  
 DELETE FROM *table-name* [WHERE *search-condition*]  
  
 *drop-table-statement* ::=  
  
 DROP TABLE *nombre de la tabla de base*  
  
 *insert-statement* ::=  
  
 INSERT INTO *nombre-tabla* [( *identificador de columna* [, *identificador de columna*]...)]      VALORES (*Insertar valor*[, *Insertar valor*]...)  
  
 *select-statement* ::=  
  
 Seleccione [todos los &#124; DISTINCT] *lista de selección*  
  
 DESDE *lista de referencias de tabla*  
  
 [Donde *condición de búsqueda*]  
  
 [*order-by-clause*]  
  
 *statement* ::= *create-table-statement*  
  
 &#124; *delete-statement-searched*  
  
 &#124; *drop-table-statement*  
  
 &#124; *insert-statement*  
  
 &#124; *select-statement*  
  
 &#124; *update-statement-searched*  
  
 *update-statement-searched*  
  
 ACTUALIZACIÓN *nombre de tabla*  
  
 ESTABLECER *identificador de columna* = {*expresión* &#124; NULL}  
  
 [, *column-identifier* = {*expression* &#124; NULL}]...  
  
 [Donde *condición de búsqueda*]  
  
 Esta sección contiene los temas siguientes.  
  
-   [Elementos que se usan en instrucciones SQL](../../../odbc/reference/appendixes/elements-used-in-sql-statements.md)  
  
-   [Compatibilidad con tipos de datos](../../../odbc/reference/appendixes/data-type-support.md)  
  
-   [Tipos de datos de parámetro](../../../odbc/reference/appendixes/parameter-data-types.md)  
  
-   [Marcadores de parámetros](../../../odbc/reference/appendixes/parameter-markers.md)
