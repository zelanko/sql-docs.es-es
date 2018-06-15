---
title: Índices XML (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: xml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- removing indexes
- deleting indexes
- secondary indexes [XML in SQL Server]
- xml data type [SQL Server], indexes
- dropping indexes
- PATH index
- DROP_EXISTING clause
- XML [SQL Server], indexes
- primary indexes [XML in SQL Server]
- indexes [SQL Server], XML
- XML indexes [SQL Server], secondary
- BLOBs, XML indexes
- disabling indexes
- XML indexes [SQL Server], modifying
- XML indexes [SQL Server]
- XML indexes [SQL Server], primary
- modifying indexes
- XML indexes [SQL Server], dropping
- VALUE index
- XML indexes [SQL Server], xml data type
- PROPERTY index
- XML indexes [SQL Server], creating
ms.assetid: f5c9209d-b3f3-4543-b30b-01365a5e7333
caps.latest.revision: 59
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 7b5109d315e3c4bafdf7af1d1c8b1bf3734e3e6d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "33017982"
---
# <a name="xml-indexes-sql-server"></a>Índices XML (SQL Server)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Es posible crear índices XML en columnas del tipo de datos **xml** . Se indizan todas las etiquetas, los valores y las rutas de acceso de las instancias XML de la columna y se mejora el rendimiento de las consultas. Un índice XML puede afectar positivamente a una aplicación en estas situaciones:  
  
-   Las consultas en columnas XML son habituales en su carga de trabajo. Es preciso considerar el costo de mantenimiento del índice XML durante la modificación de datos.  
  
-   Los valores XML son relativamente grandes y las partes recuperadas son relativamente pequeñas. La generación del índice evita tener que analizar todo el conjunto de datos en tiempo de ejecución y favorece las búsquedas basadas en índices que permiten un procesamiento más eficiente de las consultas.  
  
 Los índices XML se dividen en las categorías siguientes:  
  
-   Índice XML principal  
  
-   Índice XML secundario  
  
 El primer índice de la columna de tipo **xml** debe ser el índice XML principal. Con el índice XML principal, se admiten los siguientes tipos de índices secundarios: PATH, VALUE y PROPERTY. Dependiendo del tipo de consulta, los índices secundarios pueden contribuir a mejorar el rendimiento.  
  
> [!NOTE]  
>  No puede crear o modificar un índice XML si las opciones de base de datos no están establecidas correctamente para trabajar con el tipo de datos **xml** . Para obtener más información, vea [Usar la búsqueda de texto completo con columnas XML](../../relational-databases/xml/use-full-text-search-with-xml-columns.md).  
  
 Las instancias XML se almacenan en las columnas de tipo **xml** como objetos binarios grandes (BLOB). Estas instancias XML pueden ser grandes, y la representación binaria almacenada de instancias de datos de tipo **xml** puede tener un tamaño de hasta 2 GB. Sin ningún índice, estos objetos binarios grandes se dividen en tiempo de ejecución para evaluar una consulta. Este proceso de división puede resultar lento. Por ejemplo, considere la siguiente consulta:  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS "PD")  
  
