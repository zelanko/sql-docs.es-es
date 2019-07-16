---
title: Cómo crear consultas MDX en R con olapR - SQL Server Machine Learning Services
description: Usar la biblioteca de paquetes olapR en SQL Server para escribir consultas MDX en el script del lenguaje R.
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/22/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 66604e44d714837ec9b974af5d0a29b56396cb45
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962647"
---
# <a name="how-to-create-mdx-queries-in-r-using-olapr"></a>Cómo crear consultas MDX en R con olapR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

El [olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) paquete admite consultas MDX en cubos hospedadas en SQL Server Analysis Services. Puede crear una consulta en un cubo existente, explorar las dimensiones y otros objetos de cubo y pegar en las consultas MDX existentes para recuperar los datos.

En este artículo se describe los dos usos principales de la **olapR** paquete:

+ [Crear una consulta MDX desde R, mediante los constructores proporcionadas en el paquete olapR](#buildMDX)
+ [Ejecutar una consulta MDX válida, existente mediante un proveedor OLAP y olapR](#executeMDX)

No se admiten las siguientes operaciones:

+ Consultas DAX en un modelo tabular
+ Creación de nuevos objetos OLAP
+ Escritura diferida de las particiones, incluidas las medidas o sumas

## <a name="buildMDX"></a> Crear una consulta MDX desde R

1. Defina una cadena de conexión que especifique el origen de datos OLAP (instancia de SSAS) y el proveedor MSOLAP.

2. Use la función `OlapConnection(connectionString)` para crear un identificador para la consulta MDX y pasar la cadena de conexión.

3. Use el constructor `Query()` para crear instancias de un objeto de consulta.

4. Use las siguientes funciones del asistente para proporcionar más detalles sobre las dimensiones y las medidas que se deben incluir en la consulta MDX:

     + `cube()` : especifique el nombre de la base de datos SSAS. Si se conecta a una instancia con nombre, proporcione el nombre del equipo y el nombre de instancia. 
     + `columns()` Proporcione los nombres de las medidas que se usarán en el **ON COLUMNS** argumento.
     + `rows()` Proporcione los nombres de las medidas que se usarán en el **ON ROWS** argumento.
     + `slicers()` : especifique un campo o los miembros que se usarán como segmentación. Una segmentación se parece a un filtro que se aplica a todos los datos de consulta MDX.
     
     + `axis()` : especifique el nombre de un eje adicional para usarlo en la consulta. 
     
         Un cubo OLAP puede contener hasta 128 ejes de consulta. Por lo general, los primeros cuatro ejes se denominan **columnas**, **filas**, **páginas**, y **capítulos**. 
         
         Si la consulta es relativamente sencilla, puede usar las funciones `columns`, `rows`, etc. para crear la consulta. También puede usar la función `axis()` con un valor de índice distinto de cero para crear una consulta MDX con varios calificadores o para agregar dimensiones adicionales como calificadores.

5. Pase el identificador y la consulta MDX completada, en una de las funciones siguientes, dependiendo de la forma de los resultados: 

  + `executeMD` : devuelve una matriz multidimensional
  + `execute2D` : devuelve una trama de datos bidimensional (tabular)

## <a name="executeMDX"></a> Ejecutar una consulta MDX válida desde R

1. Defina una cadena de conexión que especifique el origen de datos OLAP (instancia de SSAS) y el proveedor MSOLAP.

2. Use la función `OlapConnection(connectionString)` para crear un identificador para la consulta MDX y pasar la cadena de conexión.

3. Defina una variable de R para almacenar el texto de la consulta MDX.

4. Pase el identificador y la variable que contiene la consulta MDX en las funciones `executeMD` o `execute2D`, en función de la forma de los resultados.

    + `executeMD` : devuelve una matriz multidimensional
    + `execute2D` : devuelve una trama de datos bidimensional (tabular)

## <a name="examples"></a>Ejemplos

Los ejemplos siguientes se basan en el proyecto de mart y cubos de datos de AdventureWorks, porque ese proyecto está ampliamente disponible, en varias versiones, incluidos los archivos de copia de seguridad que se pueden restaurar fácilmente a Analysis Services. Si no tiene un cubo existente, obtenga un cubo de ejemplo mediante cualquiera de estas opciones:

+ Crear el cubo que se usa en estos ejemplos, siga el tutorial de Analysis Services hasta lección 4: [Crear un cubo OLAP](../../analysis-services/multidimensional-tutorial/multidimensional-modeling-adventure-works-tutorial.md)

+ Descargar un cubo existente como una copia de seguridad y restaurarla en una instancia de Analysis Services. Por ejemplo, este sitio proporciona un cubo totalmente procesado en formato comprimido: [De Adventure Works Multidimensional Model SQL 2014](https://msftdbprodsamples.codeplex.com/downloads/get/882334). Extraiga el archivo y, a continuación, restaurarla a su instancia de SSAS. Para obtener más información, consulte [copias de seguridad y restauración](../../analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases.md), o [Cmdlet Restore-ASDatabase](../../analysis-services/powershell/restore-asdatabase-cmdlet.md).

### <a name="1-basic-mdx-with-slicer"></a>1. MDX básico con segmentación

Esta consulta MDX selecciona _measures_ (medidas) de count (recuento) y amount (cantidad) del recuento de ventas por Internet y el importe de las ventas, y los coloca en el eje Columna. Agrega un miembro de la dimensión Sales Territory (Territorio de ventas) como *segmentación*para filtrar la consulta de manera que en los cálculos solo se usen las ventas de Australia.

```MDX
SELECT {[Measures].[Internet Sales Count], [Measures].[InternetSales-Sales Amount]} ON COLUMNS, 
{[Product].[Product Line].[Product Line].MEMBERS} ON ROWS 
FROM [Analysis Services Tutorial] 
WHERE [Sales Territory].[Sales Territory Country].[Australia]
```

+ En las columnas puede especificar varias medidas como elementos de una cadena separada por comas.
+ El eje Fila usa todos los valores posibles (todos los MIEMBROS) de la dimensión "Product Line" (Línea de productos). 
+ Esta consulta devolvería una tabla con tres columnas, que contiene un _acumulación_ resumen de ventas por Internet de todos los países.
+ La cláusula WHERE especifica la _eje segmentador_. En este ejemplo, la segmentación de datos usa un miembro de la **SalesTerritory** dimensiones para filtrar la consulta para que se usan sólo las ventas de Australia en los cálculos.

#### <a name="to-build-this-query-using-the-functions-provided-in-olapr"></a>Para crear esta consulta con las funciones proporcionadas en olapR

```R
cnnstr <- "Data Source=localhost; Provider=MSOLAP; initial catalog=Analysis Services Tutorial"
ocs <- OlapConnection(cnnstr)

qry <- Query()
cube(qry) <- "[Analysis Services Tutorial]"
columns(qry) <- c("[Measures].[Internet Sales Count]", "[Measures].[Internet Sales-Sales Amount]")
rows(qry) <- c("[Product].[Product Line].[Product Line].MEMBERS") 
slicers(qry) <- c("[Sales Territory].[Sales Territory Country].[Australia]")

result1 <- executeMD(ocs, qry)

```

Para una instancia con nombre, asegúrese de escape de caracteres que podrían considerarse como caracteres de control en R.  Por ejemplo, la cadena de conexión siguiente hace referencia a una instancia OLAP01, en un servidor denominado ContosoHQ:

```R
cnnstr <- "Data Source=ContosoHQ\\OLAP01; Provider=MSOLAP; initial catalog=Analysis Services Tutorial"
```

#### <a name="to-run-this-query-as-a-predefined-mdx-string"></a>Para ejecutar esta consulta como una cadena MDX predefinida

```R
cnnstr <- "Data Source=localhost; Provider=MSOLAP; initial catalog=Analysis Services Tutorial"
ocs <- OlapConnection(cnnstr)

mdx <- "SELECT {[Measures].[Internet Sales Count], [Measures].[InternetSales-Sales Amount]} ON COLUMNS, {[Product].[Product Line].[Product Line].MEMBERS} ON ROWS FROM [Analysis Services Tutorial] WHERE [Sales Territory].[Sales Territory Country].[Australia]"

result2 <- execute2D(ocs, mdx)
```

Si se define una consulta mediante el Generador MDX en SQL Server Management Studio y, a continuación, guarde la cadena de MDX, numerará los ejes a partir de 0, como se muestra aquí: 

```MDX
SELECT {[Measures].[Internet Sales Count], [Measures].[Internet Sales-Sales Amount]} ON AXIS(0), 
   {[Product].[Product Line].[Product Line].MEMBERS} ON AXIS(1) 
   FROM [Analysis Services Tutorial] 
   WHERE [Sales Territory].[Sales Territory Countr,y].[Australia]
```

Aun así, puede ejecutar esta consulta como una cadena MDX predefinida, Sin embargo, para crear la misma consulta R usando el `axis()` función, deben volver a numerar los ejes que empieza por 1.

### <a name="2-explore-cubes-and-their-fields-on-an-ssas-instance"></a>2. Explorar los cubos y sus campos en una instancia SSAS

Puede usar la función `explore` para devolver una lista de cubos, dimensiones o miembros que se usarán en la construcción de la consulta. Esto resulta práctico si no tiene acceso a otras herramientas de exploración de OLAP o si quiere manipular o construir la consulta MDX mediante programación.

#### <a name="to-list-the-cubes-available-on-the-specified-connection"></a>Para consultar la lista de cubos disponibles en la conexión especificada

Para ver todos los cubos o perspectivas en la instancia en la que tiene permiso de visualización, proporcione el identificador como argumento de `explore`.

> [!IMPORTANT]
> El resultado final es **no** un cubo. TRUE indica simplemente que la operación de metadatos se realizó correctamente. Si los argumentos no son válidos, se produce un error.

```R
cnnstr <- "Data Source=localhost; Provider=MSOLAP; initial catalog=Analysis Services Tutorial"
ocs <- OlapConnection(cnnstr)
explore(ocs)
```

| Resultados  |
| ----|
| _Analysis Services Tutorial_|
|_Internet Sales_|
|_Reseller Sales_|
|_Sales Summary_|
|_[1] TRUE_|

#### <a name="to-get-a-list-of-cube-dimensions"></a>Para obtener una lista de dimensiones de cubo

Para ver todas las dimensiones del cubo o de la perspectiva, especifique el nombre del cubo o de la perspectiva.

```R
cnnstr <- "Data Source=localhost; Provider=MSOLAP; initial catalog=Analysis Services Tutorial"
ocs \<- OlapConnection(cnnstr)
explore(ocs, "Sales")
```

| Resultados  |
| ----|
| _Customer_|
|_Date_|
|_Region_|


#### <a name="to-return-all-members-of-the-specified-dimension-and-hierarchy"></a>Para devolver todos los miembros de la jerarquía y la dimensión especificadas

Después de definir el origen y de crear el identificador, especifique el cubo, la dimensión y la jerarquía que va a devolver. En los resultados devueltos, los elementos que tienen el prefijo **->** representan los elementos secundarios del miembro anterior.

```R
cnnstr <- "Data Source=localhost; Provider=MSOLAP; initial catalog=Analysis Services Tutorial"
ocs <- OlapConnection(cnnstr)
explore(ocs, "Analysis Services Tutorial", "Product", "Product Categories", "Category")
```

| Resultados  |
| ----|
| _Accessories_|
|_Bikes_|
|_Clothing_|
|_Components_|
|-> Assembly Components|
|-> Assembly Components|


## <a name="see-also"></a>Vea también

[Uso de datos de cubos OLAP en R](../../advanced-analytics/r/using-data-from-olap-cubes-in-r.md)
