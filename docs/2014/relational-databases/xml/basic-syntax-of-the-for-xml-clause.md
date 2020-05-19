---
title: Sintaxis básica de la cláusula FOR XML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- BINARY BASE64 directive
- ROOT directive
- FOR XML clause, BINARY BASE64 directive
- FOR XML clause, syntax
- FOR XML clause, ROOT directive
ms.assetid: df19ecbf-d28e-4e9c-aaa3-700f8bbd3be4
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: e09323a96a5a2fc282c1595c2606ea7e9b9a6bee
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82717352"
---
# <a name="basic-syntax-of-the-for-xml-clause"></a>Sintaxis básica de la cláusula FOR XML
  El modo de FOR XML puede ser RAW, AUTO, EXPLICIT o PATH. Determina la forma del XML resultante.  
  
> [!IMPORTANT]  
>  La directiva XMLDATA para la opción FOR XML ha quedado desusada. Utilice la XSD generación en los modos RAW y AUTO. No hay sustitución para la directiva XMLDATA en modo EXPLICIT. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 A continuación se indica la sintaxis básica que se describe en la [cláusula for (Transact-SQL)](/sql/t-sql/queries/select-for-clause-transact-sql):  
  
```  
[ FOR { BROWSE | <XML> } ]  
<XML> ::=  
XML   
    {   
      { RAW [ ('ElementName') ] | AUTO }   
        [   
           <CommonDirectives>   
           [ , { XMLDATA | XMLSCHEMA [ ('TargetNameSpaceURI') ]} ]   
           [ , ELEMENTS [ XSINIL | ABSENT ]   
        ]  
      | EXPLICIT   
        [   
           <CommonDirectives>   
           [ , XMLDATA ]   
        ]  
      | PATH [ ('ElementName') ]   
        [   
           <CommonDirectives>   
           [ , ELEMENTS [ XSINIL | ABSENT ] ]  
        ]  
     }   
  
 <CommonDirectives> ::=   
   [ , BINARY BASE64 ]  
   [ , TYPE ]  
   [ , ROOT [ ('RootName') ] ]  
```  
  
## <a name="arguments"></a>Argumentos  
 RAW[('*ElementName*')]  
 Obtiene el resultado de la consulta y transforma cada fila del conjunto de resultados en un elemento XML con un identificador genérico \<row /> como etiqueta del elemento. Opcionalmente, puede especificar un nombre para el elemento de fila cuando se utiliza esta directiva. El XML resultante utilizará el *ElementName* especificado como el elemento de fila generado para cada fila. Para obtener más información, vea [Usar el modo RAW con FOR XML](use-raw-mode-with-for-xml.md).  
  
 AUTO  
 Devuelve los resultados de la consulta en un árbol anidado XML sencillo. Cada tabla en la cláusula FROM de la que al menos se presenta una columna en la cláusula SELECT se representa como un elemento XML. A las columnas presentadas en la cláusula SELECT se les asignan los atributos de elemento apropiados. Para obtener más información, vea [Usar el modo AUTO con FOR XML](use-auto-mode-with-for-xml.md).  
  
 EXPLICIT  
 Especifica que la forma del árbol XML resultante está definida explícitamente. Con este modo, es necesario escribir las consultas de una cierta manera, de modo que se pueda especificar explícitamente información adicional acerca de la anidación deseada. Para obtener más información, vea [Usar el modo EXPLICIT con FOR XML](use-explicit-mode-with-for-xml.md).  
  
 PATH  
 Facilita la mezcla de elementos y atributos, así como la especificación de anidación adicional para representar propiedades complejas. Puede utilizar consultas FOR XML de modo EXPLICIT para construir XML a partir de un conjunto de filas, pero el modo PATH supone una alternativa más simple a las consultas de modo EXPLICIT potencialmente complicadas. El modo PATH, junto con la posibilidad de escribir consultas FOR XML anidadas y la directiva TYPE para devolver instancias de tipo **xml** , permite escribir consultas de forma más fácil. Ofrece una alternativa para escribir la mayoría de las consultas de modo EXPLICIT. El modo PATH genera un contenedor de elementos \<row> de forma predeterminada por cada fila del conjunto de resultados. También se puede especificar un nombre de elemento. En este caso, el nombre especificado se utilizará como nombre del elemento contenedor. Si se proporciona una cadena vacía (FOR XML PATH ('')), no se generará ningún elemento contenedor. Para obtener más información, vea [Usar el modo PATH con FOR XML](use-path-mode-with-for-xml.md).  
  
 XMLDATA  
 Especifica que se debe devolver un esquema XDR (XML-Data Reduced) insertado. El esquema se antepone al documento como un esquema insertado. Para obtener un ejemplo práctico, vea [Usar el modo RAW con FOR XML](use-raw-mode-with-for-xml.md).  
  
 XMLSCHEMA  
 Devuelve un esquema XML W3C (XSD) insertado. Opcionalmente, puede especificar un URI de espacio de nombres de destino al especificar esta directiva. De este modo, se devuelve el espacio de nombres especificado en el esquema. Para obtener más información, vea [Generar un esquema XSD insertado](generate-an-inline-xsd-schema.md). Para obtener un ejemplo práctico, vea [Usar el modo RAW con FOR XML](use-raw-mode-with-for-xml.md).  
  
 ELEMENTS  
 Si se especifica la opción ELEMENTS, las columnas se devuelven como subelementos. Sin embargo, se les asignan atributos XML. Esta opción solo se admite en los modos RAW, AUTO y PATH. También puede especificar XSINIL o ABSENT cuando utilice esta directiva. XSINIL especifica que se puede crear un elemento con un atributo **xsi:nil** establecido en True para los valores de columna NULL. De forma predeterminada, o cuando se especifica ABSENT junto con ELEMENTS, no se crea ningún elemento para los valores NULL. Para obtener un ejemplo práctico, vea [Usar el modo RAW con FOR XML](use-raw-mode-with-for-xml.md) y [Usar el modo AUTO con FOR XML](use-auto-mode-with-for-xml.md).  
  
 BINARY BASE64  
 Si se especifica la opción BINARY Base64, todos los datos binarios que devuelve la consulta se representan en formato codificado base64. Para recuperar datos binarios mediante el modo RAW y EXPLICIT, se debe especificar esta opción. En modo AUTO, de forma predeterminada, se devuelven datos binarios como una referencia. Para obtener un ejemplo práctico, vea [Usar el modo RAW con FOR XML](use-raw-mode-with-for-xml.md).  
  
 TYPE  
 Especifica que la consulta devuelve los resultados como el tipo **xml** . Para más información, consulte [TYPE Directive in FOR XML Queries](type-directive-in-for-xml-queries.md).  
  
 ROOT [('*RootName*')]  
 Especifica que se puede agregar un solo elemento de nivel superior al XML resultante. También se puede especificar el nombre del elemento raíz que se generará. El valor predeterminado es "root".  
  
## <a name="see-also"></a>Consulte también  
 [Usar el modo RAW con FOR XML](use-raw-mode-with-for-xml.md)   
 [Usar el modo AUTO con FOR XML](use-auto-mode-with-for-xml.md)   
 [Usar el modo EXPLICIT con FOR XML](use-explicit-mode-with-for-xml.md)   
 [Usar el modo PATH con FOR XML](use-path-mode-with-for-xml.md)   
 [SELECT &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql)   
 [FOR XML &#40;SQL Server&#41;](for-xml-sql-server.md)  
  
  
