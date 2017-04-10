---
title: "C&#243;mo crear consultas MDX con olapR | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "R"
ms.assetid: c12b988e-be7e-41ba-a84c-299a5c45d4ab
caps.latest.revision: 3
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 3
---
# C&#243;mo crear consultas MDX con olapR
## <a name="how-to-build-an-mdx-query-from-r"></a>Cómo crear una consulta MDX desde R

1. Defina una cadena de conexión que especifique el origen de datos OLAP (instancia de SSAS) y el proveedor MSOLAP.

2. Use la función `OlapConnection(connectionString)` para crear un identificador para la consulta MDX y pasar la cadena de conexión.

3. Use el constructor `Query()` para crear instancias de un objeto de consulta.

4. Use las siguientes funciones auxiliares para proporcionar más detalles sobre las dimensiones y las medidas que se deben incluir en la consulta MDX:
     + `cube()`: especifique el nombre de la base de datos SSAS.
     + `columns()`: proporcione los nombres de las medidas que se usarán en el argumento ON COLUMNS.  
     + `rows()`: proporcione los nombres de las medidas que se usarán en el argumento ON ROWS.
     + `slicers()`: especifique un campo o los miembros que se usarán como segmentación. Una segmentación se parece a un filtro que se aplica a todos los datos de consulta MDX.
     
     + `axis()`: especifique el nombre de un eje adicional para usarlo en la consulta. Un cubo OLAP puede contener hasta 128 ejes de consulta. Por lo general, los primeros cuatro ejes se denominan Columnas, Filas, Páginas y Capítulos. Si la consulta es relativamente sencilla, puede usar las funciones `columns`, `rows`, etc. para crear la consulta.     
     También puede usar la función `axis()` con un valor de índice distinto de cero para crear una consulta MDX con varios calificadores o para agregar dimensiones adicionales como calificadores.

5. Pase el identificador y la consulta MDX completada en las funciones `executeMD` o `execute2D`, en función de la forma de los resultados.

  + `executeMD`: devuelve una matriz multidimensional
  + `execute2D`: devuelve una trama de datos bidimensional (tabular)


## <a name="how-to-run-an-existing-mdx-query-from-r"></a>Cómo ejecutar una consulta MDX existente desde R

1. Defina una cadena de conexión que especifique el origen de datos OLAP (instancia de SSAS) y el proveedor MSOLAP.

2. Use la función `OlapConnection(connectionString)` para crear un identificador para la consulta MDX y pasar la cadena de conexión.

3. Defina una variable de R para almacenar el texto de la consulta MDX.

4. Pase el identificador y la variable que contiene la consulta MDX en las funciones `executeMD` o `execute2D`, en función de la forma de los resultados.

    + `executeMD`: devuelve una matriz multidimensional
    + `execute2D`: devuelve una trama de datos bidimensional (tabular)



## <a name="examples"></a>Ejemplos

### <a name="1-basic-mdx-with-slicer"></a>1. MDX básico con segmentación

Esta consulta MDX selecciona _measures_ (medidas) de count (recuento) y amount (cantidad) del recuento de ventas por Internet y el importe de las ventas, y los coloca en el eje Columna. Agrega un miembro de la dimensión Sales Territory (Territorio de ventas) como *segmentación* para filtrar la consulta de manera que en los cálculos solo se usen las ventas de Australia.

```MDX
SELECT {[Measures].[Internet Sales Count], [Measures].[InternetSales-Sales Amount]} ON COLUMNS, 
{[Product].[Product Line].[Product Line].MEMBERS} ON ROWS 
FROM [Analysis Services Tutorial] 
WHERE [Sales Territory].[Sales Territory Country].[Australia]
```

+ En las columnas puede especificar varias medidas como elementos de una cadena separada por comas.
+ El eje Fila usa todos los valores posibles (todos los MIEMBROS) de la dimensión "Product Line" (Línea de productos). 
+ Esta consulta devolvería una tabla con tres columnas, que contendría un _resumen_ de las ventas por Internet de todos los países. 
+ La cláusula WHERE es el _eje segmentador_. Usa un miembro de la dimensión Sales Territory para filtrar la consulta de manera que en los cálculos solo se usen las ventas de Australia.

#### <a name="to-build-this-query-using-the-functions-provided-in-olapr"></a>Para crear esta consulta con las funciones proporcionadas en olapR

