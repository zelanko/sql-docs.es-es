---
title: StructureColumn (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 7b6b436527aa36fb8f048a3b3c8fc55b970ef284
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68065396"
---
# <a name="structurecolumn-dmx"></a>StructureColumn (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Devuelve el valor de la columna de estructura que corresponde al caso especificado o el valor de tabla para una tabla anidada en el caso especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
StructureColumn('structure column name')  
```  
  
## <a name="arguments"></a>Argumentos  
 structure-column-name.  
 Nombre de una columna de estructura de minería de datos de tabla anidada o caso.  
  
## <a name="result-type"></a>Tipo de resultado  
 El tipo que se devuelve depende del tipo de la columna a la que se hace referencia en \<el nombre de la columna de estructura> parámetro. Por ejemplo, si la columna de estructura de minería de datos a la que se hace referencia contiene un valor escalar, la función devuelve un valor escalar.  
  
 Si es una tabla anidada, la función devuelve un valor de tabla. El valor de tabla devuelto se puede utilizar en la cláusula FROM de una instrucción sub-SELECT.  
  
## <a name="remarks"></a>Observaciones  
 Esta función es polimórfica y se puede utilizar en cualquier parte de una instrucción que permita expresiones, por ejemplo en una lista de expresiones SELECT, una expresión de condición WHERE y una expresión ORDER BY.  
  
 El nombre de la columna de la estructura de minería de datos es un valor de cadena y, como tal, se debe incluir entre comillas simples: por ejemplo, `StructureColumn('` **columna 1**`')`. Si hay varias columnas que tienen el mismo nombre, el nombre se resuelve en el contexto de la instrucción SELECT contenedora.  
  
 Los resultados que se devuelven desde una consulta mediante la función **StructureColumn** se ven afectados por la presencia de filtros en el modelo. Es decir, el filtro del modelo controla los casos que se incluyen en el modelo de minería de datos. Por consiguiente, una consulta en la columna de estructura puede devolver solo los casos que se utilizaron en el modelo de minería de datos. Consulte la sección Ejemplos de este tema para obtener un ejemplo de código que muestre el efecto de los filtros de un modelo de minería de datos tanto en las tablas de casos como en una tabla anidada.  
  
 Para obtener más información sobre cómo usar esta función en una instrucción DMX SELECT, vea [SELECT FROM &#60;model&#62;. Los casos &#40;DMX&#41;](../dmx/select-from-model-cases-dmx.md) o [SELECT FROM &#60;Structure&#62;. CASOS](../dmx/select-from-structure-cases.md).  
  
## <a name="error-messages"></a>mensajes de error  
 Se produce el error de seguridad siguiente si el usuario no tiene el permiso de obtención de detalles en la estructura de minería de datos primaria:  
  
 El usuario '% {User/} ' no tiene permiso para obtener detalles de la estructura de minería de datos primaria del modelo de minería de datos '% {Model/} '.  
  
 Se genera un mensaje de error similar al siguiente si se especifica un nombre de columna de estructura no válido:  
  
 No se encontró la columna de estructura de minería de datos '% {Structure-Column-name/} ' en la estructura de minería de datos primaria '% {Structure/} ' en el contexto actual (línea% {Line/}, columna% {Column/}).  
  
## <a name="examples"></a>Ejemplos  
 Utilizaremos la estructura de minería de datos siguiente para estos ejemplos. Observe que la estructura de minería de datos contiene dos columnas de tabla anidada: `Products` y `Hobbies`. La tabla anidada en la columna `Hobbies` tiene una única columna que se utiliza como clave para la misma. La tabla anidada de la columna `Products` es una tabla anidada compleja que tiene una columna de clave y otras columnas que se usan para la entrada. Los ejemplos siguientes muestran cómo una estructura de minería de datos puede diseñarse para incluir muchas columnas diferentes, aunque un modelo no pueda utilizar cada columna. Algunas de estas columnas pueden no ser útiles en el nivel de modelo para generalizar patrones, pero pueden ser muy útiles en la obtención de detalles.  
  
```  
CREATE MINING STRUCTURE [MyStructure]   
(  
CustomerName TEXT KEY,  
Occupation TEXT DISCRETE,  
Age LONG CONTINUOUS,  
MaritalStatus TEXT DISCRETE,  
Income LONG CONTINUOUS,  
Products  TABLE  
 (  
    ProductNameTEXT KEY,  
    Quantity LONG CONTINUOUS,  
    OnSale BOOLEAN  DISCRETE  
)  
 Hobbies  TABLE  
 (  
    Hobby KEY  
 ))  
```  
  
 Después, cree un modelo de minería de datos basado en la estructura recién creada, utilizando el código de ejemplo siguiente:  
  
```  
ALTER MINING STRUCTURE [MyStructure] ADD MINING MODEL [MyModel] (  
CustomerName,  
Age,  
MaritalStatus,  
Income PREDICT,  
Products   
(  
ProductName  
) WITH FILTER(NOT OnSale)  
) USING Microsoft_Decision_Trees   
WITH FILTER(EXISTS (Products))  
```  
  
### <a name="sample-query-1-returning-a-column-from-the-mining-structure"></a>Consulta de ejemplo 1: Devolver una columna de la estructura de minería de datos  
 La consulta del ejemplo siguiente devuelve las columnas `CustomerName` y `Age`, que se definen para formar parte del modelo de minería de datos. Sin embargo, la consulta también devuelve la columna `Age`, que forma parte de la estructura pero no del modelo de minería de datos.  
  
```  
SELECT CustomerName, Age, StructureColumn('Occupation') FROM MyModel.CASES   
WHERE Age > 30  
```  
  
 Tenga en cuenta que el filtrado de filas para restringir los casos a los clientes con una edad superior a 30 años tiene lugar en el nivel del modelo. Por consiguiente, esta expresión no devolvería los casos que están incluidos en los datos de la estructura pero que no usa el modelo. Dado que la condición de filtro utilizada para crear el modelo (`EXISTS (Products)`) restringe los casos únicamente a los clientes que compraron productos, podría haber casos en la estructura que no devuelva esta consulta.  
  
### <a name="sample-query-2-applying-a-filter-to-the-structure-column"></a>Consulta de ejemplo 2: Aplicar un filtro a la columna de la estructura  
 La consulta del ejemplo siguiente no solo devuelve las columnas del modelo `CustomerName` y `Age`, y la tabla anidada `Products`, sino también el valor de la columna `Quantity` de la tabla anidada, que no forma parte del modelo.  
  
```  
SELECT CustomerName, Age,  
(SELECT ProductName, StructureColumn('Quantity') FROM Products) FROM MA.CASES   
WHERE StructureColumn('Occupation') = 'Architect'  
```  
  
 Tenga en cuenta que, en este ejemplo, se aplica un filtro a la columna de la estructura para restringir los casos a los clientes cuya`WHERE StructureColumn('Occupation') = 'Architect'`profesión sea ' arquitecto ' (). Dado que la condición de filtro del modelo siempre se aplica a los casos al crearse el modelo, solo se incluyen en los casos del modelo aquellos que tienen en la tabla `Products` por lo menos una fila que la cumpla. Por consiguiente, se aplica tanto el filtro en la tabla anidada `Products` como el filtro en el caso `('Occupation')`.  
  
### <a name="sample-query-3-selecting-columns-from-a-nested-table"></a>Consulta de ejemplo 3: Seleccionar columnas de una tabla anidada  
 La consulta del ejemplo siguiente devuelve los nombres de los clientes que se usaron como casos de entrenamiento del modelo. Para cada cliente, la consulta devuelve también una tabla anidada que contiene los detalles de la compra. Aunque el modelo incluye la `ProductName` columna, el modelo no utiliza el valor de la `ProductName` columna. El modelo solo comprueba si el producto se adquirió a precio`NOT``OnSale`normal (). Esta consulta no devuelve solo el nombre del producto, sino que también devuelve la cantidad comprada, que no está incluida en el modelo.  
  
```  
SELECT CustomerName,    
(SELECT ProductName, StructureColumn('Quantity')FROM Products)   
FROM MyModel.CASES  
```  
  
 Observe que no puede devolver las columnas `ProductName` o `Quantity` a menos que la obtención de detalles esté habilitada en el modelo de minería de datos.  
  
### <a name="sample-query-4-filtering-on-and-returning-nested-table-columns"></a>Consulta de ejemplo 4: Filtrar y devolver columnas de tablas anidadas  
 La siguiente consulta de ejemplo devuelve las columnas de tabla anidada y los casos que están incluidos en la estructura de minería de datos, pero no en el modelo. El modelo ya se filtra con la presencia de productos `OnSale`, pero esta consulta agrega un filtro en la columna de la estructura de minería de datos, `Quantity`:  
  
```  
SELECT CustomerName, Age, StructureColumn('Occupation'),   
(SELECT ProductName, StructureColumn('Quantity') FROM Products)   
FROM MyModel.CASES   
WHERE EXISTS (SELECT * FROM Products WHERE StructureColumn('Quantity')>1)  
```  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de funciones de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Funciones &#40;DMX&#41;](../dmx/functions-dmx.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)  
  
  