SELECT CatalogDescription.query('  
  /PD:ProductDescription/PD:Summary  
') as Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist ('/PD:ProductDescription/@ProductModelID[.="19"]') = 1  
```  
  
 Para seleccionar instancias XML que cumplan la condición de la cláusula `WHERE` , el objeto binario grande (BLOB) XML de cada fila de la tabla `Production.ProductModel` se divide en tiempo de ejecución. A continuación, se evalúa la expresión `(/PD:ProductDescription/@ProductModelID[.="19"]`) en el método `exist()` . Esta división en tiempo de ejecución puede ser costosa, en función del tamaño y el número de instancias almacenadas en la columna.  
  
 Si las consultas de objetos binarios grandes (BLOB) XML son frecuentes en su entorno de aplicación, será útil indexar las columnas de tipo **xml** . No obstante, el mantenimiento del índice durante la modificación de datos lleva un costo asociado.  
  
## <a name="primary-xml-index"></a>Índice XML principal  
 El índice XML principal incluye todas las etiquetas, los valores y las rutas de acceso de las instancias XML de una columna XML. Para crear un índice XML principal, la tabla que contiene la columna XML, debe tener un índice clúster en la clave principal de la tabla. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza esta clave principal para correlacionar las filas del índice XML principal con las filas de la tabla que contiene la columna XML.  
  
 El índice XML principal es una representación dividida y persistente de los objetos binarios grandes (BLOB) XML de la columna de tipo de datos **xml** . Para cada BLOB XML de la columna, el índice crea varias filas de datos. El número de filas del índice es prácticamente igual al número de nodos del BLOB XML. Cuando una consulta recupera la instancia XML completa, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona la instancia a partir de la columna XML. Las consultas dentro de instancias XML usan el índice XML principal y pueden devolver valores escalares o subárboles XML utilizando el propio índice.  
  
 Cada fila almacena la siguiente información acerca del nodo:  
  
-   Nombre de etiqueta (p. ej., un nombre de elemento o atributo).  
  
-   Valor del nodo.  
  
-   Tipo de nodo (p. ej., un nodo de elemento, de atributo o de texto).  
  
-   Información del pedido de documento, representado mediante un identificador de nodo interno.  
  
-   Ruta de acceso desde cada nodo a la raíz del árbol XML. La consulta busca expresiones de ruta en esta columna.  
  
-   Clave principal de la tabla base. La clave principal de la tabla base está duplicada en el índice XML principal para mantener la combinación con la tabla base, y el número máximo de columnas en la clave principal de la tabla base se limita a 15.  
  
 Esta información de nodo se utiliza para evaluar y crear resultados XML para una consulta específica. Con fines de optimización, la información de nombre de etiqueta y tipo de nodo se codifica en forma de valores enteros; la columna Patch utiliza la misma codificación. Asimismo, las rutas de acceso se almacenan en orden inverso para permitir rutas de acceso coincidentes cuando solo se conoce el sufijo de la ruta de acceso. Por ejemplo:  
  
-   `//ContactRecord/PhoneNumber` , donde solo se conocen los dos últimos pasos.  
  
 O BIEN  
  
-   `/Book/*/Title` donde el carácter comodín (`*`) se especifica en mitad de la expresión.  
  
 El procesador de consultas usa el índice XML principal para las consultas relacionadas con los [xml Data Type Methods](../../t-sql/xml/xml-data-type-methods.md) y devuelve valores escalares o los subárboles XML del propio índice principal. (Este índice almacena toda la información necesaria para volver a construir la instancia XML).  
  
 Por ejemplo, la siguiente consulta devuelve información de resumen almacenada en la columna de `CatalogDescription` tipo **xml** de la tabla `ProductModel`. La consulta devuelve información perteneciente a <`Summary`> solo para modelos de producto cuya descripción de catálogo también almacena información sobre <`Features`>.  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS "PD")SELECT CatalogDescription.query('  /PD:ProductDescription/PD:Summary') as ResultFROM Production.ProductModelWHERE CatalogDescription.exist ('/PD:ProductDescription/PD:Features') = 1  
```  
  
 En relación con el índice XML principal, en lugar de dividir cada instancia de BLOB XML en la tabla base, las filas del índice que corresponden a cada BLOB XML se examinan secuencialmente para determinar la expresión especificada en el método `exist()`. Si la ruta de acceso se encuentra en la columna Path del índice, el elemento <`Summary`> y sus subárboles se recuperan a partir del índice XML principal y se convierten en un BLOB XML como resultado del método `query()`.  
  
 Tenga en cuenta que el índice XML principal no se utiliza al recuperar una instancia XML completa. Por ejemplo, la consulta siguiente recupera de la tabla la instancia XML completa que describe las instrucciones de fabricación para un modelo determinado de producto.  
  
```  
USE AdventureWorks2012;SELECT InstructionsFROM Production.ProductModel WHERE ProductModelID=7;  
```  
  
## <a name="secondary-xml-indexes"></a>Índices XML secundarios  
 Para mejorar los resultados de las búsquedas, pueden crearse índices XML secundarios. Antes de crear índices secundarios, debe existir un índice XML principal. A continuación, se indican los tipos existentes:  
  
-   Índice XML secundario PATH  
  
-   Índice XML secundario VALUE  
  
-   Índice XML secundario PROPERTY  
  
 A continuación se incluyen algunas directrices para crear uno o varios índices secundarios:  
  
-   Si la carga de trabajo incluye numerosas expresiones de ruta de acceso en las columnas XML, es probable que el índice XML secundario PATH reduzca la carga de trabajo. El caso más habitual es el uso del método **exist()** con columnas XML en la cláusula WHERE de Transact-SQL.  
  
-   Si la carga de trabajo recupera varios valores a partir de instancias XML individuales empleando expresiones de ruta de acceso, puede resultar útil la agrupación en clústeres de las rutas dentro de cada instancia XML en el índice PROPERTY. Éste suele ser el caso de una bolsa de propiedades, cuando se capturan las propiedades de un objeto y se conoce el valor de su clave principal.  
  
-   Si la carga de trabajo implica consultar valores dentro de instancias XML sin conocer los nombres de los elementos o atributos que contienen dichos valores, puede ser útil crear el índice VALUE. Esto suele ocurrir con búsquedas en ejes descendentes, como //author[last-name="Howard"], en que los elementos \<author> pueden aparecer en cualquier nivel de la jerarquía. También ocurre en consultas con caracteres comodín, como /book [@* = "novel"], en que la consulta busca elementos \<book> que tengan algún atributo con el valor "novel".  
  
### <a name="path-secondary-xml-index"></a>Índice XML secundario PATH  
 Si sus consultas suelen especificar expresiones de ruta de acceso en columnas de tipo **xml** , un índice secundario PATH podría acelerar la búsqueda. Como se indicó anteriormente en este tema, el índice principal resulta útil cuando se realizan consultas que especifican el método **exist()** en la cláusula WHERE. Si agrega un índice secundario PATH, también puede mejorar los resultados de búsqueda en dichas consultas.  
  
 Aunque un índice XML principal evita que el BLOB XML se tenga que dividir en tiempo de ejecución, es posible que no proporcione un rendimiento óptimo con consultas basadas en expresiones de ruta de acceso. Dado que todas las filas del índice XML principal correspondientes a un BLOB XML se examinan secuencialmente para instancias XML de gran tamaño, la búsqueda secuencial puede ser lenta. En este caso, incorporar un índice secundario a los valores de ruta de acceso y de nodo del índice principal puede aumentar significativamente la velocidad de búsqueda del índice. En el índice secundario PATH, los valores de ruta de acceso y de nodo son columnas de clave que permiten operaciones más eficaces durante la búsqueda de rutas. El optimizador de consultas puede utilizar el índice PATH para expresiones como las siguientes:  
  
-   `/root/Location` , que solo especifica una ruta de acceso.  
  
 O BIEN  
  
-   `/root/Location/@LocationID[.="10"]` , donde se especifican los valores de ruta de acceso y de nodo.  
  
 La consulta siguiente muestra en qué lugar es útil el índice PATH:  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS "PD")  
  
SELECT CatalogDescription.query('  
  /PD:ProductDescription/PD:Summary  
') AS Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist ('/PD:ProductDescription/@ProductModelID[.="19"]') = 1  
```  
  
 En la consulta, la expresión de ruta de acceso `/PD:ProductDescription/@ProductModelID` y el valor `"19"` del método `exist()` corresponden a los campos clave del índice PATH. Esto permite realizar búsquedas directas en el índice PATH y ofrece mejores resultados que la búsqueda secuencial de valores de ruta de acceso en el índice principal.  
  
### <a name="value-secondary-xml-index"></a>Índice XML secundario VALUE  
 Si las consultas se basan en valores, como, por ejemplo, `/Root/ProductDescription/@*[. = "Mountain Bike"]` o `//ProductDescription[@Name = "Mountain Bike"]`, y la ruta de acceso no se especifica completamente o incluye un carácter comodín, se pueden obtener resultados más rápidos creando un índice XML secundario que se agregue a los valores de nodo en el índice XML principal.  
  
 Las columnas de clave del índice VALUE (valor de nodo y ruta de acceso) pertenecen al índice XML principal. Si la carga de trabajo requiere consultar valores de instancias XML sin conocer los nombres de elemento o atributo que contienen los valores, un índice VALUE puede resultar útil. Por ejemplo, la siguiente expresión se beneficiará del índice VALUE:  
  
-   `//author[LastName="someName"]`, donde se conoce el valor del elemento <`LastName`>, pero el elemento primario <`author`> puede estar en cualquier lugar.  
  
-   `/book[@* = "someValue"]`, donde la consulta busca el elemento <`book`> que contiene algún atributo con el valor `"someValue"`.  
  
 La consulta siguiente devuelve `ContactID` de la tabla `Contact` . La cláusula `WHERE` especifica un filtro que busca valores en la columna `AdditionalContactInfo` de tipo **xml**. Los Id. de contacto se devuelven solo si el BLOB XML de información adicional de contacto correspondiente incluye un número de teléfono específico. Dado que el elemento <`telephoneNumber`> puede aparecer en cualquier lugar del XML, la expresión de ruta de acceso especifica el eje descendant-or-self.  
  
```  
WITH XMLNAMESPACES (  
  'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo' AS CI,  
  'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes' AS ACT)  
  
SELECT ContactID   
FROM   Person.Contact  
WHERE  AdditionalContactInfo.exist('//ACT:telephoneNumber/ACT:number[.="111-111-1111"]') = 1  
```  
  
 En esta situación, se conoce el valor de búsqueda para <`number`>, pero puede aparecer en cualquier lugar de la instancia XML como elemento secundario del elemento <`telephoneNumber`>. Este tipo de consulta puede beneficiarse de una búsqueda de índice basada en un valor específico.  
  
### <a name="property-secondary-index"></a>Índice secundario PROPERTY  
 Las consultas que recuperan uno o varios valores de instancias XML individuales pueden beneficiarse del índice PROPERTY. Este escenario se produce al recuperar propiedades del objeto usando el método **value()** del tipo **xml** y cuando se conoce el valor de clave principal del objeto.  
  
 El índice PROPERTY se agrega a columnas (PK, Path y valor de nodo) del índice XML principal, donde PK es la clave principal de la tabla base.  
  
 Por ejemplo, para el modelo de producto `19`, la consulta siguiente recupera los valores de los atributos `ProductModelID` y `ProductModelName` mediante el método `value()` . En lugar de utilizar el índice XML principal o los otros índices XML secundarios, el índice PROPERTY puede ofrecer una ejecución más rápida.  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS "PD")  
  
