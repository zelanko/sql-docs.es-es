---
title: Conjunto de filas DISCOVER_CALC_DEPENDENCY | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- DISCOVER_CALC_DEPENDENCIES rowset
ms.assetid: f39dde72-fa5c-4c82-8b4e-88358aa2e422
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: fff5a7975d19ca53ea9cca780f792a2d5c6057e4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36109108"
---
# <a name="discovercalcdependency-rowset"></a>DISCOVER_CALC_DEPENDENCY, conjunto de filas
  Informa sobre las dependencias entre los cálculos y sobre los objetos a los que se hace referencia en dichos cálculos. Puede utilizar esta información en una aplicación cliente para informar sobre los problemas con fórmulas complejas o para avisar cuándo se eliminan o modifican objetos relacionados. También puede utilizar el conjunto de filas para extraer las expresiones de DAX que se utilizan en medidas o columnas calculadas.  
  
 **Se aplica a:** modelos tabulares  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 El `DISCOVER_CALC_DEPENDENCY` filas contiene las columnas siguientes. La tabla también especifica el tipo de datos, indica si la columna se puede restringir para limitar las filas que se devuelven y proporciona una descripción de cada columna.  
  
|Nombre de columna|Indicador de tipo|Restricción|Descripción|  
|-----------------|--------------------|-----------------|-----------------|  
|`DATABASE_NAME`|`DBTYPE_WSTR`|Sí|Especifica el nombre de la base de datos que contiene el objeto cuyo análisis de dependencia se solicita. Si se omite, se utiliza la base de datos actual.<br /><br /> El `DISCOVER_DEPENDENCY_CALC` conjunto de filas puede restringirse mediante esta columna.|  
|`OBJECT_TYPE`|`DBTYPE_WSTR`|Sí|Indica el tipo de objeto cuyo análisis de dependencia se solicita. El objeto debe ser de uno de los tipos siguientes:<br /><br /> -   `ACTIVE_RELATIONSHIP`: una relación activa<br />-   `CALC_COLUMN`: Columna calculada<br />-   `HIERARCHY`: una jerarquía<br />-   `MEASURE`: una medida<br />-   `RELATIONSHIP`: una relación<br />-   `KPI`: un KPI (indicador clave de rendimiento)<br /><br /> El `DISCOVER_DEPENDENCY_CALC` conjunto de filas puede restringirse mediante esta columna.|  
|`QUERY`|`DBTYPE_WSTR`|Sí|En los modelos tabulares creados en [!INCLUDE[ssSQL11SP1](../../../includes/sssql11sp1-md.md)], puede incluir una expresión o consulta DAX para mostrar el gráfico de dependencias de esa consulta o expresión. La restricción QUERY proporciona a las aplicaciones cliente un modo de determinar qué objetos usa una consulta DAX.<br /><br /> La restricción `QUERY` puede especificarse en una cláusula XMLA o WHERE de una consulta DMV. Vea la sección de ejemplos para obtener más información.|  
|`TABLE`|`DBTYPE_WSTR`||El nombre de la tabla que contiene el objeto para el que se genera la información de dependencia.|  
|`OBJECT`|`DBTYPE_WSTR`||El nombre del objeto para el que se genera la información de dependencias. Si el objeto es una medida o una columna calculada, utilice el nombre de la medida. Si el objeto es una relación, el nombre de la tabla (o la dimensión de cubo) que contiene la columna que participa en la relación.|  
|`EXPRESSION`|`DBTYPE_WSTR`||La fórmula que contiene el objeto cuyas dependencias se buscan.|  
|`REFERENCED_OBJECT_TYPE`|`DBTYPE_WSTR`||Devuelve el tipo de objeto que tiene una dependencia en el objeto al que se hace referencia. Los objetos devueltos pueden ser de alguno de los tipos siguientes:<br /><br /> -   `CALC_COLUMN`: una columna calculada<br />-   `COLUMN`: Una columna de datos<br />-   `MEASURE`: una medida<br />-   `RELATIONSHIP`: una relación<br />-   `KPI`: un KPI (indicador clave de rendimiento)|  
|`REFERENCED_TABLE`|`DBTYPE_ WSTR`||El nombre de la tabla que contiene el objeto dependiente.|  
|`REFERENCED_OBJECT`|`DBTYPE_ WSTR`||El nombre del objeto que tiene una dependencia en el objeto al que se hace referencia. Para las medidas y columnas calculadas, el nombre de la medida o la columna. Para las relaciones, el nombre completo de la tabla (o dimensión de cubo) que contiene el objeto dependiente.|  
|`REFERENCED_EXPRESSION`|`DBTYPE_WSTR`||Una fórmula, en una columna calculada o en una medida, que depende del objeto al que se hace referencia.|  
  
