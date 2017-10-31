---
title: "Instrucción ALTER INDEX (índices XML selectivos) | Documentos de Microsoft"
ms.custom: 
ms.date: 05/01/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: cca96a8f-7737-42d2-bbcc-03d5f858dcc1
caps.latest.revision: 13
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e7854dd1d9365f97628341c4160c368f97308302
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="alter-index-selective-xml-indexes"></a>ALTER INDEX (índices XML selectivos)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Modifica un índice XML selectivo existente. La instrucción ALTER INDEX cambia uno o varios de los elementos siguientes:  
  
-   La lista de rutas de acceso indizadas (cláusula FOR).  
  
-   La lista de espacios de nombres (cláusula WITH XMLNAMESPACES).  
  
-   Las opciones de índice (cláusula WITH).  
  
 No puede modificar índices XML selectivos secundarios. Para obtener más información, consulte [Create, Alter y Drop secundaria los índices XML selectivos](../../relational-databases/xml/create-alter-and-drop-secondary-selective-xml-indexes.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
ALTER INDEX index_name  
    ON <table_object>   
    [WITH XMLNAMESPACES ( <xmlnamespace_list> )]  
    FOR ( <promoted_node_path_action_list> )  
    [WITH ( <index_options> )]  
  
<table_object> ::=   
{ [database_name. [schema_name ] . | schema_name. ] table_name }  
<promoted_node_path_action_list> ::=   
<promoted_node_path_action_item> [, <promoted_node_path_action_list>]  
  
<promoted_node_path_action_item>::=   
<add_node_path_item_action> | <remove_node_path_item_action>  
  
<add_node_path_item_action> ::=  
ADD <path_name> = <promoted_node_path_item>  
  
<promoted_node_path_item>::=  
<xquery_node_path_item> | <sql_values_node_path_item>  
  
<remove_node_path_item_action> ::= REMOVE <path_name>   
  
<path_name_or_typed_node_path>::=   
<path_name> | <typed_node_path>  
  
<typed_node_path> ::=   
<node_path> [[AS XQUERY <xsd_type_ext>] | [AS SQL <sql_type>]]  
  
<xquery_node_path_item> ::=   
<node_path> [AS XQUERY <xsd_type_or_node_hint>] [SINGLETON]  
  
<xsd_type_or_node_hint> ::=   
[<xsd_type>] [MAXLENGTH(x)] | 'node()'  
  
<sql_values_node_path_item> ::=   
<node_path> AS SQL <sql_type> [SINGLETON]  
  
<node_path> ::=   
character_string_literal  
  
<xsd_type_ext> ::=   
character_string_literal  
  
<sql_type> ::=   
identifier  
  
<path_name> ::=   
identifier  
  
<xmlnamespace_list> ::=   
<xmlnamespace_item> [, <xmlnamespace_list>]  
  
<xmlnamespace_item> ::=   
<xmlnamespace_uri> AS <xmlnamespace_prefix>  
  
<xml_namespace_uri> ::= character_string_literal  
<xml_namespace_prefix> ::= identifier  
  
<index_options> ::=   
(   
  | PAD_INDEX  = { ON | OFF }  
  | FILLFACTOR = fillfactor  
  | SORT_IN_TEMPDB = { ON | OFF }  
  | IGNORE_DUP_KEY =OFF  
  | DROP_EXISTING = { ON | OFF }  
  | ONLINE =OFF  
  | ALLOW_ROW_LOCKS = { ON | OFF }  
  | ALLOW_PAGE_LOCKS = { ON | OFF }  
  | MAXDOP = max_degree_of_parallelism  
)  
```  
  
##  <a name="Arguments"></a> Argumentos  
 *index_name*  
 Es el nombre del índice existente que se va a modificar.  
  
 *\<table_object >*  
 Es la tabla que contiene la columna XML que se va a indizar. Use uno de los formatos siguientes:  
  
-   `database_name.schema_name.table_name`  
  
-   `database_name..table_name`  
  
-   `schema_name.table_name`  
  
-   `table_name`  
  
 [WITH XMLNAMESPACES **(** \<xmlnamespace_list > **)**]  
 Es la lista de espacios de nombres usados por las rutas de acceso que se van a indizar. Para obtener información acerca de la sintaxis de la cláusula WITH XMLNAMESPACES, vea [WITH XMLNAMESPACES &#40; Transact-SQL &#41; ](../../t-sql/xml/with-xmlnamespaces.md).  
  
 PARA **(** \<promoted_node_path_action_list > **)**  
 Es la lista de rutas de acceso indizadas que se van a agregar o quitar.  
  
-   **Agregue una ruta de acceso.** Cuando se agrega (con ADD) una ruta de acceso, se emplea la misma sintaxis que se usa para crear rutas de acceso con la instrucción CREATE SELECTIVE XML INDEX. Para obtener información acerca de las rutas de acceso que se pueden especificar en la instrucción CREATE o ALTER, vea [especificar rutas de acceso y las sugerencias de optimización para índices XML selectivos](../../relational-databases/xml/specify-paths-and-optimization-hints-for-selective-xml-indexes.md).  
  
-   **QUITAR una ruta de acceso.** Cuando se quita (con REMOVE) una ruta de acceso, debe proporcionar el nombre especificado para la ruta de acceso cuando se creó.  
  
 [Con **(** \<index_options > **)**]  
 Solo se puede especificar \<index_options > cuando se usa ALTER INDEX con la cláusula FOR. Cuando se usa ALTER INDEX para agregar o quitar rutas de acceso del índice, las opciones de índice no son argumentos válidos. Para obtener información acerca de las opciones de índice, vea [CREATE XML INDEX &#40; Índices XML selectivos &#41; ](../../t-sql/statements/create-xml-index-selective-xml-indexes.md).  
  
## <a name="remarks"></a>Comentarios  
  
> [!IMPORTANT]  
>  Al ejecutar una instrucción ALTER INDEX, siempre se vuelve a generar el índice XML selectivo. Debe tener en cuenta el impacto de este proceso sobre los recursos de servidor.  
  
## <a name="security"></a>Seguridad  
  
### <a name="permissions"></a>Permissions  
 Se necesita el permiso ALTER en la tabla o la vista para poder ejecutar ALTER INDEX.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se muestra una instrucción ALTER INDEX. Esta instrucción agrega la ruta de acceso `'/a/b/m'` a la parte XQuery del índice y elimina la ruta de acceso `'/a/b/e'` de la parte SQL del índice creado en el ejemplo del tema [CREATE SELECTIVE XML INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-selective-xml-index-transact-sql.md). La ruta de acceso que se va a eliminar se identifica por el nombre que se especificó cuando se creó.  
  
```tsql  
ALTER INDEX sxi_index  
ON Tbl  
FOR   
(  
    ADD pathm = '/a/b/m' as XQUERY 'node()' ,  
    REMOVE pathabe  
);  
```  
  
 En el ejemplo siguiente se muestra una instrucción ALTER INDEX que especifica opciones de índice. Se permiten opciones de índice porque la instrucción no usa una cláusula FOR para agregar o quitar rutas de acceso.  
  
```tsql  
ALTER INDEX sxi_index  
ON Tbl  
PAD_INDEX = ON;  
```  
  
## <a name="see-also"></a>Vea también  
 [Índices XML selectivos &#40;SXI&#41;](../../relational-databases/xml/selective-xml-indexes-sxi.md)   
 [Crear, modificar y quitar índices XML selectivos](../../relational-databases/xml/create-alter-and-drop-selective-xml-indexes.md)   
 [Especificar rutas de acceso y sugerencias de optimización para índices XML selectivos](../../relational-databases/xml/specify-paths-and-optimization-hints-for-selective-xml-indexes.md)  
  
  

