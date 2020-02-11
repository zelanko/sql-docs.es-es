---
title: Usar el modo EXPLICIT con FOR XML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- EXPLICIT FOR XML mode
- FOR XML clause, EXPLICIT mode
- FOR XML EXPLICIT mode
ms.assetid: 8b26e8ce-5465-4e7a-b237-98d0f4578ab1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8976b77bf0823c9735e6e6e67fc3159bcb54ecdf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63231269"
---
# <a name="use-explicit-mode-with-for-xml"></a>Usar el modo EXPLICIT con FOR XML
  Como se describe en el tema [generar XML mediante for XML](../xml/for-xml-sql-server.md), el modo Raw y auto no proporciona mucho control sobre la forma del XML generado a partir del resultado de una consulta. Sin embargo, el modo EXPLICIT ofrece la máxima flexibilidad para generar el XML que se desee a partir del resultado de una consulta.  
  
 La consulta en modo EXPLICIT debe escribirse de una determinada manera para poder especificar explícitamente la información adicional sobre el XML requerido, como el anidamiento esperado en el XML, como parte de la propia consulta. Dependiendo del XML que se solicite, la escritura de consultas en modo EXPLICIT puede resultar complicada. Tal vez, una alternativa más sencilla que escribir consultas en modo EXPLICIT sea [usar el modo PATH](../xml/use-path-mode-with-for-xml.md) con anidamiento.  
  
 En modo EXPLICIT, el XML que se desea se describe como parte de la consulta, por lo que es necesario asegurarse de que el XML generado sea correcto y válido.  
  
## <a name="rowset-processing-in-explicit-mode"></a>Procesar conjuntos de filas en modo EXPLICIT  
 El modo EXPLICIT transforma en un documento XML el conjunto de filas resultante de la ejecución de la consulta. Para que el modo EXPLICIT pueda generar el documento XML, el conjunto de filas debe ajustarse a un determinado formato. Por ello, es necesario escribir la consulta SELECT para generar el conjunto de filas, la **tabla universal**, con un formato específico que permita a la lógica del procesamiento generar el XML deseado.  
  
 En primer lugar, la consulta debe crear las dos columnas de metadatos siguientes:  
  
-   La primera columna debe proporcionar el número de etiqueta, el tipo de entero, del elemento actual, y el nombre de la columna debe ser **Tag**. La consulta debe proporcionar un número de etiqueta único para cada elemento que se vaya a construir a partir del conjunto de filas.  
  
-   La segunda columna debe proporcionar un número de etiqueta del elemento primario, y el nombre de la columna debe ser **Parent**. De este modo, las columnas Tag y Parent ofrecen información sobre la jerarquía.  
  
 Los valores de estas columnas de metadatos, junto con la información de los nombres de columna, se usan para generar el XML deseado. Tenga en cuenta que la consulta debe proporcionar los nombres de columna de una manera determinada. Observe también que un valor 0 ó NULL en la columna **Parent** indica que el elemento correspondiente no tiene uno primario. El elemento se agrega al XML como elemento de nivel superior.  
  
 Para comprender cómo se procesa la tabla universal generada por una consulta para obtener el XML resultante, suponga que ha escrito una consulta que genera esta tabla universal:  
  
 ![Ejemplo de tabla universal](../../database-engine/media/xmlutable.gif "Ejemplo de tabla universal")  
  
 Observe lo siguiente en esta tabla universal:  
  
-   Las dos primeras columnas son **Tag** y **Parent** y son de metadatos. Estos valores determinan la jerarquía.  
  
-   Los nombres de columna se han especificado de una manera determinada, como se describe más adelante en este tema.  
  
-   Al generar el XML a partir de esta tabla universal, se crea una partición vertical de los datos de la tabla en grupos de columnas. La agrupación se determina en función del valor de **Tag** y los nombres de columna. Al crear XML, la lógica de procesamiento selecciona un grupo de columnas para cada fila y construye un elemento. En este ejemplo, se observa lo siguiente:  
  
    -   Para el valor 1 de la columna **Tag** en la primera fila, las columnas cuyos nombres incluyen el mismo número de etiqueta, **Customer!1!cid** y **Customer!1!name**, forman un grupo. Estas columnas se utilizan para procesar la fila, y se observa que la forma del elemento generado es <`Customer id=... name=...`>. El formato del nombre de columna se describe más adelante en este tema.  
  
    -   Para las filas con valor 2 en la columna **Tag**, las columnas **Order!2!id** y **Order!2!date** forman un grupo que se usa después para construir elementos, <`Order id=... date=... /`>.  
  
    -   Para las filas con valor 3 en la columna **Tag**, las columnas **OrderDetail!3!id!id** y **OrderDetail!3!pid!idref** forman un grupo. Cada una de estas filas genera un elemento, <`OrderDetail id=... pid=...`>, a partir de estas columnas.  
  
