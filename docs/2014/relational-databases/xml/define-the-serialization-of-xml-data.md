---
title: Definición de la serialización de datos XML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- entitization rules [XML in SQL Server]
- serialization
- reparsing serialized XML structures
- encoding [XML in SQL Server]
- XML [SQL Server], serialization
- xml data type [SQL Server], serialization
- typed XML
ms.assetid: 42b0b5a4-bdd6-4a60-b451-c87f14758d4b
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: aa8862574285fe8e8a95119501d64565b35a6aa0
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37183962"
---
# <a name="define-the-serialization-of-xml-data"></a>Definir la serialización de datos XML
  Cuando el tipo de datos xml se convierte de manera explícita o implícita a un tipo SQL binario o de cadena, el contenido del tipo de datos xml se serializa de acuerdo con las reglas que se describen en este tema.  
  
## <a name="serialization-encoding"></a>Codificación de la serialización  
 Si el tipo SQL de destino es VARBINARY, el resultado se serializa en UTF-16 con una marca de orden de bytes UTF-16 delante, pero sin una declaración XML. Si el tipo de destino es demasiado pequeño, se genera un error.  
  
 Por ejemplo:  
  
```  
select CAST(CAST(N'<Δ/>' as XML) as VARBINARY(MAX))  
```  
  
 El resultado es el siguiente:  
  
```  
0xFFFE3C0094032F003E00  
```  
  
 Si el tipo SQL de destino es NVARCHAR o NCHAR, el resultado se serializa en UTF-16 sin una marca de orden de bytes y sin una declaración XML. Si el tipo de destino es demasiado pequeño, se genera un error.  
  
 Por ejemplo:  
  
```  
select CAST(CAST(N'<Δ/>' as XML) as NVARCHAR(MAX))  
```  
  
 El resultado es el siguiente:  
  
```  
<Δ/>  
```  
  
 Si el tipo SQL de destino es VARCHAR o NCHAR, el resultado se serializa en la codificación que corresponda a la página de códigos de intercalación de la base de datos, sin marca de orden de bytes ni declaración XML. Si el tipo de destino es demasiado pequeño o el valor no se puede asignar a la página de códigos de intercalación de destino, se genera un error.  
  
 Por ejemplo:  
  
```  
select CAST(CAST(N'<Δ/>' as XML) as VARCHAR(MAX))  
```  
  
 Se puede generar un error si la página de códigos de la intercalación actual no puede representar el carácter Unicode Δ, o se representará en la codificación específica.  
  
 Cuando se devuelven los resultados XML al cliente, los datos se envían codificados como UTF-16. Después, el proveedor del lado cliente expondrá los datos de acuerdo con sus reglas de API.  
  
## <a name="serialization-of-the-xml-structures"></a>Serialización de las estructuras XML  
 El contenido de un tipo de datos **xml** se serializa de la forma habitual. Concretamente, los nodos de elementos se asignan a marcado de elemento y los nodos de texto se asignan a contenido de texto. No obstante, en las siguientes secciones se describen las circunstancias en las que se crean entidades para los caracteres y cómo se serializan los valores atómicos con tipo.  
  
## <a name="entitization-of-xml-characters-during-serialization"></a>Creación de entidades para caracteres XML durante la serialización  
 Todas las estructuras XML serializadas deberían poder analizarse de nuevo. Por tanto, algunos caracteres deben serializarse como entidades para que conserven su funcionalidad de ida y vuelta durante la fase de normalización del analizador XML. Sin embargo, deben crearse entidades para algunos caracteres con el fin de que el formato del documento sea correcto, y, por tanto, se pueda analizar. A continuación se exponen las reglas de creación de entidades que se aplican durante la serialización:  
  
-   Para los caracteres &, \< y > siempre se crean las entidades &amp;, &lt; y &gt;, respectivamente, si aparecen en valores de atributos o en el contenido de elementos.  
  
-   Dado que SQL Server usa comillas (U+0022) para incluir los valores de los atributos, para las comillas de los valores de atributo se crea la entidad &quot;.  
  