## <a name="example"></a>Ejemplo  
 **Sintaxis básica**  
  
 La consulta siguiente es una consulta DMV simple que devuelve valores para todas las columnas de este conjunto de filas, utilizando la base de datos predeterminada en la conexión actual. Puede ejecutar esta consulta en una ventana de consulta MDX y ver los resultados en [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]. También puede seguir las técnicas descritas en [Querying PowerPivot DMVs from Excel](http://go.microsoft.com/fwlink/?LinkID=235146) para ver los resultados de la consulta DMV en Excel.  
  
```  
SELECT * FROM $System.DISCOVER_CALC_DEPENDENCY  
```  
  
## <a name="example"></a>Ejemplo  
 **Ordenar los resultados**  
  
 Agregue una cláusula ORDER BY para ordenar el conjunto de filas por la tabla o por otra columna.  
  
```  
SELECT * FROM $System.DISCOVER_CALC_DEPENDENCY ORDER BY [TABLE] ASC  
```  
  
## <a name="example"></a>Ejemplo  
 **Filtrar con una cláusula WHERE**  
  
 En la consulta siguiente se muestra cómo agregar una restricción utilizando una cláusula WHERE. Las columnas siguientes se pueden usar como filtros de consulta en una cláusula WHERE: `Database_Name`, `Object_Type`, y `Query`.  
  
```  
SELECT * From $SYSTEM.DISCOVER_CALC_DEPENDENCY WHERE OBJECT_TYPE = 'RELATIONSHIP' OR OBJECT_TYPE = 'ACTIVE_RELATIONSHIP'  
```  
  
## <a name="example"></a>Ejemplo  
 **Filtrar según las medidas y columnas calculadas para ver las expresiones DAX subyacentes**  
  
 En esta consulta, puede seleccionar solo la medida o la columna calculada y después ver la expresión DAX que se usa en el cálculo. La columna EXPRESSION contiene las expresiones DAX. Si utiliza DISCOVER_CALC_DEPENDENCY para extraer la expresión de DAX usada en el modelo, esta consulta es suficiente para ese fin. Devuelve todas las expresiones usadas en el modelo, en orden ascendente.  
  
```  
SELECT * From $SYSTEM.DISCOVER_CALC_DEPENDENCY WHERE OBJECT_TYPE = 'MEASURE' OR OBJECT_TYPE = 'CALC_COLUMN' ORDER BY [EXPRESSION] ASC  
```  
  
## <a name="example"></a>Ejemplo  
 **Filtrar con QUERY**  
  
 Usando la restricción QUERY, puede proporcionar una consulta DAX para ver todos los objetos usados en esa consulta. Considere una consulta sencilla como ‘Evaluate Customer’. Según se ha escrito, esta consulta devuelve las filas de los datos de los clientes, en las que la composición de las filas se base en la columna en la tabla Customer. Si ahora ejecuta DISCOVER_CALC_DEPENDENCY con una restricción QUERY de ‘Evaluate Customer’, obtendrá las columnas (u objetos) que se usan en esa consulta. En este caso, es una lista de las columnas en la tabla Customer.  
  
 El siguiente conjunto de consultas demuestra la sintaxis de la restricción QUERY. Puede ejecutar estas consultas con el [Modelo tabular AdventureWorks SQL Server 2012](http://msftdbprodsamples.codeplex.com/releases/view/55330) para ver el conjunto de resultados.  
  
 La primera consulta muestra cómo especificar una restricción QUERY para los nombres de objeto que incluyen espacios. La segunda consulta, tomada prestada de [Ejecutar consultas DAX a través de OLE DB y ADOMD.NET](http://go.microsoft.com/fwlink/?LinkId=254329), es una consulta más compleja que incluye objetos de varias tablas.  
  
> [!NOTE]  
>  Aunque las consultas parecen usar dobles comillas, de hecho solo se usan comillas simples. Un par de comillas simples encierra ' Evaluate \<Tablename >', y las comillas sencillas usadas alrededor del nombre de tabla tienen que evitarse duplicándolas. Las comillas sencillas alrededor de un nombre de tabla solo son necesarias para los nombres de tabla que incluyen un espacio.  
  
```  
SELECT * From $SYSTEM.DISCOVER_CALC_DEPENDENCY WHERE QUERY = 'EVALUATE ''Reseller Sales'''  
```  
  
```  
SELECT * from $system.DISCOVER_CALC_DEPENDENCY WHERE QUERY = 'EVALUATE CALCULATETABLE(VALUES(''Product Subcategory''[Product Subcategory Name]), ''Product Category''[Product Category Name] = "Bikes")'  
```  
  
## <a name="example"></a>Ejemplo  
 **Ejemplo XMLA de restricción de consulta**  
  
 Puede usar un comando XMLA Discover para devolver los objetos de consulta en una tabla. XMLA devuelve los resultados como XML sin formato. Puede usar ADOMD.NET para analizar los resultados en un formato más legible.  
  
```  
<Discover xmlns="urn:schemas-microsoft-com:xml-analysis">  
   <RequestType>DISCOVER_CALC_DEPENDENCY</RequestType>  
     <Restrictions>  
        <RestrictionList>  
            <QUERY>Evaluate 'Reseller Sales'</QUERY>  
        </RestrictionList>  
    </Restrictions>  
    <Properties />  
</Discover>  
```  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>Usar ADOMD.NET para devolver el conjunto de filas  
 Cuando se utilizan ADOMD.NET y el conjunto de filas de esquema para recuperar metadatos, puede utilizar el GUID o una cadena para hacer referencia a un objeto de conjunto de filas de esquema del método GetSchemaDataSet. Para obtener más información, vea [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md).  
  
 La tabla siguiente proporciona el GUID y los valores de cadena que identifican este conjunto de filas.  
  
|Argumento|Valor|  
|--------------|-----------|  
|GUID|a07ccd46-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|DependencyGraph|  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de Analysis Services](../analysis-services-schema-rowsets.md)   
 [Usar vistas de administración dinámica &#40;DMV&#41; supervisar Analysis Services](../../instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)  
  
  