---
title: "PARA (cláusula de Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 08/09/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FOR
- FOR CLAUSE
- FOR_TSQL
- FOR_CLAUSE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- XML option [SQL Server]
- BROWSE option
- FOR clause [Transact-SQL]
ms.assetid: 08a6f084-8f73-4f2a-bae4-3c7513dc99b9
caps.latest.revision: 54
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: f092e78608e8fa2b44061056ef4e5b9e7e1649a7
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="select---for-clause-transact-sql"></a>SELECT - FOR (cláusula de Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Utilice la cláusula FOR para especificar una de las siguientes opciones para los resultados de la consulta.  
  
-   Permitir actualizaciones mientras está viendo los resultados de la consulta en un cursor de modo de exploración mediante la especificación de **FOR BROWSE**.  
  
-   Dar formato a resultados de la consulta como XML mediante la especificación de **FOR XML**.  
  
-   Dar formato a resultados de la consulta como JSON mediante la especificación de **FOR JSON**.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
[ FOR { BROWSE | <XML> | <JSON>} ]  
  
<XML> ::=  
XML   
{   
    { RAW [ ( 'ElementName' ) ] | AUTO }   
    [   
        <CommonDirectivesForXML>   
        [ , { XMLDATA | XMLSCHEMA [ ( 'TargetNameSpaceURI' ) ] } ]   
        [ , ELEMENTS [ XSINIL | ABSENT ]   
    ]  
  | EXPLICIT   
    [   
        <CommonDirectivesForXML>   
        [ , XMLDATA ]   
    ]  
  | PATH [ ( 'ElementName' ) ]   
    [  
        <CommonDirectivesForXML>   
        [ , ELEMENTS [ XSINIL | ABSENT ] ]  
    ]  
}   
  
<CommonDirectivesForXML> ::=   
[ , BINARY BASE64 ]  
[ , TYPE ]  
[ , ROOT [ ( 'RootName' ) ] ]  
  
<JSON> ::=  
JSON   
{   
    { AUTO | PATH }   
    [   
        [ , ROOT [ ( 'RootName' ) ] ]  
        [ , INCLUDE_NULL_VALUES ]  
        [ , WITHOUT_ARRAY_WRAPPER ]  
    ]  
  
}  
```  
  
## <a name="for-browse"></a>FOR BROWSE  
 BROWSE  
 Especifica que se permiten las actualizaciones mientras se visualizan los datos en el cursor del modo de exploración de DB-Library. Una tabla se puede examinar en una aplicación si la tabla incluye una **timestamp** columna, la tabla tiene un índice único y la opción FOR BROWSE está al final de las instrucciones SELECT enviadas a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  No se puede utilizar el \<lock_hint > HOLDLOCK en una instrucción SELECT que incluya la opción FOR BROWSE.
  
 FOR BROWSE no puede aparecer en instrucciones SELECT combinadas mediante el operador UNION.  
  
> [!NOTE]  
>  Cuando las columnas de clave de índice único de una tabla pueden aceptar valores NULL, y la tabla está en la parte interna de la combinación externa, el índice no se admite en el modo de exploración.  
  
 El modo de exploración permite examinar las filas de la tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y actualizar los datos de la tabla fila por fila. Para tener acceso a un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tabla en la aplicación en el modo de exploración, debe utilizar una de las dos opciones siguientes:  
  
-   La instrucción SELECT que utiliza para tener acceso a los datos de su [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe terminar con las palabras clave de la tabla **FOR BROWSE**. Al activar la **FOR BROWSE** opción para usar el modo de exploración, se crean tablas temporales.  
  
-   Debe ejecutar las siguientes [!INCLUDE[tsql](../../includes/tsql-md.md)] instrucción que se va a activar el modo de exploración utilizando la **NO_BROWSETABLE** opción:  
  
    ```  
    SET NO_BROWSETABLE ON  
    ```  
  
     Al activar la **NO_BROWSETABLE** opción, todas las instrucciones SELECT se comportan como si la **FOR BROWSE** opción se anexa a las instrucciones. Sin embargo, el **NO_BROWSETABLE** opción no crea las tablas temporales que la **FOR BROWSE** opción normalmente se usa para enviar los resultados a la aplicación.  
  
 Cuando intenta tener acceso a los datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tablas en modo de exploración utilizando una consulta SELECT que implica una instrucción de combinación externa y, cuando se define un índice único en la tabla que está presente en el lado interno de una instrucción de combinación externa, el modo de exploración no sup puerto el índice único. El modo de exploración únicamente admite el índice único cuando todas las columnas de clave de índice único pueden aceptar valores NULL. El modo de exploración no admite el índice único si se cumplen las condiciones siguientes:  
  
-   Intenta obtener acceso a los datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tablas en modo de exploración utilizando una consulta SELECT que implica una instrucción de combinación externa.  
  
-   Un índice único se define en la tabla que está presente en el lado interno de una instrucción de combinación externa.  
  
 Para reproducir este comportamiento en el modo de exploración, siga estos pasos:  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], cree una base de datos denominada SampleDB.  
  
2.  En la base de datos SampleDB, cree una tabla tleft y una tabla tright que contengan ambas una única columna que se denomine c1. Defina un índice único en la columna c1 de la tabla tleft y establezca la columna para aceptar valores NULL. Para ello, ejecute las instrucciones de [!INCLUDE[tsql](../../includes/tsql-md.md)] siguientes en una ventana de consulta adecuada:  
  
    ```  
    CREATE TABLE tleft(c1 INT NULL UNIQUE) ;  
    GO   
    CREATE TABLE tright(c1 INT NULL) ;  
    GO  
    ```  
  
3.  Inserte varios valores en las tablas tleft y tright. Asegúrese de insertar un valor NULL en la tabla tleft. Para ello, ejecute las instrucciones de [!INCLUDE[tsql](../../includes/tsql-md.md)] siguientes en la ventana de consulta:  
  
    ```  
    INSERT INTO tleft VALUES(2) ;  
    INSERT INTO tleft VALUES(NULL) ;  
    INSERT INTO tright VALUES(1) ;  
    INSERT INTO tright VALUES(3) ;  
    INSERT INTO tright VALUES(NULL) ;  
    GO  
    ```  
  
4.  Activar la **NO_BROWSETABLE** opción. Para ello, ejecute las instrucciones de [!INCLUDE[tsql](../../includes/tsql-md.md)] siguientes en la ventana de consulta:  
  
    ```  
    SET NO_BROWSETABLE ON ;  
    GO  
    ```  
  
5.  Obtenga acceso a los datos de las tablas tleft y tright utilizando una instrucción de combinación externa en la consulta SELECT. Asegúrese de que la tabla tleft está en el lado interno de la instrucción de combinación externa. Para ello, ejecute las instrucciones de [!INCLUDE[tsql](../../includes/tsql-md.md)] siguientes en la ventana de consulta:  
  
    ```  
    SELECT tleft.c1   
    FROM tleft   
    RIGHT JOIN tright   
    ON tleft.c1 = tright.c1   
    WHERE tright.c1 <> 2 ;  
  
    ```  
  
     Observe la salida siguiente en el panel Resultados:  
  
     c1  
  
     ---\-  
  
     NULL  
  
     NULL  
  
 Después de ejecutar la consulta SELECT para obtener acceso a las tablas en el modo de exploración, el conjunto de resultados de la consulta SELECT contiene dos valores NULL para la columna c1 de la tabla tleft debido a la definición de la instrucción de combinación externa derecha. Por consiguiente, en el conjunto de resultados no puede distinguir entre los valores NULL que procedían de la tabla y los incluidos por la instrucción de combinación externa derecha. Puede recibir resultados incorrectos si debe omitir los valores NULL del conjunto de resultados.  
  
> [!NOTE]  
>  Si las columnas que están incluidas en el índice único no aceptan valores NULL, todos los valores NULL en el conjunto de resultados fueron incluidos por la instrucción de combinación externa.  
  
## <a name="for-xml"></a>FOR XML  
 XML  
 Especifica que el resultado de una consulta se devolverá como documento XML. Debe especificarse uno de los siguientes modos XML: RAW, AUTO, EXPLICIT. Para obtener más información acerca de los datos XML y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [FOR XML &#40; SQL Server &#41; ](../../relational-databases/xml/for-xml-sql-server.md).  
  
 Sin formato [ **('***ElementName***')** ]  
 Obtiene el resultado de la consulta y transforma cada fila del conjunto de resultados en un elemento XML con un identificador genérico \<fila / > como etiqueta del elemento. Opcionalmente, puede especificar un nombre para el elemento de fila. La salida XML resultante utiliza especificado *ElementName* como el elemento de fila generado para cada fila. Para obtener más información, consulte [usar el modo RAW con FOR XML](../../relational-databases/xml/use-raw-mode-with-for-xml.md) y [usar el modo RAW con FOR XML](../../relational-databases/xml/use-raw-mode-with-for-xml.md).  
  
 AUTO  
 Devuelve los resultados de la consulta en un árbol anidado XML sencillo. Cada tabla de la cláusula FROM, para la que al menos se presenta una columna en la cláusula SELECT, se representa como elemento XML. A las columnas presentadas en la cláusula SELECT se les asignan los atributos de elemento apropiados. Para obtener más información, vea [Usar el modo AUTO con FOR XML](../../relational-databases/xml/use-auto-mode-with-for-xml.md).  
  
 EXPLICIT  
 Especifica que la forma del árbol XML resultante está definida explícitamente. Con este modo, las consultas deben escribirse de una determinada manera para que pueda especificar explícitamente información adicional acerca de la anidación deseada. Para obtener más información, vea [Usar el modo EXPLICIT con FOR XML](../../relational-databases/xml/use-explicit-mode-with-for-xml.md).  
  
 XMLDATA  
 Devuelve el esquema XDR insertado, pero no agrega el elemento raíz al resultado. Si se especifica XMLDATA, el esquema XDR se agrega al documento.  
  
> [!IMPORTANT]  
>  La directiva XMLDATA está en desuso. Utilice la XSD generación en los modos RAW y AUTO. No hay sustitución para la directiva XMLDATA en modo EXPLICIT. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 XMLSCHEMA [ **('***TargetNameSpaceURI***')** ]  
 Devuelve el esquema XSD insertado. Opcionalmente puede especificar un URI de espacio de nombres de destino al especificar esta directiva, que devuelve el espacio de nombres especificado en el esquema. Para obtener más información, vea [Generar un esquema XSD insertado](../../relational-databases/xml/generate-an-inline-xsd-schema.md).  
  
 ELEMENTS  
 Especifica que las columnas se devuelven como subelementos. Sin embargo, se les asignan atributos XML. Esta opción solo se admite en los modos RAW, AUTO y PATH. Para obtener más información, vea [Usar el modo RAW con FOR XML](../../relational-databases/xml/use-raw-mode-with-for-xml.md).  
  
 XSINIL  
 Especifica que un elemento con **xsi: nil** atributo establecido en **True** pueden crear para los valores de columna NULL. Esta opción solo se puede especificar con la directiva ELEMENTS. Para obtener más información, consulte [generar elementos para valores NULL con el parámetro XSINIL](../../relational-databases/xml/generate-elements-for-null-values-with-the-xsinil-parameter.md).  
  
 ABSENT  
 Indica que para los valores de columna NULL, no se agregarán los elementos XML correspondientes en el resultado XML. Especifique esta opción solo con ELEMENTS.  
  
 Ruta de acceso [ **('***ElementName***')** ]  
 Genera un \<fila > contenedor de elemento para cada fila del conjunto de resultados. Opcionalmente, puede especificar un nombre de elemento para el \<fila > contenedor de elementos. Si se ha proporcionado una cadena vacía como FOR XML PATH (**''**)), no se genera un elemento contenedor. El uso de PATH puede proporcionar una alternativa más sencilla a consultas escritas con la directiva EXPLICIT. Para obtener más información, vea [Usar el modo PATH con FOR XML](../../relational-databases/xml/use-path-mode-with-for-xml.md).  
  
 BINARY BASE64  
 Especifica que la consulta devuelve los datos binarios en el formato codificado BINARY BASE64. Al recuperar datos binarios mediante el modo RAW y EXPLICIT, se debe especificar esta opción. Éste es el valor predeterminado en el modo AUTO.  
  
 TYPE  
 Especifica que la consulta devuelve los resultados como **xml** tipo. Para más información, consulte [TYPE Directive in FOR XML Queries](../../relational-databases/xml/type-directive-in-for-xml-queries.md).  
  
 RAÍZ [ **('***RootName***')** ]  
 Especifica que se va a agregar un solo elemento de nivel superior al XML resultante. También se puede especificar el nombre del elemento raíz que se generará. Si no se especifica el nombre de raíz opcional, el valor predeterminado \<raíz > se agrega el elemento.  
  
 Para obtener más información, consulte [FOR XML &#40; SQL Server &#41; ](../../relational-databases/xml/for-xml-sql-server.md).  
  
 **Por ejemplo, XML**  
  
 En el siguiente ejemplo se especifica `FOR XML AUTO` con las opciones `TYPE` y `XMLSCHEMA`. Causa de la `TYPE` opción, el conjunto de resultados se devuelve al cliente como un **xml** tipo. La opción `XMLSCHEMA` especifica que el esquema XSD insertado está incluido en los datos XML devueltos y la opción `ELEMENTS` especifica que el resultado XML está centrado en elementos.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT p.BusinessEntityID, FirstName, LastName, PhoneNumber AS Phone  
FROM Person.Person AS p  
JOIN Person.PersonPhone AS pph ON p.BusinessEntityID  = pph.BusinessEntityID  
WHERE LastName LIKE 'G%'  
ORDER BY LastName, FirstName   
FOR XML AUTO, TYPE, XMLSCHEMA, ELEMENTS XSINIL;  
```  
  
## <a name="for-json"></a>FOR JSON  
 JSON  
 Especificar FOR JSON para devolver los resultados de una consulta con formato de texto JSON. También tiene que especificar uno de los siguientes modos JSON: AUTO o ruta de acceso. Para obtener más información sobre la **FOR JSON** cláusula, vea [Format Query Results resultados como JSON con FOR JSON &#40; SQL Server &#41; ](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md).  
  
 AUTO  
 Basada en el formato JSON a la salida automáticamente en la estructura de la **seleccione** instrucción  
            mediante la especificación de **FOR JSON AUTO**. Para más información y ejemplos, vea [Aplicar formato a la salida JSON automáticamente con el modo AUTO &#40;SQL Server&#41;](../../relational-databases/json/format-json-output-automatically-with-auto-mode-sql-server.md).  
  
 PATH  
 Obtener el control completo sobre el formato de la salida JSON mediante la especificación   
            **FOR JSON PATH**. El modo**PATH** le permite crear objetos contenedores y anidar propiedades complejas. Para más información y ejemplos, vea [Format Nested JSON Output with PATH Mode &#40;SQL Server&#41;](../../relational-databases/json/format-nested-json-output-with-path-mode-sql-server.md) (Aplicar formato a la salida JSON automáticamente con el modo PATH &#40;SQL Server&#41;).  
  
 INCLUDE_NULL_VALUES  
 Incluir valores null en la salida JSON mediante la especificación de la **INCLUDE_NULL_VALUES** opción con la **FOR JSON** cláusula. Si no especifica esta opción, la salida no incluye las propiedades JSON para valores null en los resultados de la consulta. Para obtener más información y ejemplos, vea [incluir valores Null en la salida de JSON con la opción INCLUDE_NULL_VALUES &#40; SQL Server &#41; ](../../relational-databases/json/include-null-values-in-json-include-null-values-option.md).  
  
 RAÍZ [ **('***RootName***')** ]  
 Agregar un único elemento de nivel superior a la salida JSON mediante la especificación de la **raíz** opción con la **FOR JSON** cláusula. Si no especifica la opción **ROOT** , la salida JSON no tiene un elemento raíz. Para obtener más información y ejemplos, vea [agregar un nodo raíz a la salida de JSON con la opción ROOT &#40; SQL Server &#41; ](../../relational-databases/json/add-a-root-node-to-json-output-with-the-root-option-sql-server.md).  
  
 WITHOUT_ARRAY_WRAPPER  
 Quitar los corchetes que rodean la salida JSON de forma predeterminada mediante la especificación de la **WITHOUT_ARRAY_WRAPPER** opción con la **FOR JSON** cláusula. Si no especifica esta opción, la salida JSON aparecerá entre corchetes. Use la **WITHOUT_ARRAY_WRAPPER** opción para generar un objeto JSON único como salida.  Para obtener más información, vea [Quitar corchetes de la salida JSON con la opción WITHOUT_ARRAY_WRAPPER &#40;SQL Server&#41;](../../relational-databases/json/remove-square-brackets-from-json-without-array-wrapper-option.md).  
  
 Para obtener más información, vea [Format Query Results as JSON with FOR JSON &#40;SQL Server&#41; (Aplicar el formato JSON a los resultados de la consulta con FOR JSON &#40;SQL Server&#41;)](../../relational-databases/json/format-query-results-as-json-with-for-json-sql-server.md).  
  
## <a name="see-also"></a>Vea también  
 [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md)  
  
  