-   La entidad que se crea para un par suplente es una única referencia de carácter numérico, solo cuando la conversión se realiza en el servidor. Por ejemplo, el par suplente U+D800 U+DF00 pasa a ser la entidad de referencia de carácter numérico &\#x00010300;.  
  
-   Para evitar que un carácter de tabulación (U+0009) o avance de línea (LF, U+000A) se normalice durante el análisis, tendrán como entidades sus referencias de carácter numérico (&\#x9; y &\#xA;, respectivamente) en los valores de atributos.  
  
-   Para evitar que un carácter de retorno de carro (CR, U+000D) se normalice durante el análisis, tendrá como entidad su referencia de carácter numérico (&\#xD;) en los valores de atributos y en el contenido de elementos.  
  
-   Para proteger los nodos de texto que solo contienen espacios en blanco, se crea una entidad para uno de los caracteres de espacio en blanco, generalmente el último, que se corresponde con su referencia de carácter numérico. De esta manera, cuando se vuelve a realizar el análisis, se conserva el nodo de texto de espacio en blanco independientemente de la configuración del control de espacios en blanco durante el análisis.  
  
 Por ejemplo:  
  
```  
declare @u NVARCHAR(50)  
set @u = N'<a a="  
    '+NCHAR(0xD800)+NCHAR(0xDF00)+N'>">   '+NCHAR(0xA)+N'</a>'  
select CAST(CONVERT(XML,@u,1) as NVARCHAR(50))  
```  
  
 El resultado es el siguiente:  
  
```  
<a a="  
    𐌀>">     
</a>  
```  
  
 Si no quiere aplicar la regla de protección del último espacio en blanco, puede usar la opción explícita de CONVERT 1 al convertir el tipo **xml** en un tipo de cadena o binario. Por ejemplo, para evitar la creación de entidades, tiene las opciones siguientes:  
  
```  
select CONVERT(NVARCHAR(50), CONVERT(XML, '<a>   </a>', 1), 1)  
```  
  
 Tenga en cuenta que [query() (método de tipo de datos xml)](/sql/t-sql/xml/query-method-xml-data-type) genera una instancia de tipo de datos xml. Por tanto, se crearán entidades para cualquier resultado del método **query()** que se convierta en un tipo binario o de cadena de acuerdo con las reglas previamente descritas. Si se quieren obtener los valores de cadena sin creación de entidades, en su lugar debe usarse [value() (método del tipo de datos xml)](/sql/t-sql/xml/value-method-xml-data-type) . A continuación se ofrece un ejemplo de uso del método **query()** :  
  
```  
declare @x xml  
set @x = N'<a>This example contains an entitized char: <.</a>'  
select @x.query('/a/text()')  
```  
  
 El resultado es el siguiente:  
  
```  
This example contains an entitized char: <.  
```  
  
 A continuación se ofrece un ejemplo de uso del método **value()** :  
  
```  
select @x.value('(/a/text())[1]', 'nvarchar(100)')  
```  
  
 El resultado es el siguiente:  
  
```  
This example contains an entitized char: <.  
```  
  
## <a name="serializing-a-typed-xml-data-type"></a>Serializar un tipo de datos xml con tipo  
 Una instancia de tipo de datos **xml** con tipo contiene valores cuyos tipos se corresponden con los tipos de su esquema XML. Estos valores se serializan según su tipo de esquema XML, en el mismo formato que genera la conversión XQuery a xs:string. Para obtener más información, vea [Reglas de conversión de tipos en XQuery](/sql/xquery/type-casting-rules-in-xquery).  
  
 Por ejemplo, el valor 1.34e1 de tipo xs:double se serializa como 13.4, como se observa en el ejemplo siguiente:  
  
```  
declare @x xml  
set @x =''  
select CAST(@x.query('1.34e1') as nvarchar(50))  
```  
  
 Se obtiene el valor de cadena 13.4.  
  
## <a name="see-also"></a>Vea también  
 [Reglas de conversión de tipos en XQuery](/sql/xquery/type-casting-rules-in-xquery)   
 [CAST y CONVERT &#40;Transact-SQL&#41;](/sql/t-sql/functions/cast-and-convert-transact-sql)  
  
  
