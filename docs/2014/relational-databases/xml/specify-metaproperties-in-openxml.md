---
title: Especificar metapropiedades en OPENXML | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- overflow in XML document [SQL Server]
- metaproperties [XML in SQL Server]
- unconsumed data
- extracting information of XML nodes [SQL Server]
- OPENXML statement, metaproperties
ms.assetid: 29bfd1c6-3f9a-43c4-924a-53d438e442f4
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: af67d79616f2223f62998494122787460eaa3a41
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37193115"
---
# <a name="specify-metaproperties-in-openxml"></a>Especificar metapropiedades en OPENXML
  Los atributos de las metapropiedades de un documento XML son atributos que describen las propiedades de un elemento XML (como elemento, atributo o cualquier otro nodo DOM). Estos atributos no existen físicamente en el texto del documento XML. Sin embargo, OPENXML proporciona estas metapropiedades para todos los elementos XML. Estas metapropiedades permiten extraer información, como la posición local e información de espacio de nombres, de los nodos XML. Esta información ofrece más detalles de los que aparentemente hay en la representación textual.  
  
 Estas metapropiedades se pueden asignar a las columnas del conjunto de filas en una instrucción OPENXML mediante el parámetro *ColPattern* . Las columnas contendrán los valores de las metapropiedades a las que se asignan. Para obtener más información sobre la sintaxis de OPENXML, vea [OPENXML &#40;Transact-SQL&#41;](/sql/t-sql/functions/openxml-transact-sql).  
  
 Para tener acceso a los atributos de las metapropiedades, se proporciona un espacio de nombres específico de SQL Server. Este espacio de nombres, **urn:schemas-microsoft-com:xml-metaprop** , permite al usuario tener acceso a los atributos de las metapropiedades. Si se devuelve el resultado de una consulta OPENXML en un formato de tabla irregular, dicha tabla contiene una columna para cada atributo de metapropiedad, excepto para la metapropiedad **xmltext** .  
  
 Algunos de los atributos de metapropiedades se utilizan para el procesamiento. Por ejemplo, el atributo de metapropiedad **xmltext** se utiliza para controlar el desbordamiento. El control del desbordamiento se refiere a los datos no utilizados ni procesados del documento. Una de las columnas del conjunto de filas que se genera mediante OPENXML se puede identificar como la columna de desbordamiento. Para ello, la columna se asigna a la metapropiedad **xmltext** mediante el parámetro *ColPattern* . En ese caso, la columna recibirá los datos de desbordamiento. El parámetro *flags* determina si la columna contiene todo o solo los datos no utilizados.  
  
 La siguiente tabla muestra una lista de los atributos de las metapropiedades que posee cada elemento XML analizado. Se puede obtener acceso a estos atributos de las metapropiedades mediante el espacio de nombres **urn:schemas-microsoft-com:xml-metaprop**. Se descarta cualquier valor que el usuario establezca directamente en el documento XML mediante estas metapropiedades.  
  
> [!NOTE]  
>  No se puede hacer referencia a estas metapropiedades en ninguna navegación XPath.  
  
|Atributo de metapropiedad|Descripción|  
|----------------------------|-----------------|  
|**@mp:id**|Proporciona un identificador del nodo DOM generado por el sistema para todo el documento. Este Id. hace referencia al mismo nodo XML siempre y cuando no se vuelva a analizar el documento.<br /><br /> Si el Id. XML es **0** , significa que se trata de un elemento raíz. El Id. XML del elemento primario es NULL.|  
|**@mp:localname**|Almacena la parte local del nombre del nodo. Se utiliza con un prefijo y un URI del espacio de nombres para asignar nombres a los nodos de elemento o atributo.|  
|**@mp:namespaceuri**|Proporciona el URI del espacio de nombres del elemento actual. Si el valor de este atributo es NULL, no hay ningún espacio de nombres.|  
|**@mp:prefix**|Almacena el prefijo del espacio de nombres del nombre del elemento actual.<br /><br /> Si no hay ningún prefijo (NULL) y se proporciona un URI, significa que el espacio de nombres especificado es el espacio de nombres predeterminado. Si no se proporciona ningún URI, no se adjunta ningún espacio de nombres.|  
|**@mp:prev**|Almacena el nodo anterior relacionado con un nodo. Proporciona información sobre el orden de los elementos del documento.<br /><br /> **@mp:prev** contiene el Id. XML del nodo relacionado anterior que tiene el mismo elemento primario. Si un elemento está al principio de la lista de nodos relacionados, **@mp:prev** es NULL.|  
|**@mp:xmltext**|Se utiliza para el procesamiento. Se trata de la serialización textual del elemento y sus atributos, y de los subelementos, tal como se utiliza en el control de desbordamiento de OPENXML.|  
  
 Esta tabla muestra las propiedades adicionales que se proporcionan para los elementos primarios, que permiten recuperar información acerca de la jerarquía.  
  
|Atributo de metapropiedad Parent|Descripción|  
|-----------------------------------|-----------------|  
|**@mp:parentid**|Se corresponde con **../@mp:id**|  
|**@mp:parentlocalname**|Se corresponde con **../@mp:localname**|  
|**@mp:parentnamespacerui**|Se corresponde con **../@mp:namespaceuri**|  
|**@mp:parentprefix**|Se corresponde con **../@mp:prefix**|  
  
## <a name="examples"></a>Ejemplos  
 En los ejemplos siguientes se muestra cómo se utiliza OPENXML para crear distintas vistas de conjuntos de filas.  
  
### <a name="a-mapping-the-openxml-rowset-columns-to-the-metaproperties"></a>A. Asignar las columnas de conjunto de filas OPENXML a las metapropiedades  
 Este ejemplo utiliza OPENXML para crear una vista de conjunto de filas del documento XML de ejemplo. Concretamente, muestra cómo se pueden asignar los distintos atributos de metapropiedades a columnas de conjunto de filas en una instrucción OPENXML mediante el parámetro *ColPattern* .  
  
 La instrucción OPENXML muestra lo siguiente:  
  
-   El parámetro **id** se asigna al atributo de metapropiedad **@mp:id** e indica que la columna contiene el id. XML único del elemento, generado por el sistema.  
  
-   El parámetro **parent** se asigna a **@mp:parentid** e indica que la columna contiene el Id. XML del elemento primario del elemento.  
  
-   El parámetro **parentLocalName** se asigna a **@mp:parentlocalname** e indica que la columna contiene el nombre local del elemento primario.  
  
 Y, a continuación, la instrucción SELECT devuelve el conjunto de filas proporcionado por OPENXML.  
  
```  
DECLARE @idoc int  
DECLARE @doc nvarchar(1000)  
-- Sample XML document  
SET @doc = N'<root>  
  <Customer cid= "C1" name="Janine" city="Issaquah">  
      <Order oid="O1" date="1/20/1996" amount="3.5" />  
      <Order oid="O2" date="4/30/1997" amount="13.4">Customer was very satisfied</Order>  
   </Customer>  
   <Customer cid="C2" name="Ursula" city="Oelde" >  
      <Order oid="O3" date="7/14/1999" amount="100" note="Wrap it blue white red">  
          <Urgency>Important</Urgency>  
      </Order>  
      <Order oid="O4" date="1/20/1996" amount="10000"/>  
   </Customer>  
</root>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @idoc OUTPUT, @doc  
  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@idoc, '/root/Customer/Order', 9)  
      WITH (id int '@mp:id',   
            oid char(5),   
            date datetime,   
            amount real,   
            parentIDNo int '@mp:parentid',   
            parentLocalName varchar(40) '@mp:parentlocalname')  
EXEC sp_xml_removedocument @idoc  
```  
  
 El resultado es el siguiente:  
  
```  
id   oid         date                amount    parentIDNo  parentLocalName    
--- ------- ---------------------- ---------- ------------ ---------------  
6    O1    1996-01-20 00:00:00.000     3.5         2        Customer  
10   O2    1997-04-30 00:00:00.000     13.4        2        Customer  
19   O3    1999-07-14 00:00:00.000     100.0       15       Customer  
25   O4    1996-01-20 00:00:00.000     10000.0     15       Customer  
```  
  
### <a name="b-retrieving-the-whole-xml-document"></a>B. Recuperar todo el documento XML  
 En este ejemplo, se usa OPENXML para crear una vista de conjunto de filas de una columna del documento XML de ejemplo. Esta columna ( **Col1**) se asigna a la metapropiedad **xmltext** y se convierte en una columna de desbordamiento. Como consecuencia, la columna recibe los datos no utilizados. En este caso es todo el documento.  
  
 A continuación, la instrucción SELECT devuelve el conjunto de filas completo.  
  
```  
DECLARE @idoc int  
DECLARE @doc nvarchar(1000)  
SET @doc = N'<?xml version="1.0"?>  
<root>  
  <Customer cid= "C1" name="Janine" city="Issaquah">  
      <Order oid="O1" date="1/20/1996" amount="3.5" />  
      <Order oid="O2" date="4/30/1997" amount="13.4">Customer was very   
             satisfied</Order>  
   </Customer>  
   <Customer cid="C2" name="Ursula" city="Oelde" >  
      <Order oid="O3" date="7/14/1999" amount="100" note="Wrap it blue   
             white red">  
     <MyTag>Testing to see if all the subelements are returned</MyTag>  
          <Urgency>Important</Urgency>  
      </Order>  
      <Order oid="O4" date="1/20/1996" amount="10000"/>  
   </Customer>  
</root>'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @idoc OUTPUT, @doc  
  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@idoc, '/')  
   WITH (Col1 ntext '@mp:xmltext')  
```  
  
 Para recuperar todo el documento sin la declaración XML, se puede especificar la consulta como se muestra a continuación:  
  
```  
SELECT *  
FROM OPENXML (@idoc, '/root')  
   WITH (Col1 ntext '@mp:xmltext')  
EXEC sp_xml_removedocument @idoc  
```  
  
 La consulta devuelve el elemento raíz que tiene la raíz del nombre y los datos contenidos en el elemento raíz.  
  
### <a name="c-specifying-the-xmltext-metaproperty-to-retrieve-the-unconsumed-data-in-a-column"></a>C. Especificar la metapropiedad xmltext para recuperar los datos no usados en una columna  
 Este ejemplo utiliza OPENXML para crear una vista de conjunto de filas del documento XML de ejemplo. Muestra cómo recuperar los datos XML no utilizados mediante la asignación del atributo de metapropiedad **xmltext** a una columna de conjunto de filas en OPENXML.  
  
 El parámetro **comment** se identifica como la columna de desbordamiento al asignarla a la metapropiedad **@mp:xmltext** . El parámetro *flags* se establece en **9** (XML_ATTRIBUTE y XML_NOCOPY). Esto indica que es una asignación **centrada en atributos** y que solo deberían copiarse los datos no usados en la columna de desbordamiento.  
  
 A continuación, la instrucción SELECT devuelve el conjunto de filas proporcionado por OPENXML.  
  
 En este ejemplo, se establece la metapropiedad **@mp:parentlocalname** para una columna ( **ParentLocalName**) del conjunto de filas generado por OPENXML. Como resultado, esta columna contiene el nombre local del elemento primario.  
  
 Se especifican dos columnas adicionales en el conjunto de filas, **parent** y **comment**. El parámetro **parent** se asigna a **@mp:parentid** e indica que la columna contiene el Id. XML del elemento primario del elemento. La columna comment se identifica como la columna de desbordamiento mediante su asignación a la metapropiedad **@mp:xmltext** .  
  
```  
DECLARE @idoc int  
DECLARE @doc nvarchar(1000)  
-- sample XML document  
SET @doc = N'<root>  
  <Customer cid= "C1" name="Janine" city="Issaquah">  
      <Order oid="O1" date="1/20/1996" amount="3.5" />  
      <Order oid="O2" date="4/30/1997" amount="13.4">Customer was very satisfied</Order>  
   </Customer>  
   <Customer cid="C2" name="Ursula" city="Oelde" >  
      <Order oid="O3" date="7/14/1999" amount="100" note="Wrap it blue white red">  
          <Urgency>Important</Urgency>  
      </Order>  
      <Order oid="O4" date="1/20/1996" amount="10000"/>  
   </Customer>  
</root>  
'  
-- Create an internal representation of the XML document.  
EXEC sp_xml_preparedocument @idoc OUTPUT, @doc  
  
-- Execute a SELECT statement using OPENXML rowset provider.  
SELECT *  
FROM OPENXML (@idoc, '/root/Customer/Order', 9)  
      WITH (oid char(5),   
            date datetime,  
            comment ntext '@mp:xmltext')  
EXEC sp_xml_removedocument @idoc  
```  
  
 Éste es el resultado. Como las columnas oid y date ya se han utilizado, no aparecen en la columna de desbordamiento.  
  
```  
oid   date                        comment                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            
----- --------------------------- ----------------------------------------  
O1    1996-01-20 00:00:00.000     <Order amount="3.5"/>  
O2    1997-04-30 00:00:00.000     <Order amount="13.4">Customer was very   
                                   satisfied</Order>  
O3    1999-07-14 00:00:00.000     <Order amount="100" note="Wrap it blue   
                                   white red"><Urgency>   
                                   Important</Urgency></Order>  
O4    1996-01-20 00:00:00.000     <Order amount="10000"/>  
```  
  
## <a name="see-also"></a>Vea también  
 [OPENXML &#40;Transact-SQL&#41;](/sql/t-sql/functions/openxml-transact-sql)   
 [OPENXML &#40;SQL Server&#41;](../xml/openxml-sql-server.md)  
  
  
