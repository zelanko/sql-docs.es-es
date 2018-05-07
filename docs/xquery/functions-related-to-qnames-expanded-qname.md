---
title: Expanded-QName (XQuery) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.component: xquery
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- expanded-QName function
- fn:expanded-QName function
ms.assetid: b8377042-95cc-467b-9ada-fe43cebf4bc3
caps.latest.revision: 19
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: b76f85fae2f01322838c40b79227da896fabd01c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="functions-related-to-qnames---expanded-qname"></a>Las funciones relacionadas con QNames - QName expandido
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Devuelve un valor de tipo xs: QName con el espacio de nombres URI especificado en el *$paramURI* y el nombre local especificado en el *$paramLocal*. Si *$paramURI* es una cadena vacía o una secuencia vacía, no representa ningún espacio de nombres.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
fn:expanded-QName($paramURI as xs:string?, $paramLocal as xs:string?) as xs:QName?  
```  
  
## <a name="arguments"></a>Argumentos  
 *$paramURI*  
 Es el URI del espacio de nombres de QName.  
  
 *$paramLocal*  
 Es la parte local del nombre de QName.  
  
## <a name="remarks"></a>Comentarios  
 Las siguientes condiciones a la **expanded-QName()** función:  
  
-   Si el *$paramLocal* valor especificado no está en la forma léxica correcta para el tipo xs: NCName, una secuencia vacía, se devuelve y representa un error dinámico.  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no admite la conversión del tipo xs:QName a ningún otro tipo. Por este motivo, el **expanded-QName()** no se puede usar la función en la construcción de XML. Por ejemplo, cuando se construye un nodo, como `<e> expanded-QName(…) </e>`, el valor no puede tener un tipo. Esto requeriría la conversión del valor de tipo xs:QName devuelto por `expanded-QName()` en xdt:untypedAtomic. Sin embargo, esta opción no se admite. Más adelante en este tema se ofrece un ejemplo.  
  
-   Es posible modificar o comparar los valores de tipo QName existentes. Por ejemplo, `/root[1]/e[1] eq expanded-QName("http://nsURI" "myNS")` compara el valor del elemento, <`e`>, con el QName devuelto por la **expanded-QName()** (función).  
  
## <a name="examples"></a>Ejemplos  
 Este tema ofrecen ejemplos de XQuery con instancias XML almacenadas en varias **xml** escriba columnas en la [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] base de datos.  
  
### <a name="a-replacing-a-qname-type-node-value"></a>A. Reemplazar un valor de nodo del tipo QName  
 En este ejemplo se ilustra cómo se puede modificar el valor de un nodo de elemento del tipo QName. En el ejemplo, se realizan las tareas siguientes:  
  
-   Se crea una colección de esquemas XML que define un elemento del tipo QName.  
  
-   Crea una tabla con un **xml** columna de tipo mediante el uso de la colección de esquemas XML.  
  
-   Se guarda una instancia XML en la tabla.  
  
-   Usa el **modify()** método del tipo de datos xml para modificar el valor del elemento de tipo QName en la instancia. El **expanded-QName()** función se utiliza para generar el nuevo valor de tipo QName.  
  
```  
-- If XML schema collection (if exists)  
-- drop xml schema collection SC  
-- go  
-- Create XML schema collection  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema"  
    xmlns:xs="http://www.w3.org/2001/XMLSchema"   
    targetNamespace="QNameXSD"   
      xmlns:xqo="QNameXSD" elementFormDefault="qualified">  
      <element name="Root" type="xqo:rootType" />  
      <complexType name="rootType">  
            <sequence minOccurs="1" maxOccurs="1">  
                        <element name="ElemQN" type="xs:QName" />  
            </sequence>  
      </complexType>  