-   Tenga en cuenta que, al generar la jerarquía en XML, las filas se procesan por orden. La jerarquía XML se determina como se indica a continuación:  
  
    -   La primera fila especifica el valor 1 en **Tag** y el valor NULL en **Parent** . Por lo tanto, el elemento correspondiente, <`Customer`>, se agrega al XML como elemento de nivel superior.  
  
        ```  
        <Customer cid="C1" name="Janine">  
        ```  
  
    -   La segunda fila identifica el valor 2 en **Tag** y el valor 1 en **Parent** . Por tanto, se agrega un elemento <`Order`> como elemento secundario del elemento <`Customer`>.  
  
        ```  
        <Customer cid="C1" name="Janine">  
           <Order id="O1" date="1/20/1996">  
        ```  
  
    -   Las dos filas siguientes identifican el valor 3 en **Tag** y el valor 2 en **Parent** . Por tanto, se agregan dos elementos <`OrderDetail`> como elementos secundarios del elemento <`Order`>.  
  
        ```  
        <Customer cid="C1" name="Janine">  
           <Order id="O1" date="1/20/1996">  
              <OrderDetail id="OD1" pid="P1"/>  
              <OrderDetail id="OD2" pid="P2"/>  
        ```  
  
    -   La última fila identifica 2 como número de etiqueta en **Tag** y 1 como número de etiqueta en **Parent** . Por lo tanto, se agrega otro elemento secundario <`Order`> al elemento primario <`Customer`>.  
  
        ```  
        <Customer cid="C1" name="Janine">  
           <Order id="O1" date="1/20/1996">  
              <OrderDetail id="OD1" pid="P1"/>  
              <OrderDetail id="OD2" pid="P2"/>  
           </Order>  
           <Order id="O2" date="3/29/1997">  
        </Customer>  
        ```  
  
 En resumen, los valores de las columnas de metadatos **Tag** y **Parent** , la información proporcionada en los nombres de columna y el orden correcto de las filas generan el XML deseado al utilizar el modo EXPLICIT.  
  
### <a name="universal-table-row-ordering"></a>Ordenación de las filas en la tabla universal  
 Al generar el XML, las filas de la tabla universal se procesan por orden. Por tanto, para recuperar las instancias secundarias correctas asociadas a su instancia primaria, las filas del conjunto de filas deben estar ordenadas de modo que a cada nodo principal le sigan directamente sus nodos secundarios.  
  
## <a name="specifying-column-names-in-a-universal-table"></a>Especificar nombres de columna en una tabla universal  
 Al escribir consultas en modo EXPLICIT, los nombres de columna del conjunto de filas resultante se deben especificar con este formato. Ofrecen información de transformación, incluidos nombres de elementos y atributos y otros datos, especificada mediante el uso de directivas.  
  
 Éste es el formato general:  
  
