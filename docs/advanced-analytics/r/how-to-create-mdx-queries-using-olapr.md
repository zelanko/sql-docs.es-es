---
title: Cómo crear consultas MDX en R mediante olapr
description: Utilice la biblioteca de paquetes de olapr en SQL Server para escribir consultas MDX en el script de lenguaje R.
ms.prod: sql
ms.technology: machine-learning
ms.date: 05/22/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: fb2918e5fb89d85d7f6fa1cc12622481e585d848
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68887662"
---
# <a name="how-to-create-mdx-queries-in-r-using-olapr"></a>Cómo crear consultas MDX en R mediante olapr
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

El paquete [olapR](https://docs.microsoft.com/machine-learning-server/r-reference/olapr/olapr) admite consultas MDX en cubos alojados en SQL Server Analysis Services. Puede crear una consulta en un cubo existente, explorar dimensiones y otros objetos de cubo y pegar las consultas MDX existentes para recuperar los datos.

En este artículo se describen los dos usos principales del paquete olapr:

+ [Crear una consulta MDX desde R, con los constructores proporcionados en el paquete olapr](#buildMDX)
+ [Ejecutar una consulta MDX válida existente mediante olapr y un proveedor OLAP](#executeMDX)

No se admiten las siguientes operaciones:

+ Consultas DAX en un modelo tabular
+ Creación de nuevos objetos OLAP
+ Escritura diferida en particiones, incluidas medidas o sumas

## <a name="buildMDX"></a>Crear una consulta MDX desde R

1. Defina una cadena de conexión que especifique el origen de datos OLAP (instancia de SSAS) y el proveedor MSOLAP.

2. Use la función `OlapConnection(connectionString)` para crear un identificador para la consulta MDX y pasar la cadena de conexión.

3. Use el constructor `Query()` para crear instancias de un objeto de consulta.

4. Use las siguientes funciones del asistente para proporcionar más detalles sobre las dimensiones y las medidas que se deben incluir en la consulta MDX:

     + `cube()` : especifique el nombre de la base de datos SSAS. Si se conecta a una instancia con nombre, proporcione el nombre del equipo y el nombre de la instancia. 
     + `columns()`Proporcione los nombres de las medidas que se usarán en el argumento **on Columns** .
     + `rows()`Proporcione los nombres de las medidas que se usarán en el argumento **on Rows** .
     + `slicers()` : especifique un campo o los miembros que se usarán como segmentación. Una segmentación se parece a un filtro que se aplica a todos los datos de consulta MDX.
     
     + `axis()` : especifique el nombre de un eje adicional para usarlo en la consulta. 
     
         Un cubo OLAP puede contener hasta 128 ejes de consulta. Por lo general, los cuatro primeros ejes se conocen como **columnas**, **filas**, **páginas**y **capítulos**. 
         
         Si la consulta es relativamente sencilla, puede usar las funciones `columns`, `rows`, etc. para crear la consulta. También puede usar la función `axis()` con un valor de índice distinto de cero para crear una consulta MDX con varios calificadores o para agregar dimensiones adicionales como calificadores.

5. Pase el identificador y la consulta MDX completada a una de las siguientes funciones, dependiendo de la forma de los resultados: 

  + `executeMD` : devuelve una matriz multidimensional
  + `execute2D` : devuelve una trama de datos bidimensional (tabular)

## <a name="executeMDX"></a>Ejecutar una consulta MDX válida desde R

1. Defina una cadena de conexión que especifique el origen de datos OLAP (instancia de SSAS) y el proveedor MSOLAP.

2. Use la función `OlapConnection(connectionString)` para crear un identificador para la consulta MDX y pasar la cadena de conexión.

3. Defina una variable de R para almacenar el texto de la consulta MDX.

4. Pase el identificador y la variable que contiene la consulta MDX en las funciones `executeMD` o `execute2D`, en función de la forma de los resultados.

    + `executeMD` : devuelve una matriz multidimensional
    + `execute2D` : devuelve una trama de datos bidimensional (tabular)

## <a name="examples"></a>Ejemplos

Los ejemplos siguientes se basan en la data mart de AdventureWorks y el proyecto de cubo, porque ese proyecto está ampliamente disponible, en varias versiones, incluidos los archivos de copia de seguridad que se pueden restaurar fácilmente a Analysis Services. Si no tiene un cubo existente, obtenga un cubo de ejemplo con cualquiera de estas opciones:

+ Cree el cubo que se usa en estos ejemplos siguiendo el Analysis Services tutorial hasta la lección 4: [Crear un cubo OLAP](https://docs.microsoft.com/analysis-services/multidimensional-tutorial/multidimensional-modeling-adventure-works-tutorial)

+ Descargue un cubo existente como copia de seguridad y restáurelo en una instancia de Analysis Services. Por ejemplo, este sitio proporciona un cubo totalmente procesado en formato comprimido: [Modelo multidimensional de Adventure Works SQL 2014](https://msftdbprodsamples.codeplex.com/downloads/get/882334). Extraiga el archivo y, a continuación, restáurelo en la instancia de SSAS. Para obtener más información, vea [Backup and restore](https://docs.microsoft.com/analysis-services/multidimensional-models/backup-and-restore-of-analysis-services-databases)o [restore-asdatabase cmdlet](https://docs.microsoft.com/analysis-services/powershell/restore-asdatabase-cmdlet).

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
+ Esta consulta devolvería una tabla con tres columnas, que contiene un resumen de las ventas por Internet de todos los países.
+ La cláusula WHERE especifica el _eje segmentador_. En este ejemplo, la segmentación usa un miembro de la dimensión **SalesTerritory** para filtrar la consulta de modo que solo se usen las ventas de Australia en los cálculos.

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

En el caso de una instancia con nombre, asegúrese de usar el carácter de escape para los caracteres que se puedan considerar caracteres de control en R.  Por ejemplo, la siguiente cadena de conexión hace referencia a una instancia de OLAP01, en un servidor denominado ContosoHQ:

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

Si define una consulta mediante el Generador MDX en SQL Server Management Studio y, a continuación, guarda la cadena MDX, se numerarán los ejes a partir de 0, como se muestra a continuación: 

```MDX
SELECT {[Measures].[Internet Sales Count], [Measures].[Internet Sales-Sales Amount]} ON AXIS(0), 
   {[Product].[Product Line].[Product Line].MEMBERS} ON AXIS(1) 
   FROM [Analysis Services Tutorial] 
   WHERE [Sales Territory].[Sales Territory Countr,y].[Australia]
```

Aun así, puede ejecutar esta consulta como una cadena MDX predefinida, Sin embargo, para crear la misma consulta mediante R con `axis()` la función, debe renumerar los ejes a partir de 1.

### <a name="2-explore-cubes-and-their-fields-on-an-ssas-instance"></a>2. Explorar los cubos y sus campos en una instancia SSAS

Puede usar la función `explore` para devolver una lista de cubos, dimensiones o miembros que se usarán en la construcción de la consulta. Esto resulta práctico si no tiene acceso a otras herramientas de exploración de OLAP o si quiere manipular o construir la consulta MDX mediante programación.

#### <a name="to-list-the-cubes-available-on-the-specified-connection"></a>Para consultar la lista de cubos disponibles en la conexión especificada

Para ver todos los cubos o perspectivas en la instancia en la que tiene permiso de visualización, proporcione el identificador como argumento de `explore`.

> [!IMPORTANT]
> El resultado final **no** es un cubo; TRUE simplemente indica que la operación de metadatos se ha realizado correctamente. Si los argumentos no son válidos, se produce un error.

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

Después de definir el origen y de crear el identificador, especifique el cubo, la dimensión y la jerarquía que va a devolver. En los resultados devueltos, los elementos que tienen **->** el prefijo representan elementos secundarios del miembro anterior.

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

[Usar datos de cubos OLAP en R](../../advanced-analytics/r/using-data-from-olap-cubes-in-r.md)
