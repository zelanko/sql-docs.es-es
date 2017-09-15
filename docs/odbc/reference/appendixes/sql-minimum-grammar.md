---
title: "La gramática mínima de SQL | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
ms.assetid: 4f36d785-104f-4fec-93be-f201203bc7c7
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c225ab76f4c67938590bd19f21bfafafa20742d8
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sql-minimum-grammar"></a>Gramática mínima de SQL
Esta sección describe la sintaxis SQL mínima que debe ser compatible con un controlador ODBC. La sintaxis descrita en esta sección es un subconjunto de la sintaxis de nivel de entrada de SQL-92.  
  
 Una aplicación puede usar cualquiera de la sintaxis de esta sección y estar seguro de que cualquier controlador compatible con ODBC admite esta sintaxis. Para determinar si se admiten las características adicionales de SQL-92 no estén en esta sección, la aplicación debe llamar a **SQLGetInfo** con el tipo de información de SQL_SQL_CONFORMANCE. Incluso si el controlador no se ajusta a cualquier nivel de conformidad de SQL-92, una aplicación todavía puede utilizar la sintaxis descrita en esta sección. Si un controlador es compatible con un nivel de SQL-92, por otro lado, admite toda la sintaxis incluida en ese nivel. Esto incluye la sintaxis de esta sección porque la gramática mínima que se describe aquí es un subconjunto puro del nivel más bajo de conformidad de SQL-92. Una vez que la aplicación sepa el nivel de SQL-92 admitido, puede determinar si una característica de nivel superior se admite (si existe) mediante una llamada a **SQLGetInfo** con el tipo de información individual correspondiente a esa característica.  
  
 Controladores que solo funcionan con orígenes de datos de solo lectura podrían no admitir las partes de la gramática que se incluyen en esta sección que tratan con datos que cambian. Una aplicación puede determinar si un origen de datos es de solo lectura mediante una llamada a **SQLGetInfo** con el tipo de información de SQL_DATA_SOURCE_READ_ONLY.  
  
## <a name="statement"></a>.  
 *instrucción CREATE table* :: =  
  
 CREATE TABLE *nombre de la tabla de base*  
  
 (*identificador de la columna de tipo de datos* [*, tipo de datos del identificador de la columna*]...)  
  
> [!IMPORTANT]  
>  Como un *tipo de datos* en un *instrucción create table*, las aplicaciones deben utilizar un tipo de datos de la columna TYPE_NAME del conjunto de resultados devuelto por **SQLGetTypeInfo**.  
  
 *busca en la instrucción de eliminación* :: =  
  
 DELETE FROM *nombre de la tabla* [donde *condición de búsqueda*]  
  
 *instrucción de tabla DROP* :: =  
  
 DROP TABLE *nombre de la tabla de base*  
  
 *instrucción INSERT* :: =  
  
 INSERT INTO *nombre de la tabla* [( *identificador de la columna* [, *identificador de la columna*]...)]      VALORES (*valor de inserción*[, *valor de inserción*]...)  
  
 *instrucción SELECT* :: =  
  
 Seleccione [todas las &#124; DISTINCT] *lista de selección*  
  
 DESDE *lista de referencias de tabla*  
  
 [Donde *condición de búsqueda*]  
  
 [*cláusula order by*]  
  
 *instrucción* :: = *instrucción create table*  
  
 &#124; *busca en la instrucción de eliminación*  
  
 &#124; *declaración de tabla de destino*  
  
 &#124; *instrucción insert*  
  
 &#124; *instrucción select*  
  
 &#124; *búsquedas en la instrucción update*  
  
 *búsquedas en la instrucción Update*  
  
 ACTUALIZACIÓN *nombre de la tabla*  
  
 ESTABLECER *identificador de la columna* = {*expresión* &#124; NULL}  
  
 [, *identificador de la columna* = {*expresión* &#124; NULL}]...  
  
 [Donde *condición de búsqueda*]  
  
 Esta sección contiene los temas siguientes.  
  
-   [Elementos que se usan en instrucciones SQL](../../../odbc/reference/appendixes/elements-used-in-sql-statements.md)  
  
-   [Compatibilidad con tipos de datos](../../../odbc/reference/appendixes/data-type-support.md)  
  
-   [Tipos de datos de parámetro](../../../odbc/reference/appendixes/parameter-data-types.md)  
  
-   [Marcadores de parámetros](../../../odbc/reference/appendixes/parameter-markers.md)
