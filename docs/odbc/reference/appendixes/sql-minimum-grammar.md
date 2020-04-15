---
title: Gramática mínima de SQL ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 20eee34feadb8e3140f25019ec6b0d036ff02e14
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304996"
---
# <a name="sql-minimum-grammar"></a>Gramática mínima de SQL
En esta sección se describe la sintaxis SQL mínima que debe admitir un controlador ODBC. La sintaxis descrita en esta sección es un subconjunto de la sintaxis de nivel de entrada de SQL-92.  
  
 Una aplicación puede usar cualquiera de la sintaxis de esta sección y estar seguro de que cualquier controlador compatible con ODBC admitirá esa sintaxis. Para determinar si se admiten características adicionales de SQL-92 no en esta sección, la aplicación debe llamar a **SQLGetInfo** con el tipo de información SQL_SQL_CONFORMANCE. Incluso si el controlador no se ajusta a ningún nivel de conformidad de SQL-92, una aplicación todavía puede utilizar la sintaxis descrita en esta sección. Si un controlador se ajusta a un nivel SQL-92, por otro lado, admite toda la sintaxis incluida en ese nivel. Esto incluye la sintaxis de esta sección porque la gramática mínima que se describe aquí es un subconjunto puro del nivel de conformidad SQL-92 más bajo. Una vez que la aplicación conoce el nivel de SQL-92 admitido, puede determinar si se admite una característica de nivel superior (si existe) llamando a **SQLGetInfo** con el tipo de información individual correspondiente a esa característica.  
  
 Es posible que los controladores que solo funcionan con orígenes de datos de solo lectura no admitan las partes de la gramática incluidas en esta sección que tratan sobre el cambio de datos. Una aplicación puede determinar si un origen de datos es de solo lectura mediante una llamada a **SQLGetInfo** con el tipo de información SQL_DATA_SOURCE_READ_ONLY.  
  
## <a name="statement"></a>.  
 *create-table-statement* ::  
  
 CREATE TABLE *base-table-name*  
  
 (*tipo de datos de identificador de columna* [*,tipo de datos de identificador de columna*]...)  
  
> [!IMPORTANT]  
>  Como *tipo de datos* en una *instrucción create-table ,* las aplicaciones deben usar un tipo de datos de la columna TYPE_NAME del conjunto de resultados devuelto por **SQLGetTypeInfo**.  
  
 *delete-statement-searched* ::  
  
 DELETE FROM *nombre-tabla* [WHERE *search-condition*]  
  
 *drop-table-statement* ::  
  
 DROP TABLE *base-table-name*  
  
 *insert-statement* ::  
  
 INSERT INTO *nombre-tabla* [( *identificador de columna* [, identificador de *columna*]...)]      VALUES (*insert-value*[, *insert-value*]... )  
  
 *select-statement* ::=  
  
 SELECT [ALL &#124; DISTINCT] *select-list*  
  
 FROM *tabla-referencia-lista*  
  
 [WHERE *search-condition*]  
  
 [*orden por cláusula*]  
  
 *declaración* ::- *create-table-statement*  
  
 &#124; *de búsqueda de la declaración de eliminación*  
  
 &#124; *drop-table-statement*  
  
 &#124; *insértese*  
  
 &#124; *select-statement*  
  
 &#124; *update-statement-searched*  
  
 *update-statement-searched*  
  
 ACTUALIZAR *nombre-tabla*  
  
 SET *column-identifier* á -*expresión* &#124; NULL ?  
  
 [, *identificador de columna:* *expresión* &#124; NULL]...  
  
 [WHERE *search-condition*]  
  
 Esta sección contiene los temas siguientes.  
  
-   [Elementos que se usan en instrucciones SQL](../../../odbc/reference/appendixes/elements-used-in-sql-statements.md)  
  
-   [Compatibilidad con tipos de datos](../../../odbc/reference/appendixes/data-type-support.md)  
  
-   [Tipos de datos de parámetro](../../../odbc/reference/appendixes/parameter-data-types.md)  
  
-   [Marcadores de parámetros](../../../odbc/reference/appendixes/parameter-markers.md)