```R
cnnstr <- "Data Source=localhost; Provider=MSOLAP;"
ocs <- OlapConnection(cnnstr)

qry <- Query()
cube(qry) <- "[Analysis Services Tutorial]"
columns(qry) <- c("[Measures].[Internet Sales Count]", "[Measures].[Internet Sales-Sales Amount]")
rows(qry) <- c("[Product].[Product Line].[Product Line].MEMBERS") 
slicers(qry) <- c("[Sales Territory].[Sales Territory Country].[Australia]")

result1 <- executeMD(ocs, qry)

```

#### <a name="to-run-this-query-as-a-predefined-mdx-string"></a>Para ejecutar esta consulta como una cadena MDX predefinida

```R
cnnstr <- "Data Source=localhost; Provider=MSOLAP;"
ocs <- OlapConnection(cnnstr)

mdx <- "SELECT {[Measures].[Internet Sales Count], [Measures].[InternetSales-Sales Amount]} ON COLUMNS, {[Product].[Product Line].[Product Line].MEMBERS} ON ROWS FROM [Analysis Services Tutorial] WHERE [Sales Territory].[Sales Territory Country].[Australia]"

result2 <- execute2D(ocs, mdx)
```

Tenga en cuenta que, si define una consulta con el Generador MDX en SQL Server Management Studio y después guarda la cadena de MDX, numerará los ejes a partir del 0, como se muestra a continuación: 

~~~~
SELECT {[Measures].[Internet Sales Count], [Measures].[Internet Sales-Sales Amount]} ON AXIS(0), 
   {[Product].[Product Line].[Product Line].MEMBERS} ON AXIS(1) 
   FROM [Analysis Services Tutorial] 
   WHERE [Sales Territory].[Sales Territory Country].[Australia]
~~~~

Aun así, puede ejecutar esta consulta como una cadena MDX predefinida, aunque para crear la misma consulta en R usando la función `axis()`, debe asegurarse de numerar los ejes a partir del 1.


### <a name="2-explore-cubes-and-their-fields-on-an-ssas-instance"></a>2. Explorar los cubos y sus campos en una instancia SSAS

Puede usar la función `explore` para devolver una lista de cubos, dimensiones o miembros que se usarán en la construcción de la consulta. Esto resulta práctico si no tiene acceso a otras herramientas de exploración de OLAP o si quiere manipular o construir la consulta MDX mediante programación.

#### <a name="to-list-the-cubes-available-on-the-specified-connection"></a>Para consultar la lista de cubos disponibles en la conexión especificada

Para ver todos los cubos o perspectivas en la instancia en la que tiene permiso de visualización, proporcione el identificador como argumento de `explore`.
Tenga en cuenta que el resultado final no es un cubo: TRUE solo indica que la operación de metadatos se ha efectuado correctamente. Si los argumentos no son válidos, se produce un error.

```R
cnnstr <- "Data Source=localhost; Provider=MSOLAP;"
ocs <- OlapConnection(cnnstr)
explore(ocs)
```

| Resultado  |  
| ----|
| _Analysis Services Tutorial_|
|_Internet Sales_|
|_Reseller Sales_|
|_Sales Summary_|
|_[1] TRUE_|
     


#### <a name="to-get-a-list-of-cube-dimensions"></a>Para obtener una lista de dimensiones de cubo

Para ver todas las dimensiones del cubo o de la perspectiva, especifique el nombre del cubo o de la perspectiva.

```R
cnnstr <- "Data Source=localhost; Provider=MSOLAP;"
ocs <- OlapConnection(cnnstr)
explore(ocs, "Sales")
```

| Resultado  |  
| ----|
| _Customer_|
|_Date_|
|_Region_|


#### <a name="to-return-all-members-of-the-specified-dimension-and-hierarchy"></a>Para devolver todos los miembros de la jerarquía y la dimensión especificadas

Después de definir el origen y de crear el identificador, especifique el cubo, la dimensión y la jerarquía que va a devolver.
Tenga en cuenta que los elementos de los resultados devueltos que tienen el prefijo **->** representan los elementos secundarios del miembro anterior.

```R
cnnstr <- "Data Source=localhost; Provider=MSOLAP;"
ocs <- OlapConnection(cnnstr)
explore(ocs, "Analysis Services Tutorial", "Product", "Product Categories", "Category")
```

| Resultado  |  
| ----|
| _Accessories_|
|_Bikes_|
|_Clothing_|
|_Components_|
|-> Assembly Components|
|-> Assembly Components|



## <a name="see-also"></a>Vea también

[Using Data from OLAP Cubes in R](../../advanced-analytics/r-services/using-data-from-olap-cubes-in-r.md) (Usar datos de cubos OLAP en R)