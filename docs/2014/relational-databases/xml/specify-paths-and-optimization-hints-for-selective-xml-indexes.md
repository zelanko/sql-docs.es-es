---
title: Especificar rutas de acceso y sugerencias de optimización para índices XML selectivos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 486ee339-165b-4aeb-b760-d2ba023d7d0a
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0305c5229d5e690b163cfec12e87aa1d412af4f6
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2018
ms.locfileid: "43889851"
---
# <a name="specify-paths-and-optimization-hints-for-selective-xml-indexes"></a>Especificar rutas de acceso y sugerencias de optimización para índices XML selectivos
  En este tema se describe cómo especificar rutas de acceso del nodo al índice y sugerencias de optimización para indizar cuando se crean o modifican índices XML selectivos.  
  
 Especifique las rutas de acceso del nodo y las sugerencias de optimización al mismo tiempo en una de las instrucciones siguientes:  
  
-   En la cláusula **FOR** de una instrucción **CREATE** . Para obtener más información, vea [CREAR ÍNDICE XML SELECTIVO &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-selective-xml-index-transact-sql).  
  
-   En la cláusula **ADD** de una instrucción **ALTER** . Para obtener más información, vea [ALTER INDEX &#40;Selective XML Indexes&#41;](../indexes/indexes.md).  
  
 Para obtener más información sobre los índices XML selectivos, vea [Índices XML selectivos &#40;SXI&#41;](../xml/selective-xml-indexes-sxi.md).  
  
##  <a name="untyped"></a> Descripción de los tipos de XQuery y SQL Server en XML sin tipo  
 Los índices XML selectivos admiten dos sistemas de tipos: tipos XQuery y tipos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . La ruta de acceso indizada se puede usar para buscar coincidencias con una expresión XQuery o para buscar coincidencias con el tipo de valor devuelto del método value() del tipo de datos XML.  
  
-   Si una ruta de acceso al índice no está anotada, o si está anotada con la palabra clave XQUERY, la ruta de acceso coincide con una expresión XQuery. Hay dos variaciones de rutas de acceso del nodo con XQUERY:  
  
    -   Si no especifica la palabra clave XQUERY y el tipo de datos XQuery, se usan las asignaciones predeterminadas. Normalmente el rendimiento y el almacenamiento no son óptimos.  
  
    -   Si se especifica la palabra clave XQUERY y el tipo de datos XQuery, y opcionalmente otras sugerencias de optimización, puede obtener el mejor rendimiento y el almacenamiento más eficiente posibles. Sin embargo, una conversión puede producir un error.  
  
-   Si una ruta de acceso al índice está anotada con la palabra clave SQL, la ruta de acceso coincide con el tipo de valor devuelto del método value() del tipo de datos XML. Especifique el tipo de datos adecuado de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , que es el tipo de valor devuelto que espera del método value().  
  
 Hay sutiles diferencias entre el sistema de tipos XML de las expresiones XQuery y el sistema de tipos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se aplica al método value() del tipo de datos XML. Entre estas diferencias cabe citar las siguientes:  
  
-   El sistema de tipos XQuery reconoce los espacios finales. Por ejemplo, según la semántica de tipos XQuery, las cadenas "abc" y "abc " no son iguales, mientras que en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estas cadenas son iguales.  
  
-   Los tipos de datos de punto flotante XQuery admiten valores especiales de +/- cero y +/- infinito. Estos valores especiales no se admiten en los tipos de datos de punto flotante de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="xquery-types-in-untyped-xml"></a>Tipos XQuery en XML sin tipo  
  
-   Los tipos XQuery coinciden con expresiones XQuery en todos los métodos del tipo de datos XML incluido el método value().  
  
-   Los tipos XQuery admiten estas sugerencias de optimización: node(), SINGLETON, DATA TYPE y MAXLENGTH.  
  
 Para las expresiones XQuery sobre XML sin tipo, puede elegir entre dos modos de funcionamiento:  
  
-   **Modo de asignación predeterminada**. En este modo, solo especifica la ruta de acceso al crear un índice XML selectivo.  
  
-   **Modo de asignación especificada por el usuario**. En este modo, especifica la ruta de acceso y las sugerencias opcionales de optimización.  
  
 El modo de asignación predeterminada emplea una opción de almacenamiento conservadora que siempre es segura y general. Puede coincidir con cualquier tipo de expresión. Una limitación del modo de asignación predeterminada es que el rendimiento no es óptimo, ya que se necesita un mayor número de conversiones en tiempo de ejecución y no hay índices secundarios disponibles.  
  
 A continuación se muestra un ejemplo de un índice XML selectivo creado con las asignaciones predeterminadas. Para las tres rutas de acceso, se usa el tipo de nodo predeterminado (**xs:untypedAtomic**) y cardinalidad.  
  
```tsql  
CREATE SELECTIVE XML INDEX example_sxi_UX_default  
ON Tbl(xmlcol)  
FOR  
(  
mypath01 =  '/a/b',  
mypath02 = '/a/b/c',  
mypath03 = '/a/b/d'  
)  
```  
  
 El modo de asignación especificada por el usuario permite especificar un tipo y la cardinalidad del nodo para obtener un rendimiento mejor. Sin embargo, este rendimiento mejorado se obtiene a costa de la seguridad (porque una conversión puede producir un error) y la generalidad (porque solo se compara el tipo especificado con el índice XML selectivo).  
  
 Los tipos XQuery admitidos para XML sin tipo son los siguientes:  
  
-   **xs:boolean**  
  
-   **xs:double**  
  
-   **xs:string**  
  
-   **xs:date**  
  
-   **xs:time**  
  
-   **xs:dateTime**  
  
 Si no se especifica el tipo, se supone que el nodo tiene el tipo de datos **xs:untypedAtomic** .  
  
 Puede optimizar el índice XML selectivo que se muestra de la manera siguiente:  
  
```tsql  
CREATE SELECTIVE XML INDEX example_sxi_UX_optimized  
ON Tbl(xmlcol)  
FOR  
(  
mypath= '/a/b' as XQUERY 'node()',  
pathX = '/a/b/c' as XQUERY 'xs:double' SINGLETON,  
pathY = '/a/b/d' as XQUERY 'xs:string' MAXLENGTH(200) SINGLETON  
)  
-- mypath – Only the node value is needed; storage is saved.  
-- pathX – Performance is improved; secondary indexes are possible.  
-- pathY - Performance is improved; secondary indexes are possible; storage is saved.  
```  
  
### <a name="sql-server-types-in-untyped-xml"></a>Tipos de SQL Server en XML sin tipo  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] los tipos coinciden con el valor devuelto del método value().  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admiten esta sugerencia de optimización: SINGLETON.  
  
 Es obligatorio especificar un tipo para las rutas de acceso que devuelven tipos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Use el mismo tipo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que usaría en el método value().  
  
 Estudie la siguiente consulta:  
  
```tsql  
SELECT T.record,  
    T.xmldata.value('(/a/b/d)[1]', 'NVARCHAR(200)')  
FROM myXMLTable T  
```  
  
 La consulta especificada devuelve un valor de la ruta de acceso `/a/b/d` empaquetado en un tipos de datos NVARCHAR(200), por lo que el tipo de datos para especificar el nodo es obvio. Sin embargo, no hay ningún esquema para especificar la cardinalidad del nodo en XML sin tipo. Para especificar que el nodo `d` aparece como máximo una vez en su nodo primario `b`, cree un índice XML selectivo que use la sugerencia de optimización SINGLETON de la manera siguiente:  
  
```tsql  
CREATE SELECTIVE XML INDEX example_sxi_US  
ON Tbl(xmlcol)  
FOR  
(  
node1223 = '/a/b/d' as SQL NVARCHAR(200) SINGLETON  
)  
```  
  

  
##  <a name="typed"></a> Descripción de la compatibilidad con índices XML selectivos para XML con tipo  
 XML con tipo en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es un esquema asociado a un documento XML determinado. El esquema define la estructura global del documento y los tipos de nodos. Si existe un esquema, el índice XML selectivo aplica la estructura del esquema cuando el usuario promueve rutas de acceso, por lo que no es necesario especificar los tipos XQUERY para las rutas de acceso.  
  
 El índice XML selectivo admite los tipos XSD siguientes:  
  
-   **xs:anyUri**  
  
-   **xs:boolean**  
  
-   **xs:date**  
  
-   **xs:dateTime**  
  
-   **xs:day**  
  
-   **xs:decimal**  
  
-   **xs:double**  
  
-   **xs:float**  
  
-   **xs:int**  
  
-   **xs:integer**  
  
-   **xs:language**  
  
-   **xs:long**  
  
-   **xs:name**  
  
-   **xs:NCName**  
  
-   **xs:negativeInteger**  
  
-   **xs:nmtoken**  
  
-   **xs:nonNegativeInteger**  
  
-   **xs:nonPositiveInteger**  
  
-   **xs:positiveInteger**  
  
-   **xs:qname**  
  
-   **xs:short**  
  
-   **xs:string**  
  
-   **xs:time**  
  
-   **xs:token**  
  
-   **xs:unsignedByte**  
  
-   **xs:unsignedInt**  
  
-   **xs:unsignedLong**  
  
-   **xs:unsignedShort**  
  
 Cuando el índice XML selectivo se crea en un documento que tiene un esquema asociado, si se especifica un tipo XQUERY al crear o modificar el índice se devuelve un error. El usuario puede emplear anotaciones de tipo SQL en la parte de promoción de la ruta de acceso. El tipo SQL debe ser una conversión válida del tipo XSD definido en el esquema o, de lo contrario, se producirá un error. Se admiten todos los tipos SQL que tienen una representación suficiente en XSD, salvo los tipos de fecha y hora.  
  
> [!NOTE]  
>  El índice selectivo se usa si el tipo especificado en la promoción de ruta de acceso del índice XML selectivo es igual que el valor devuelto del método value().  
  
 Se pueden usar las siguientes sugerencias de optimización con los documentos XML con tipo:  
  
-   Sugerencia de optimización node().  
  
-   La sugerencia de optimización MAXLENGTH se puede usar con tipos xs:string para acortar el valor indizado.  
  
 Para obtener más información acerca de las sugerencias de optimización, vea [Especificar sugerencias de optimización](#hints).  
  
##  <a name="paths"></a> Especificar rutas de acceso  
 Un índice XML selectivo permite indizar solo un subconjunto de nodos de los datos XML almacenados que son pertinentes para las consultas que espera ejecutar. Cuando el subconjunto de nodos pertinentes es mucho menor que el número total de nodos del documento XML, el índice XML selectivo solo almacena los nodos pertinentes. Para beneficiarse de un índice XML selectivo, identifique el subconjunto correcto de nodos para indizar.  
  
### <a name="choosing-the-nodes-to-index"></a>Elegir los nodos para indizar  
 Puede usar los dos principios simples siguientes para identificar el subconjunto correcto de nodos para agregar un índice XML selectivo.  
  
1.  **Principio 1**: para evaluar una expresión XQuery especificada, indice todos los nodos que necesite examinar.  
  
    -   Indice todos los nodos cuya existencia o valor se emplee en la expresión XQuery.  
  
    -   Indice todos los nodos de la expresión XQuery en la que se aplican los predicados XQuery.  
  
     Examine la consulta simple siguiente sobre el [documento XML de ejemplo](#sample) de este tema:  
  
    ```tsql  
    SELECT T.record FROM myXMLTable T  
    WHERE T.xmldata.exist('/a/b[./c = "43"]') = 1  
    ```  
  
     Para devolver las instancias XML que cumplen esta consulta, un índice XML selectivo necesita examinar dos nodos en cada instancia XML:  
  
    -   Nodo `c`, porque su valor se emplea en la expresión XQuery.  
  
    -   Nodo `b`, porque se aplica un predicado sobre el nodo`b` en la expresión XQuery.  
  
2.  **Principio 2**: para obtener el máximo rendimiento, índice todos los nodos que sean necesarios para evaluar una expresión XQuery dada. Si solo indiza algunos de los nodos, el índice XML selectivo mejora la evaluación de las subexpresiones que incluyen solo nodos indizados.  
  
 Para mejorar el rendimiento de la instrucción SELECT mostrada anteriormente, puede crear el índice XML selectivo siguiente:  
  
```tsql  
CREATE SELECTIVE XML INDEX simple_sxi  
ON Tbl(xmlcol)  
FOR  
(  
    path123 =  '/a/b',  
    path124 =  '/a/b/c'  
)  
```  
  
### <a name="indexing-identical-paths"></a>Indizar rutas de acceso idénticas  
 No puede promover rutas de acceso idénticas como el mismo tipo de datos con nombres de ruta de acceso diferentes. Por ejemplo, la consulta siguiente genera un error porque `pathOne` y `pathTwo` son idénticas:  
  
```tsql  
CREATE SELECTIVE INDEX test_simple_sxi ON T1(xmlCol)  
FOR  
(  
    pathOne = 'book/authors/authorID' AS XQUERY 'xs:string',  
    pathTwo = 'book/authors/authorID' AS XQUERY 'xs:string'  
)  
```  
  
 Sin embargo, puede promover rutas de acceso idénticas como tipos de datos diferentes con nombres distintos. Por ejemplo, la consulta siguiente ahora es aceptable porque los tipos de datos son diferentes:  
  
```tsql  
CREATE SELECTIVE INDEX test_simple_sxi ON T1(xmlCol)  
FOR  
(  
    pathOne = 'book/authors/authorID' AS XQUERY 'xs:double',  
    pathTwo = 'book/authors/authorID' AS XQUERY 'xs:string'  
)  
```  
  
### <a name="examples"></a>Ejemplos  
 A continuación se muestran algunos ejemplos adicionales de cómo seleccionar los nodos correctos para indizar para diferentes tipos XQuery.  
  
 **Ejemplo 1**  
  
 Esta es una expresión XQuery simple que usa el método exist():  
  
```tsql  
SELECT T.record FROM myXMLTable T  
WHERE T.xmldata.exist('/a/b/c/d/e/h') = 1  
```  
  
 En la tabla siguiente se muestran los nodos que se deben indizar para permitir que esta consulta use el índice XML selectivo.  
  
|Nodo para incluir en el índice|Motivo para indizar este nodo|  
|----------------------------------|-----------------------------------|  
|**/a/b/c/d/e/h**|La existencia del nodo `h` se evalúa en el método exist().|  
  
 **Ejemplo 2**  
  
 Esta es una variación más compleja de la expresión XQuery anterior a la que se ha aplicado un predicado:  
  
```tsql  
SELECT T.record FROM myXMLTable T  
WHERE T.xmldata.exist('/a/b/c/d/e[./f = "SQL"]') = 1  
```  
  
 En la tabla siguiente se muestran los nodos que se deben indizar para permitir que esta consulta use el índice XML selectivo.  
  
|Nodo para incluir en el índice|Motivo para indizar este nodo|  
|----------------------------------|-----------------------------------|  
|**/a/b/c/d/e**|Se aplica un predicado sobre el nodo `e`.|  
|**/a/b/c/d/e/f**|El valor del nodo `f` se evalúa dentro del predicado.|  
  
 **Ejemplo 3**  
  
 Esta es una consulta más compleja con una cláusula value():  
  
```tsql  
SELECT T.record,  
    T.xmldata.value('(/a/b/c/d/e[./f = "SQL"]/g)[1]', 'nvarchar(100)')  
FROM myXMLTable T  
```  
  
 En la tabla siguiente se muestran los nodos que se deben indizar para permitir que esta consulta use el índice XML selectivo.  
  
|Nodo para incluir en el índice|Motivo para indizar este nodo|  
|----------------------------------|-----------------------------------|  
|**/a/b/c/d/e**|Se aplica un predicado sobre el nodo `e`.|  
|**/a/b/c/d/e/f**|El valor del nodo `f` se evalúa dentro del predicado.|  
|**/a/b/c/d/e/g**|El método value() devuelve el valor del nodo `g` .|  
  
 **Ejemplo 4**  
  
 Esta es una consulta que usa una cláusula FLWOR dentro de una cláusula exist(). (El nombre FLWOR proviene de las cinco cláusulas que pueden crear una expresión FLWOR de XQuery: for, let, where, order by y return).  
  
```tsql  
SELECT T.record FROM myXMLTable T  
WHERE T.xmldata.exist('  
  For $x in /a/b/c/d/e  
  Where $x/f = "SQL"  
  Return $x/g  
') = 1  
```  
  
 En la tabla siguiente se muestran los nodos que se deben indizar para permitir que esta consulta use el índice XML selectivo.  
  
|Nodo para incluir en el índice|Motivo para indizar este nodo|  
|----------------------------------|-----------------------------------|  
|**/a/b/c/d/e**|La existencia del nodo `e` se evalúa en la cláusula FLWOR.|  
|**/a/b/c/d/e/f**|El valor del nodo `f` se evalúa en la cláusula FLWOR.|  
|**/a/b/c/d/e/g**|El método exist() evalúa la existencia del nodo `g` .|  
  

  
##  <a name="hints"></a> Especificar sugerencias de optimización  
 Puede usar sugerencias opcionales de optimización para especificar detalles de asignación adicionales para un nodo indizado mediante un índice XML selectivo. Por ejemplo, puede especificar el tipo de datos y la cardinalidad del nodo, así como cierta información sobre la estructura de los datos. Esta información adicional admite una mejor asignación. También consigue mejoras en el rendimiento, ahorros de almacenamiento o ambos.  
  
 El uso de sugerencias de optimización es opcional. Siempre puede aceptar las asignaciones predeterminadas, que son confiables pero no puede proporcionar un rendimiento y un almacenamiento óptimos.  
  
 Algunas sugerencias de optimización (por ejemplo, la sugerencia SINGLETON) presentan restricciones sobre los datos. En algunos casos, se pueden producir errores cuando esas restricciones no se cumplen.  
  
### <a name="benefits-of-optimization-hints"></a>Ventajas de las sugerencias de optimización  
 En la tabla siguiente se identifican las sugerencias de optimización que admiten un almacenamiento o un rendimiento más eficiente.  
  
|Sugerencia de optimización|Almacenamiento más eficiente|Rendimiento mejorado|  
|-----------------------|----------------------------|--------------------------|  
|**node()**|Sí|no|  
|**SINGLETON**|no|Sí|  
|**DATA TYPE**|Sí|Sí|  
|**MAXLENGTH**|Sí|Sí|  
  
### <a name="optimization-hints-and-data-types"></a>Sugerencias de optimización y tipos de datos  
 Puede indizar nodos como tipos de datos XQuery o como tipos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . En la tabla siguiente se muestran las sugerencias de optimización que se admiten con cada tipo de datos.  
  
|Sugerencia de optimización|Tipos de datos XQuery|Tipos de datos SQL|  
|-----------------------|-----------------------|--------------------|  
|**node()**|Sí|no|  
|**SINGLETON**|Sí|Sí|  
|**DATA TYPE**|Sí|no|  
|**MAXLENGTH**|Sí|no|  
  
### <a name="node-optimization-hint"></a>Sugerencia de optimización node()  
 Se aplica a: tipos de datos XQuery  
  
 Puede usar la optimización node() para especificar un nodo cuyo valor no es necesario para evaluar la consulta típica. Esta sugerencia reduce los requisitos de almacenamiento cuando la consulta típica solo tiene que evaluar la existencia del nodo. (De forma predeterminada, un índice XML selectivo almacena el valor para todos los nodos promovidos, excepto para los tipos de nodos complejos).  
  
 Considere el ejemplo siguiente:  
  
```tsql  
SELECT T.record FROM myXMLTable T  
WHERE T.xmldata.exist('/a/b[./c=5]') = 1  
```  
  
 Para usar un índice XML selectivo con el fin de evaluar esta consulta, promueva los nodos `b` y `c`. Sin embargo, puesto que el valor del nodo `b` no es necesario, puede usar la sugerencia node() con la siguiente sintaxis:  
  
 `/a/b/ as node()`  
  
 Si una consulta necesita el valor de un nodo que se ha indizado con la sugerencia node(), no se puede usar el índice XML selectivo.  
  
### <a name="singleton-optimization-hint"></a>Sugerencia de optimización SINGLETON  
 Se aplica a: tipos de datos XQuery o de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
 La sugerencia de optimización SINGLETON especifica la cardinalidad de un nodo. Esta sugerencia mejora el rendimiento de las consultas porque se sabe de antemano que un nodo aparece como máximo una vez dentro de su elemento primario o antecesor.  
  
 Examine el [documento XML de ejemplo](#sample) de este tema.  
  
 Para usar un índice XML selectivo con el fin de consultar este documento, puede especificar la sugerencia SINGLETON para el nodo `d` puesto que aparece como máximo una vez dentro de su elemento primario.  
  
 Si se ha especificado la sugerencia SINGLETON, pero un nodo aparece más de una vez dentro de su elemento primario o antecesor, se generará un error cuando cree el índice (para datos existentes) o cuando ejecute una consulta (para datos nuevos).  
  
### <a name="data-type-optimization-hint"></a>Sugerencia de optimización DATA TYPE  
 Se aplica a: tipos de datos XQuery  
  
 La sugerencia de optimización DATA TYPE permite especificar un tipo de datos XQuery o de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para el nodo indizado. El tipo de datos se usa para la columna de la tabla de datos del índice XML selectivo correspondiente al nodo indizado.  
  
 Al convertir un valor existente al tipo de datos especificado se produce un error y la operación de inserción (en el índice) funciona correctamente; sin embargo, se inserta un valor NULL en la tabla de datos del índice.  
  
### <a name="maxlength-optimization-hint"></a>Sugerencia de optimización MAXLENGTH  
 Se aplica a: tipos de datos XQuery  
  
 La sugerencia de optimización MAXLENGTH permite limitar la longitud de datos xs:string. MAXLENGTH no es pertinente para los tipos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , ya que especifica la longitud al especificar los tipos de fecha VARCHAR o NVARCHAR.  
  
 Cuando una cadena existente es más larga que el valor de MAXLENGTH especificado, se produce un error al insertar el valor en el índice.  
  

  
##  <a name="sample"></a> Documento XML de ejemplo  
 En los ejemplos de este tema se hace referencia al documento XML de ejemplo siguiente:  
  
```xml  
<a>  
    <b>  
         <c atc="aa">10</c>  
         <c atc="bb">15</c>  
         <d atd1="dd" atd2="ddd">md </d>  
    </b>  
     <b>  
        <c></c>  
        <c atc="">117</c>  
     </b>  
</a>  
```  
  

  
## <a name="see-also"></a>Vea también  
 [Índices XML selectivos &#40;SXI&#41;](../xml/selective-xml-indexes-sxi.md)   
 [Crear, modificar y quitar índices XML selectivos](../xml/create-alter-and-drop-selective-xml-indexes.md)  
  
  