</schema>'  
go  
-- Create table.  
CREATE TABLE T( XmlCol xml(SC) )  
-- Insert sample XML instnace  
INSERT INTO T VALUES ('  
<Root xmlns="QNameXSD" xmlns:ns="http://myURI">  
      <ElemQN>ns:someName</ElemQN>  
</Root>')  
go  
-- Verify the insertion  
SELECT * from T  
go  
-- Result  
<Root xmlns="QNameXSD" xmlns:ns="http://myURI">  
  <ElemQN>ns:someName</ElemQN>  
</Root>   
```  
  
 En la siguiente consulta, el <`ElemQN`> se sustituye el valor del elemento mediante el uso de la **modify()** método del tipo de datos xml y el valor de reemplazo de XML DML, como se muestra.  
  
```  
-- the value.  
UPDATE T   
SET XmlCol.modify('  
  declare default element namespace "QNameXSD";   
  replace value of /Root[1]/ElemQN   
  with expanded-QName("http://myURI", "myLocalName") ')  
go  
-- Verify the result  
SELECT * from T  
go  
```  
  
 Éste es el resultado. Tenga en cuenta que ahora el elemento <`ElemQN`> del tipo QName tiene un nuevo valor:  
  
```  
<Root xmlns="QNameXSD" xmlns:ns="urn">  
  <ElemQN xmlns:p1="http://myURI">p1:myLocalName</ElemQN>  
</Root>  
```  
  
 Las instrucciones siguientes eliminan los objetos utilizados en el ejemplo.  
  
```  
-- Cleanup  
DROP TABLE T  
go  
drop xml schema collection SC  
go  
```  
  
### <a name="b-dealing-with-the-limitations-when-using-the-expanded-qname-function"></a>B. Superar las limitaciones cuando se utiliza la función expanded-QName()  
 El **QName expandido** no se puede usar la función en la construcción de XML. Esto se ilustra en el siguiente ejemplo. Para evitar esta limitación, el ejemplo inserta primero un nodo y, a continuación, modifica el nodo.  
  
```  
-- if exists drop the table T  
--drop table T  
-- go  
-- Create XML schema collection  
-- DROP XML SCHEMA COLLECTION SC  
-- go  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
      <element name="root" type="QName" nillable="true"/>  
</schema>'  
go  
 -- Create table T with a typed xml column (using the XML schema collection)  
CREATE TABLE T (xmlCol XML(SC))  
go  
-- Insert an XML instance.  
insert into T values ('<root xmlns:a="http://someURI">a:b</root>')  
 go  
-- Verify  
SELECT *   
FROM T  
```  
  
 El intento siguiente agrega otro elemento <`root`> pero se produce un error, puesto que no se admite la función expanded-QName() en la construcción de XML.  
  
```  
update T SET xmlCol.modify('  
insert <root>{expanded-QName("http://ns","someLocalName")}</root> as last into / ')  
go  
```  
  
 Una solución consiste en insertar primero una instancia con un valor para el elemento <`root`> y, a continuación, modificarlo. En este ejemplo, se utiliza un valor inicial nil cuando se inserta el elemento <`root`>. La colección de esquemas XML de este ejemplo permite un valor nil para el elemento <`root`>.  
  
```  
update T SET xmlCol.modify('  
insert <root xsi:nil="true"/> as last into / ')  
go  
-- now replace the nil value with another QName.  
update T SET xmlCol.modify('  
replace value of /root[last()] with expanded-QName("http://ns","someLocalName") ')  
go  
 -- verify   
SELECT * FROM T  
go  
-- result  
<root>b</root>  
```  
  
 `<root xmlns:a="http://someURI">a:b</root>`  
  
 `<root xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:p1="http://ns">p1:someLocalName</root>`  
  
 Se puede comparar el valor QName, tal y como se muestra en la consulta siguiente. La consulta devuelve solo el <`root`> elementos cuyos valores coinciden con el QName del tipo de valor devuelto por la **expanded-QName()** (función).  
  
```  
SELECT xmlCol.query('  
    for $i in /root  
    return  
       if ($i eq expanded-QName("http://ns","someLocalName") ) then  
          $i  
       else  
          ()')  
FROM T  
```  
  
### <a name="implementation-limitations"></a>Limitaciones de la implementación  
 Hay una limitación: el **expanded-QName()** acepta la secuencia vacía como segundo argumento de función y se devolverá vacía en lugar de generar un error en tiempo de ejecución cuando el segundo argumento sea incorrecto.  
  
## <a name="see-also"></a>Vea también  
 [Las funciones relacionadas con QNames &#40;XQuery&#41;](http://msdn.microsoft.com/library/7e07eb26-f551-4b63-ab77-861684faff71)  
  
  