SELECT CatalogDescription.value('(/PD:ProductDescription/@ProductModelID)[1]', 'int') as ModelID,  
       CatalogDescription.value('(/PD:ProductDescription/@ProductModelName)[1]', 'varchar(30)') as ModelName          
FROM Production.ProductModel     
WHERE ProductModelID = 19  
```  
  
 Salvo por las diferencias descritas más adelante en este tema, crear un índice XML en una columna de tipo**xml** es similar a crear un índice en una columna que no sea de tipo**xml** . Las siguientes instrucciones DDL [!INCLUDE[tsql](../../includes/tsql-md.md)] pueden usarse para crear y administrar índices XML:  
  
-   [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  
  
-   [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)  
  
-   [DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)  
  
## <a name="getting-information-about-xml-indexes"></a>Obtener información acerca de los índices XML  
 Las entradas del índice XML aparecen en la vista de catálogo, sys.indexes, con el "tipo" de índice 3. La columna del nombre contiene el nombre del índice XML.  
  
 Los índices XML también se registran en la vista de catálogo sys.xml_indexes. Ésta contiene todas las columnas de sys.indexes y algunas específicas que son útiles para índices XML. El valor NULL de la columna secondary_type indica un índice XML principal; los valores "P", "R" y "V" representan los índices XML secundarios PATH, PROPERTY y VALUE, respectivamente.  
  
 Es posible encontrar el uso de espacio de los índices XML en la función con valores de tabla [sys.dm_db_index_physical_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md). Contiene información como el número de páginas de disco ocupadas, el tamaño medio de las filas en bytes y el número de registros de todos los tipos de índice. Se refiere también a los índices XML. Esta información está disponible para cada partición de base de datos. Los índices XML usan el mismo esquema de partición y la misma función de partición que la tabla base.  
  
## <a name="see-also"></a>Ver también  
 [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)   
 [Datos XML &#40;SQL Server&#41;](../../relational-databases/xml/xml-data-sql-server.md)  
  
  
