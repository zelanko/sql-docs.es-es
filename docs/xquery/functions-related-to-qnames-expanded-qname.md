---
title: Expanded-QName (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- expanded-QName function
- fn:expanded-QName function
ms.assetid: b8377042-95cc-467b-9ada-fe43cebf4bc3
author: rothja
ms.author: jroth
ms.openlocfilehash: 7c50409ea35809c52de718a8281bf76f75a5a0e0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68004583"
---
# <a name="functions-related-to-qnames---expanded-qname"></a>Funciones relacionadas con QNames: expanded-QName
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Devuelve un valor del tipo xs: QName con el espacio de nombres URI especificado en el *$paramURI* y el nombre local especificado en el *$paramLocal*. Si *$paramURI* es una cadena vacía o una secuencia vacía, no representa ningún espacio de nombres.  
  
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
  
-   Si el *$paramLocal* valor especificado no está en la forma léxica correcta para el tipo xs: NCName, se devuelve una secuencia vacía y representa un error dinámico.  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no admite la conversión del tipo xs:QName a ningún otro tipo. Por este motivo, el **expanded-QName()** función no se puede usar en la construcción de XML. Por ejemplo, cuando se construye un nodo, como `<e> expanded-QName(...) </e>`, el valor no puede tener un tipo. Esto requeriría la conversión del valor de tipo xs:QName devuelto por `expanded-QName()` en xdt:untypedAtomic. Sin embargo, esta opción no se admite. Más adelante en este tema se ofrece un ejemplo.  
  
-   Es posible modificar o comparar los valores de tipo QName existentes. Por ejemplo, `/root[1]/e[1] eq expanded-QName("http://nsURI" "myNS")` compara el valor del elemento, <`e`>, con el QName devuelto por la **expanded-QName()** función.  
  
## <a name="examples"></a>Ejemplos  
 En este tema se proporciona ejemplos de XQuery con instancias XML almacenadas en varias **xml** escriba columnas en el [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] base de datos.  
  
### <a name="a-replacing-a-qname-type-node-value"></a>A. Reemplazar un valor de nodo del tipo QName  
 En este ejemplo se ilustra cómo se puede modificar el valor de un nodo de elemento del tipo QName. En el ejemplo, se realizan las tareas siguientes:  
  
-   Se crea una colección de esquemas XML que define un elemento del tipo QName.  
  
-   Crea una tabla con un **xml** columna de tipo mediante el uso de la colección de esquemas XML.  
  
-   Se guarda una instancia XML en la tabla.  
  
-   Usa el **modify()** método del tipo de datos xml para modificar el valor del elemento en la instancia de tipo QName. El **expanded-QName()** función se utiliza para generar el nuevo valor de tipo QName.  
  
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
<Root xmlns="QNameXSD" xmlns:ns="https://myURI">  
      <ElemQN>ns:someName</ElemQN>  
</Root>')  
go  
-- Verify the insertion  
SELECT * from T  
go  
-- Result  
<Root xmlns="QNameXSD" xmlns:ns="https://myURI">  
  <ElemQN>ns:someName</ElemQN>  
</Root>   
```  
  
 En la siguiente consulta, el <`ElemQN`> se reemplaza el valor del elemento utilizando el **modify()** método del tipo de datos xml y el valor de reemplazo de XML DML, como se muestra.  
  
```  
-- the value.  
UPDATE T   
SET XmlCol.modify('  
  declare default element namespace "QNameXSD";   
  replace value of /Root[1]/ElemQN   
  with expanded-QName("https://myURI", "myLocalName") ')  
go  
-- Verify the result  
SELECT * from T  
go  
```  
  
 Éste es el resultado. Tenga en cuenta que el elemento <`ElemQN`> de QName tiene ahora un nuevo valor de tipo:  
  
```  
<Root xmlns="QNameXSD" xmlns:ns="urn">  
  <ElemQN xmlns:p1="https://myURI">p1:myLocalName</ElemQN>  
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
  
### <a name="b-dealing-with-the-limitations-when-using-the-expanded-qname-function"></a>b. Superar las limitaciones cuando se utiliza la función expanded-QName()  
 El **expanded-QName** función no se puede usar en la construcción de XML. Esto se ilustra en el siguiente ejemplo: Para evitar esta limitación, el ejemplo inserta primero un nodo y, a continuación, modifica el nodo.  
  
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
insert into T values ('<root xmlns:a="https://someURI">a:b</root>')  
 go  
-- Verify  
SELECT *   
FROM T  
```  
  
 El intento siguiente agrega otro <`root`> elemento, pero se produce un error, porque no se admite la función expanded-QName() en construcción de XML.  
  
```  
update T SET xmlCol.modify('  
insert <root>{expanded-QName("http://ns","someLocalName")}</root> as last into / ')  
go  
```  
  
 Una solución para este problema consiste en Insertar primero una instancia con un valor para el <`root`> elemento y, a continuación, modificarlo. En este ejemplo, se usa un valor inicial nil cuando el <`root`> se inserta el elemento. La colección de esquemas XML en este ejemplo permite un valor nulo para el <`root`> elemento.  
  
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
  
 `<root xmlns:a="https://someURI">a:b</root>`  
  
 `<root xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:p1="http://ns">p1:someLocalName</root>`  
  
 Se puede comparar el valor QName, tal y como se muestra en la consulta siguiente. La consulta devuelve sólo el <`root`> los elementos cuyos valores coinciden con el QName tipo de valor devuelto por la **expanded-QName()** función.  
  
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
 Hay una limitación: El **expanded-QName()** función acepta una secuencia vacía como segundo argumento y se devolverá vacía en lugar de generar un error en tiempo de ejecución cuando el segundo argumento sea incorrecto.  
  
## <a name="see-also"></a>Vea también  
 [Funciones relacionadas con QNames &#40;XQuery&#41;](https://msdn.microsoft.com/library/7e07eb26-f551-4b63-ab77-861684faff71)  
  
  
