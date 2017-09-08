---
title: OPENXML (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OPENXML_TSQL
- OPENXML
dev_langs:
- TSQL
helpviewer_keywords:
- OPENXML statement
- rowsets [SQL Server], XML documents
- XML [SQL Server], rowset views
ms.assetid: 8088b114-7d01-435a-8e0d-b81abacc86d6
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ff4578d88cdb76468d261843c36043ef4696d92c
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="openxml-transact-sql"></a>OPENXML (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  OPENXML proporciona una vista de un conjunto de filas en un documento XML. Puesto que OPENXML es un proveedor de conjuntos de filas, puede utilizarse en instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] en las que pueden aparecer proveedores de conjuntos de filas como una tabla, vista o la función OPENROWSET.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
OPENXML( idoc int [ in] , rowpattern nvarchar [ in ] , [ flags byte [ in ] ] )   
[ WITH ( SchemaDeclaration | TableName ) ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *IDOC*  
 Es el identificador del documento de la representación interna de un documento XML. Se crea la representación interna de un documento XML mediante una llamada a **sp_xml_preparedocument**.  
  
 *rowpattern*  
 Es el patrón XPath utilizado para identificar los nodos (en el documento XML cuyo identificador se pasa en el *idoc* parámetro) a procesar como filas.  
  
 *marcas*  
 Indica la asignación que debe utilizarse entre los datos XML y el conjunto de filas relacional, y cómo debe llenarse la columna de desbordamiento; *marcas de* es un parámetro de entrada opcional y puede tener uno de los siguientes valores.  
  
|Valor del byte|Description|  
|----------------|-----------------|  
|**0**|Valor predeterminado es **centrada en atributos** asignación.|  
|**1**|Use la **centrada en atributos** asignación. Se puede combinar con XML_ELEMENTS. En este caso, **centrada en atributos** asignación se aplica en primer lugar y, a continuación, **centrado** se aplica la asignación para todas las columnas que no se ha trabajado con.|  
|**2**|Use la **centrado** asignación. Se puede combinar con XML_ATTRIBUTES. En este caso, **centrada en atributos** asignación se aplica en primer lugar y, a continuación, **centrado** se aplica la asignación para todas las columnas no han visto afectadas.|  
|**8**|Puede combinarse (OR lógico) con XML_ATTRIBUTES o XML_ELEMENTS. En el contexto de la recuperación, esta marca indica que los datos consumidos no deben copiarse a la propiedad de desbordamiento  **@mp:xmltext** .|  
  
 *SchemaDeclaration*  
 Es la definición de esquema de la forma: *ColName**ColType* [*ColPattern* | *metapropiedad*] [**** *ColNameColType* [*ColPattern* | *metapropiedad*]...]  
  
 *ColName*  
 Es el nombre de columna en el conjunto de filas.  
  
 *ColType*  
 Es el tipo de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de la columna en el conjunto de filas. Si difieren de los tipos de columna de subyacente **xml** se produce el tipo de datos del atributo, la conversión de tipos.  
  
 *ColPattern*  
 Es un parámetro opcional, un patrón XPath general que describe la forma de asignar los nodos XML a las columnas. Si *ColPattern* no se especifica, la asignación predeterminada (**centrada en atributos** o **centrado** asignar tal y como especifica *marcas* ) tiene lugar.  
  
 El patrón XPath especificado como *ColPattern* se utiliza para especificar la naturaleza especial de la asignación (en el caso de **centrada en atributos** y **centrado** asignación) que sobrescribe o mejora la asignación predeterminada indicada en *marcas*.  
  
 El patrón XPath general especificado como *ColPattern* también admite las metapropiedades.  
  
 *Metapropiedades*  
 Es una de las metapropiedades que proporciona OPENXML. Si *metapropiedad* se especifica, la columna contiene la información proporcionada por la metapropiedad. Las metapropiedades permiten extraer información (como información sobre el espacio de nombres y la posición relativa) acerca de nodos XML. Esto proporciona más información que la que se puede ver en la representación de texto.  
  
 *Nombre de tabla*  
 Es el nombre de tabla que puede proporcionarse (en lugar de *SchemaDeclaration*) si ya existe una tabla con el esquema deseado y ningún patrón de columna es necesarios.  
  
## <a name="remarks"></a>Comentarios  
 La cláusula WITH proporciona un formato de conjunto de filas (e información de asignación adicionales según sea necesario) mediante el uso *SchemaDeclaration* o especificando una existente *TableName*. Si no se especifica la cláusula opcional WITH, los resultados se devuelven en un **borde** formato de tabla. Las tablas irregulares representan la estructura refinada del documento XML (por ejemplo, los nombres de elementos o atributos, la jerarquía del documento, los espacios de nombre, las instrucciones de proceso, etc.) en una única tabla.  
  
 En la tabla siguiente describe la estructura de la **borde** tabla.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**id**|**bigint**|Es el id. único del nodo del documento.<br /><br /> El elemento raíz tiene un valor de identificador 0. Los valores de identificador negativos están reservados.|  
|**parentid**|**bigint**|Identifica el elemento primario del nodo. El elemento primario especificado por este identificador no es necesariamente el elemento primario, pero depende del NodeType del nodo cuyo elemento primario indica este identificador. Por ejemplo, si se trata de un nodo de texto, su elemento primario puede ser un nodo de atributo.<br /><br /> Si el nodo está en el nivel superior del documento XML, su **ParentID** es NULL.|  
|**NodeType**|**int**|Identifica el tipo de nodo. Es un entero que se corresponde con la numeración del tipo de nodo XML DOM.<br /><br /> Los tipos de nodo son:<br /><br /> 1 = Nodo de elemento<br /><br /> 2 = Nodo de atributo<br /><br /> 3 = Nodo de texto|  
|**localname**|**nvarchar**|Proporciona el nombre local del elemento o atributo. Es NULL si el objeto DOM no tiene nombre.|  
|**prefijo**|**nvarchar**|Es el prefijo del espacio del nombre del nodo.|  
|**namespaceuri**|**nvarchar**|Es el URI del espacio de nombres del nodo. Si el valor es NULL, no hay ningún espacio de nombres.|  
|**datatype**|**nvarchar**|Es el tipo de datos reales de la fila del elemento o atributo y, en caso contrario, es NULL. El tipo de datos se infiere a partir de las DTD insertadas o del esquema insertado.|  
|**prev**|**bigint**|Es el id. XML del anterior elemento del mismo nivel. Es NULL si no existe ningún elemento previo directo del mismo nivel.|  
|**texto**|**ntext**|Contiene el valor del atributo o el contenido del elemento en formato de texto (o es NULL si el **borde** entrada de la tabla no requiere un valor).|  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-a-simple-select-statement-with-openxml"></a>A. Usar una instrucción SELECT simple con OPENXML  
 En el siguiente ejemplo se crea una representación interna de la imagen XML utilizando `sp_xml_preparedocument`. A continuación se ejecuta una instrucción `SELECT` que usa un proveedor del conjunto de filas `OPENXML` contra la representación interna del documento XML.  
  
 El *marca* valor se establece en `1`. Esto indica **centrada en atributos** asignación. Por tanto, los atributos XML se asignan a las columnas del conjunto de filas. El *rowpattern* especificado como `/ROOT/Customer` identifica el `<Customers>` nodos para procesarse.  
  
 Opcional *ColPattern* parámetro (patrón de columna) no se especifica porque el nombre de columna coincide con los nombres de atributo XML.  
  
 El proveedor del conjunto de filas `OPENXML` crea un conjunto de filas de 2 columnas (`CustomerID` y `ContactName`) desde el que la instrucción `SELECT` recupera las columnas necesarias (en este caso, todas las columnas).  
  
```  
DECLARE @idoc int, @doc varchar(1000);  
SET @doc ='  
<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order CustomerID="VINET" EmployeeID="5" OrderDate="1996-07-04T00:00:00">  
      <OrderDetail OrderID="10248" ProductID="11" Quantity="12"/>  
      <OrderDetail OrderID="10248" ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Order CustomerID="LILAS" EmployeeID="3" OrderDate="1996-08-16T00:00:00">  
      <OrderDetail OrderID="10283" ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>';  
--Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @idoc OUTPUT, @doc;  
-- Execute a SELECT statement that uses the OPENXML rowset provider.  
SELECT    *  
FROM       OPENXML (@idoc, '/ROOT/Customer',1)  
            WITH (CustomerID  varchar(10),  
                  ContactName varchar(20));  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
CustomerID ContactName            
---------- --------------------   
VINET      Paul Henriot  
LILAS      Carlos Gonzlez  
```  
  
 Si el mismo `SELECT` instrucción se ejecuta con *marcas* establecido en `2`, lo que indica **centrado** asignación, los valores de `CustomerID` y `ContactName` para ambos de la los clientes en el documento XML se devuelven como NULL, porque no hay ningún elemento con el nombre `CustomerID` o `ContactName` en el documento XML.  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
CustomerID ContactName  
---------- -----------  
NULL       NULL  
NULL       NULL  
```  
  
### <a name="b-specifying-colpattern-for-mapping-between-columns-and-the-xml-attributes"></a>B. Especificar ColPattern para la asignación entre columnas y los atributos XML  
 En la siguiente consulta se devuelven los atributos de CustomerID, OrderDate, ProductID y Quantity del documento XML. El *rowpattern* identifica el `<OrderDetails>` elementos. `ProductID` y `Quantity` son los atributos del elemento `<OrderDetails>`. No obstante, `OrderID`, `CustomerID` y `OrderDate` son los atributos del elemento primario (`<Orders>`).  
  
 Opcional *ColPattern* se especifica. Indica lo siguiente:  
  
-   El `OrderID`, `CustomerID`, y `OrderDate` el conjunto de filas se asignan a los atributos del elemento primario de los nodos identificados por *rowpattern* en el documento XML.  
  
-   El `ProdID` columna del conjunto de filas se asigna a la `ProductID` atributo y el `Qty` columna del conjunto de filas se asigna a la `Quantity` atributos de los nodos identificados en *rowpattern*.  
  
 Aunque la **centrado** asignación especificada por el *marcas* parámetro, la asignación especificada en *ColPattern* sobrescribe esta asignación.  
  
```  
DECLARE @idoc int, @doc varchar(1000);   
SET @doc ='  
<ROOT>  
<Customer CustomerID="VINET" ContactName="Paul Henriot">  
   <Order OrderID="10248" CustomerID="VINET" EmployeeID="5"   
           OrderDate="1996-07-04T00:00:00">  
      <OrderDetail ProductID="11" Quantity="12"/>  
      <OrderDetail ProductID="42" Quantity="10"/>  
   </Order>  
</Customer>  
<Customer CustomerID="LILAS" ContactName="Carlos Gonzlez">v  
   <Order OrderID="10283" CustomerID="LILAS" EmployeeID="3"   
           OrderDate="1996-08-16T00:00:00">  
      <OrderDetail ProductID="72" Quantity="3"/>  
   </Order>  
</Customer>  
</ROOT>';   
  
--Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @idoc OUTPUT, @doc;   
  
-- SELECT stmt using OPENXML rowset provider  
SELECT *  
FROM   OPENXML (@idoc, '/ROOT/Customer/Order/OrderDetail',2)   
         WITH (OrderID       int         '../@OrderID',   
               CustomerID  varchar(10) '../@CustomerID',   
               OrderDate   datetime    '../@OrderDate',   
               ProdID      int         '@ProductID',   
               Qty         int         '@Quantity');  
  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
OrderID CustomerID           OrderDate                 ProdID    Qty  
------------------------------------------------------------------------  
10248      VINET       1996-07-04 00:00:00.000   11      12  
10248      VINET       1996-07-04 00:00:00.000   42      10  
10283      LILAS       1996-08-16 00:00:00.000   72      3  
```  
  
### <a name="c-obtaining-results-in-an-edge-table-format"></a>C. Obtener resultados en formato de tabla irregular  
 El documento XML del ejemplo siguiente está formado por los elementos `<Customers>`, `<Orders>` y `<Order_0020_Details>`. En primer lugar, **sp_xml_preparedocument** para obtener un identificador de documento se llama. Este identificador de documentos se pasa a `OPENXML`.  
  
 En el `OPENXML` (instrucción), el *rowpattern* (`/ROOT/Customers`) identifica los `<Customers>` nodos que se va a procesar. Dado que no se proporciona la cláusula WITH, `OPENXML` devuelve el conjunto de filas en una **borde** formato de tabla.  
  
 Por último, el `SELECT` instrucción recupera todas las columnas de la **borde** tabla.  
  
```  
DECLARE @idoc int, @doc varchar(1000);   
SET @doc ='  
<ROOT>  
<Customers CustomerID="VINET" ContactName="Paul Henriot">  
   <Orders CustomerID="VINET" EmployeeID="5" OrderDate=  
           "1996-07-04T00:00:00">  
      <Order_x0020_Details OrderID="10248" ProductID="11" Quantity="12"/>  
      <Order_x0020_Details OrderID="10248" ProductID="42" Quantity="10"/>  
   </Orders>  
</Customers>  
<Customers CustomerID="LILAS" ContactName="Carlos Gonzlez">  
   <Orders CustomerID="LILAS" EmployeeID="3" OrderDate=  
           "1996-08-16T00:00:00">  
      <Order_x0020_Details OrderID="10283" ProductID="72" Quantity="3"/>  
   </Orders>  
</Customers>  
</ROOT>';  
  
--Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @idoc OUTPUT, @doc;   
  
-- SELECT statement that uses the OPENXML rowset provider.  
SELECT    *  
FROM       OPENXML (@idoc, '/ROOT/Customers')   
EXEC sp_xml_removedocument @idoc;  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Ejemplos: Usar OPENXML](../../relational-databases/xml/examples-using-openxml.md)  
  
  