```  
  
ElementName!TagNumber!AttributeName!Directive  
```  
  
 A continuación, se describe cada parte del formato.  
  
 *ElementName*  
 Es el identificador genérico resultante del elemento. Por ejemplo, si se especifica **Customers** como *ElementName*, \<se genera el elemento customers>.  
  
 *TagNumber*  
 Es un valor de etiqueta único asignado a un elemento. Este valor, junto con las dos columnas de metadatos **Tag** y **Parent**, determina el anidamiento de los elementos en el XML resultante.  
  
 *AttributeName*  
 Proporciona el nombre del atributo que se va a crear en el identificador *ElementName*especificado. Éste es el comportamiento si no se especifica *Directive* .  
  
 Si se especifica *Directive* y es **xml**, **cdata**o **element**, este valor se utiliza para crear un elemento secundario de *ElementName*, y se le agrega el valor de la columna.  
  
 Si se especifica *Directive*, *AttributeName* puede estar vacío. Por ejemplo, ElementName!TagNumber!!Directive. En este caso, el valor de la columna está incluido directamente en el *ElementName*.  
  
 *Directiva*  
 *Directive* es opcional y se puede usar para proporcionar información adicional para la construcción del XML. *La Directiva* tiene dos propósitos.  
  
 Uno de los objetivos es codificar valores como ID, IDREF e IDREFS. Puede especificar palabras clave **ID**, **IDREF**e **IDREFS** como valores de *Directive*. Estas directivas sobrescriben los tipos de atributo. De este modo, puede crear vínculos entre documentos.  
  
 También puede usar *Directive* para indicar la forma de asignar los datos de cadena a XML. Las palabras clave **hide**, **element, elementxsinil**, **xml**, **xmltext**y **cdata** se pueden usar como *Directive*. La directiva **hide** oculta el nodo. Es útil cuando se recuperan valores solo para ordenarlos, sin incluirlos en el XML resultante.  
  
 La directiva **element** genera un elemento contenido en lugar de un atributo. Los datos contenidos se codifican como entidad. Por ejemplo, el **<** carácter se &lt;convierte en. En el caso de valores de columna NULL, no se genera ningún elemento. Si desea que se genere un elemento para valores de columna NULL, puede especificar la directiva **elementxsinil** . De este modo, se generará un elemento con el atributo sxi:nil=TRUE.  
  
 La directiva **xml** es la misma que la directiva **element** , excepto en que no se produce la codificación de entidades. Observe que la directiva **element** se puede combinar con **ID**, **IDREF**o **IDREFS**, mientras que la directiva **xml** no se puede combinar con ninguna otra directiva, excepto **hide**.  
  
 La directiva **cdata** Incluye los datos englobándolos en una sección CDATA. El contenido no se codifica por entidad. El tipo de datos original debe ser de texto, como **varchar**, **nvarchar**, **text**o **ntext**. Esta directiva solo puede utilizarse con **hide**. Si se utiliza esta directiva, no debe especificarse *AttributeName* .  
  
 La combinación de directivas entre estos dos grupos es válida en la mayoría de los casos, pero no se permite la combinación entre ellas mismas.  
  
 Si no se especifican *Directive* ni *AttributeName* (por ejemplo, **Customer!1**), se implica una directiva **element** (como **Customer!1!!element**) y los datos de columna se incluyen en *ElementName*.  
  
 Si se especifica la directiva **xmltext** , el contenido de la columna se incluye en una única etiqueta que se integrará con el resto del documento. Esta directiva es útil para capturar los datos XML de desbordamiento no utilizados que OPENXML almacena en una columna. Para obtener más información, vea [OPENXML &#40;SQL Server&#41;](../xml/openxml-sql-server.md).  
  
 Si se especifica *AttributeName* , el nombre de etiqueta se sustituye por el nombre especificado. En caso contrario, el atributo se agrega a la lista actual de atributos de los elementos que los incluyen colocando el contenido al principio del contenido sin codificación de entidades. La columna con esta directiva debe ser de tipo texto, como **varchar**, **nvarchar**, **char**, **nchar**, **text**o **ntext**. Esta directiva solo puede utilizarse con **hide**. Esta directiva es útil para capturar los datos de desbordamiento almacenados en una columna. Si el contexto no es un XML bien estructurado, el comportamiento no está definido.  
  
## <a name="in-this-section"></a>En esta sección  
 Los siguientes ejemplos ilustran el uso del modo EXPLICIT.  
  
-   [Ejemplo: Recuperar información de los empleados](../xml/example-retrieving-employee-information.md)  
  
-   [Ejemplo: Especificar la directiva ELEMENT](../xml/example-specifying-the-element-directive.md)  
  
-   [Ejemplo: Especificar la directiva ELEMENTXSINIL](../xml/example-specifying-the-elementxsinil-directive.md)  
  
-   [Ejemplo: Construir elementos del mismo nivel con el modo EXPLICIT](../xml/example-constructing-siblings-with-explicit-mode.md)  
  
-   [Ejemplo: especificar las directivas ID e IDREF](../xml/example-specifying-the-id-and-idref-directives.md)  
  
-   [Ejemplo: Especificar las directivas ID e IDREFS](../xml/example-specifying-the-id-and-idrefs-directives.md)  
  
-   [Ejemplo: Especificar la directiva HIDE](../xml/example-specifying-the-hide-directive.md)  
  
-   [Ejemplo: Especificar la directiva ELEMENT y la codificación de entidades](../xml/example-specifying-the-element-directive-and-entity-encoding.md)  
  
-   [Ejemplo: Especificar la directiva CDATA](../xml/example-specifying-the-cdata-directive.md)  
  
-   [Ejemplo: Especificar la directiva XMLTEXT](../xml/example-specifying-the-xmltext-directive.md)  
  
## <a name="see-also"></a>Consulte también  
 [Usar el modo RAW con FOR XML](../xml/use-raw-mode-with-for-xml.md)   
 [Usar el modo AUTO con FOR XML](../xml/use-auto-mode-with-for-xml.md)   
 [Usar el modo PATH con FOR XML](../xml/use-path-mode-with-for-xml.md)   
 [SELECT &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql)   
 [FOR XML &#40;SQL Server&#41;](../xml/for-xml-sql-server.md)  
  
  
