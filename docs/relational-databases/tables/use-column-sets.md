---
title: Usar conjuntos de columnas | Microsoft Docs
ms.custom: ''
ms.date: 07/30/2015
ms.prod: sql
ms.prod_service: table-view-index, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- sparse columns, column sets
- column sets
ms.assetid: a4f9de95-dc8f-4ad8-b957-137e32bfa500
caps.latest.revision: 28
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 221ee8a61bb5c433332b1cf293d019d849e20568
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "33012922"
---
# <a name="use-column-sets"></a>Usar conjuntos de columnas
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Las tablas que utilizan columnas dispersas pueden designar un conjunto de columnas que devuelva todas las columnas dispersas de la tabla. Un conjunto de columnas es una representación XML sin tipo que combina todas las columnas dispersas de una tabla en una salida estructurada. Un conjunto de columnas se asemeja a una columna calculada en que el conjunto no se almacena físicamente en la tabla. Un conjunto de columnas difiere de una columna calculada en que el conjunto de columnas se puede actualizar directamente.  
  
 Considere la posibilidad de usar los conjuntos de columnas cuando una tabla contenga un gran número de columnas y resulte complicado realizar cualquier operación con ellas. Las aplicaciones pueden experimentar ciertas mejoras de rendimiento si realizan la selección e inserción de datos usando los conjuntos de columnas en tablas que contienen muchas columnas. Sin embargo, es posible que se reduzca el rendimiento de los conjuntos de columnas si se definen muchos índices en las columnas de la tabla. Esto es debido a que aumenta la cantidad de memoria necesaria para un plan de ejecución.  
  
 Para definir un conjunto de columnas, use las palabras clave *<nombreDeConjuntoDeColumnas>* FOR ALL_SPARSE_COLUMN de las instrucciones [CREATE TABLE](../../t-sql/statements/create-table-transact-sql.md) o [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md).  
  
## <a name="guidelines-for-using-column-sets"></a>Directrices para usar conjuntos de columnas  
 Cuando use conjuntos de columnas, tenga en cuenta las directrices siguientes:  
  
-   Se pueden agregar columnas dispersas y un conjunto de columnas como parte de la misma instrucción.  
  
-   No se puede agregar un conjunto de columnas a una tabla si ésta ya contiene columnas dispersas.  
  
-   El conjunto de columnas no puede modificarse. Para modificar un conjunto de columnas, es preciso eliminar y volver a crear las columnas dispersas.  
  
-   Se puede agregar un conjunto de columnas a una tabla si ésta no incluye ninguna columna dispersa. Si posteriormente se agregan columnas dispersas a la tabla, dichas columnas aparecerán en el conjunto de columnas.  
  
-   Solo se permite un conjunto de columnas por tabla.  
  
-   El conjunto de columnas es opcional y no es necesario para usar columnas dispersas.  
  
-   No se pueden definir restricciones ni valores predeterminados en un conjunto de columnas.  
  
-   Las columnas calculadas no pueden contener columnas del conjunto de columnas.  
  
-   Las consultas distribuidas no se pueden utilizar en tablas que contienen conjuntos de columnas.  
  
-   La replicación no admite conjuntos de columnas.  
  
-   La captura de datos modificados no admite conjuntos de columnas.  
  
-   Un conjunto de columnas no puede formar parte de ningún tipo de índice. Esto incluye índices XML, índices de texto completo y vistas indizadas. Un conjunto de columnas no se puede agregar como columna incluida en ningún índice.  
  
-   Un conjunto de columnas no se puede utilizar en la expresión de filtro de un índice filtrado o de estadísticas filtradas.  
  
-   Cuando una vista incluye un conjunto de columnas, éste aparece en la vista como una columna XML.  
  
-   Un conjunto de columnas no se puede incluir en la definición de una vista indizada.  
  
-   Las vistas con particiones que incluyen tablas que contienen conjuntos de columnas se actualizan cuando la vista con particiones especifica las columnas dispersas por nombre. Una vista con particiones no se actualiza cuando hace referencia al conjunto de columnas.  
  
-   Las notificaciones de consulta que hacen referencia a conjuntos de columnas no se permiten.  
  
-   Los datos XML tienen un límite de tamaño de 2 GB. Si los datos combinados de todas las columnas dispersas cuyo valor de una fila no sea NULL superan este límite, la consulta o la operación DML generará un error.  
  
-   Para obtener más información sobre los datos devueltos por la función COLUMNS_UPDATED, vea [Usar columnas dispersas](../../relational-databases/tables/use-sparse-columns.md).  
  
## <a name="guidelines-for-selecting-data-from-a-column-set"></a>Directrices para seleccionar datos de un conjunto de columnas  
 Tenga en cuenta las directrices siguientes a la hora de seleccionar datos de un conjunto de columnas:  
  
-   Conceptualmente, un conjunto de columnas es un tipo de columna XML calculada y actualizable que agrega un conjunto de columnas relacionales subyacentes en una única representación XML. El conjunto de columnas solo admite la propiedad ALL_SPARSE_COLUMNS. Esta propiedad se usa para agregar todos los valores distintos de NULL de todas las columnas dispersas para una fila determinada.  
  
-   En el editor de tablas de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , los conjuntos de columnas se muestran como un campo XML modificable. Defina los conjuntos de columnas con el siguiente formato:  
  
    ```  
    <column_name_1>value1</column_name_1><column_name_2>value2</column_name_2>...  
    ```  
  
     A continuación se enumeran algunos ejemplos de valores de conjuntos de columnas:  
  
    -   `<sparseProp1>10</sparseProp1><sparseProp3>20</sparseProp3>`  
  
    -   `<DocTitle>Bicycle Parts List</DocTitle><Region>West</Region>`  
  
-   Las columnas dispersas que contienen valores NULL se omiten en la representación XML del conjunto de columnas.  
  
> [!WARNING]  
>  Al agregar un conjunto de columnas, cambia el comportamiento de las consultas SELECT *. La consulta devolverá el conjunto de columnas como una columna XML, pero no devolverá las columnas dispersas individuales. Los diseñadores de esquemas y los desarrolladores deben tener cuidado de no alterar el comportamiento de las aplicaciones existentes.  
  
## <a name="inserting-or-modifying-data-in-a-column-set"></a>Insertar o modificar datos en un conjunto de columnas  
 La manipulación de los datos de una columna dispersa se puede llevar a cabo usando el nombre de las columnas individuales, o bien haciendo referencia al nombre del conjunto de columnas y especificando sus valores usando el formato XML de dicho conjunto. Las columnas dispersas pueden aparecer en cualquier orden en la columna XML.  
  
 Cuando se insertan o actualizan valores de columnas dispersas usando el conjunto de columnas XML, los valores que se insertan en las columnas dispersas subyacentes se convierten de manera implícita desde el tipo de datos **xml** . En el caso de columnas numéricas, un valor en blanco en el XML para la columna numérica se convierte en una cadena vacía. Esto hace que se inserte un cero en la columna numérica, tal y como se muestra en el ejemplo siguiente.  
  
```  
CREATE TABLE t (i int SPARSE, cs xml column_set FOR ALL_SPARSE_COLUMNS);  
GO  
INSERT t(cs) VALUES ('<i/>');  
GO  
SELECT i FROM t;  
GO  
```  
  
 En este ejemplo, no se ha especificado ningún valor para la columna `i`, pero se ha insertado el valor `0` .  
  
## <a name="using-the-sqlvariant-data-type"></a>Usar el tipo de datos sql_variant  
 El tipo de datos **sql_variant** puede almacenar varios tipos de datos distintos, como **int**, **char**y **date**. Los conjuntos de columnas generan la información sobre el tipo de datos, como la escala, la precisión y la información de configuración regional que se asocia a un valor **sql_variant** , como atributos en la columna XML generada. Si intenta proporcionar estos atributos en una instrucción XML generada de forma personalizada como una entrada para una operación de inserción o de actualización en un conjunto de columnas, algunos de dichos atributos son obligatorios y a otros se les asigna un valor predeterminado. En la tabla siguiente se enumeran los tipos de datos y los valores predeterminados que genera el servidor cuando no se proporciona el valor.  
  
|Tipo de datos|localeID*|sqlCompareOptions|sqlCollationVersion|SqlSortId|Longitud máxima|Precisión|Escala|  
|---------------|----------------|-----------------------|-------------------------|---------------|--------------------|---------------|-----------|  
|**char**, **varchar**, **binary**|-1|'Default'|0|0|8000|No aplicable**|No aplicable|  
|**nvarchar**|-1|'Default'|0|0|4000|No aplicable|No aplicable|  
|**decimal**, **float**, **real**|No aplicable|No aplicable|No aplicable|No aplicable|No aplicable|18|0|  
|**integer**, **bigint**, **tinyint**, **smallint**|No aplicable|No aplicable|No aplicable|No aplicable|No aplicable|No aplicable|No aplicable|  
|**datetime2**|No aplicable|No aplicable|No aplicable|No aplicable|No aplicable|No aplicable|7|  
|**datetime offset**|No aplicable|No aplicable|No aplicable|No aplicable|No aplicable|No aplicable|7|  
|**datetime**, **date**, **smalldatetime**|No aplicable|No aplicable|No aplicable|No aplicable|No aplicable|No aplicable|No aplicable|  
|**money**, **smallmoney**|No aplicable|No aplicable|No aplicable|No aplicable|No aplicable|No aplicable|No aplicable|  
|**time**|No aplicable|No aplicable|No aplicable|No aplicable|No aplicable|No aplicable|7|  
  
 \*  Un valor -1 en localeID significa la configuración regional predeterminada. La configuración regional en inglés es 1033.  
  
 No aplicable = No se genera ningún valor para estos atributos durante una operación de selección en el conjunto de columnas. Genera un error cuando el autor de la llamada especifica un valor para este atributo en la representación XML proporcionada para un conjunto de columnas durante una operación de inserción o actualización.  
  
## <a name="security"></a>Seguridad  
 El modelo de seguridad para un conjunto de columnas funciona de forma similar al modelo de seguridad existente entre la tabla y columnas. Los conjuntos de columnas se pueden visualizar en forma de minitabla, en la que una operación de selección funciona como una operación SELECT *. Pero la relación entre el conjunto de columnas y las columnas dispersas es una relación de agrupación en lugar de ser estrictamente un contenedor. El modelo de seguridad comprueba la seguridad en la columna del conjunto de columnas y respeta las operaciones DENY en las columnas dispersas subyacentes. Las características adicionales del modelo de seguridad son las siguientes:  
  
-   Los permisos de seguridad se pueden otorgar y revocar desde la columna del conjunto de columnas, de forma similar a como se haría en cualquier otra columna de la tabla.  
  
-   Una instrucción GRANT o REVOKE para los permisos SELECT, INSERT, UPDATE, DELETE o REFERENCES en una columna del conjunto de columnas no se propaga a las columnas miembro subyacentes de dicho conjunto. Solo se aplica al uso de la columna del conjunto de columnas. El permiso DENY en un conjunto de columnas sí se propaga a las columnas dispersas subyacentes de la tabla.  
  
-   La ejecución de las instrucciones SELECT, INSERT, UPDATE y DELETE en la columna del conjunto de columnas requiere que el usuario disponga de los permisos correspondientes en dicha columna, así como en todas las columnas dispersas de la tabla. Dado que el conjunto de columnas representa todas las columnas dispersas de la tabla, debe tener el permiso correspondiente en estas columnas, y esto incluye aquellas columnas dispersas que no va a modificar.  
  
-   La ejecución de una instrucción REVOKE en una columna dispersa o en un conjunto de columnas hace que éstas adopten la configuración de seguridad de su objeto primario.  
  
## <a name="examples"></a>Ejemplos  
 En los ejemplos siguientes, una tabla de documentos contiene el conjunto de columnas común `DocID` y `Title`. El grupo de producción desea tener una columna `ProductionSpecification` y una columna `ProductionLocation` para todos los documentos de producción. El grupo de marketing desea tener una columna `MarketingSurveyGroup` para los documentos de marketing.  
  
### <a name="a-creating-a-table-that-has-a-column-set"></a>A. Crear una tabla que tenga un conjunto de columnas  
 En el ejemplo siguiente se crea la tabla que utiliza columnas dispersas y se incluye el conjunto de columnas `SpecialPurposeColumns`. El ejemplo inserta dos filas en la tabla y, a continuación, selecciona datos de dicha tabla.  
  
> [!NOTE]  
>  Esta tabla solo tiene cinco columnas para facilitar su visualización y lectura.  
  
```  
USE AdventureWorks2012;  
GO  
  
CREATE TABLE DocumentStoreWithColumnSet  
    (DocID int PRIMARY KEY,  
     Title varchar(200) NOT NULL,  
     ProductionSpecification varchar(20) SPARSE NULL,  
     ProductionLocation smallint SPARSE NULL,  
     MarketingSurveyGroup varchar(20) SPARSE NULL,  
     MarketingProgramID int SPARSE NULL,  
     SpecialPurposeColumns XML COLUMN_SET FOR ALL_SPARSE_COLUMNS);  
GO  
```  
  
### <a name="b-inserting-data-to-a-table-by-using-the-names-of-the-sparse-columns"></a>B. Insertar datos en una tabla usando los nombres de las columnas dispersas  
 En los ejemplos siguientes se insertan dos filas en la tabla creada en el ejemplo A. Estos ejemplos utilizan los nombres de las columnas dispersas y no hacen referencia al conjunto de columnas.  
  
```  
INSERT DocumentStoreWithColumnSet (DocID, Title, ProductionSpecification, ProductionLocation)  
VALUES (1, 'Tire Spec 1', 'AXZZ217', 27);  
GO  
  
INSERT DocumentStoreWithColumnSet (DocID, Title, MarketingSurveyGroup)  
VALUES (2, 'Survey 2142', 'Men 25 - 35');  
GO  
```  
  
### <a name="c-inserting-data-to-a-table-by-using-the-name-of-the-column-set"></a>C. Insertar datos en una tabla usando el nombre del conjunto de columnas  
 En el ejemplo siguiente se inserta una tercera fila en la tabla creada en el ejemplo A. Esta vez no se utilizan los nombres de las columnas dispersas. En su lugar, se utiliza el nombre del conjunto de columnas y la operación de inserción proporciona los valores para dos de las cuatro columnas dispersas en formato XML.  
  
```  
INSERT DocumentStoreWithColumnSet (DocID, Title, SpecialPurposeColumns)  
VALUES (3, 'Tire Spec 2', '<ProductionSpecification>AXW9R411</ProductionSpecification><ProductionLocation>38</ProductionLocation>');  
GO  
```  
  
### <a name="d-observing-the-results-of-a-column-set-when-select--is-used"></a>D. Observar los resultados de un conjunto de columnas al usar SELECT *  
 En el ejemplo siguiente se seleccionan todas las columnas de la tabla que contiene un conjunto de columnas. Devuelve una columna XML con los valores combinados de las columnas dispersas. No devuelve las columnas dispersas de forma individual.  
  
```  
SELECT DocID, Title, SpecialPurposeColumns FROM DocumentStoreWithColumnSet ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `DocID Title        SpecialPurposeColumns`  
  
 `1      Tire Spec 1  <ProductionSpecification>AXZZ217</ProductionSpecification><ProductionLocation>27</ProductionLocation>`  
  
 `2      Survey 2142  <MarketingSurveyGroup>Men 25 - 35</MarketingSurveyGroup>`  
  
 `3      Tire Spec 2  <ProductionSpecification>AXW9R411</ProductionSpecification><ProductionLocation>38</ProductionLocation>`  
  
### <a name="e-observing-the-results-of-selecting-the-column-set-by-name"></a>E. Observar los resultados de seleccionar el conjunto de columnas por nombre  
 Dado que el departamento de producción no está interesado en los datos de marketing, en este ejemplo se agrega una cláusula `WHERE` para restringir la salida. El ejemplo usa el nombre del conjunto de columnas.  
  
```  
SELECT DocID, Title, SpecialPurposeColumns  
FROM DocumentStoreWithColumnSet  
WHERE ProductionSpecification IS NOT NULL ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `DocID Title        SpecialPurposeColumns`  
  
 `1     Tire Spec 1  <ProductionSpecification>AXZZ217</ProductionSpecification><ProductionLocation>27</ProductionLocation>`  
  
 `3     Tire Spec 2  <ProductionSpecification>AXW9R411</ProductionSpecification><ProductionLocation>38</ProductionLocation>`  
  
### <a name="f-observing-the-results-of-selecting-sparse-columns-by-name"></a>F. Observar los resultados de seleccionar columnas dispersas por nombre  
 Si una tabla contiene un conjunto de columnas, también se puede consultar dicha tabla usando los nombres de columna individuales, tal y como se muestra en el ejemplo siguiente.  
  
```  
SELECT DocID, Title, ProductionSpecification, ProductionLocation   
FROM DocumentStoreWithColumnSet  
WHERE ProductionSpecification IS NOT NULL ;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `DocID Title        ProductionSpecification ProductionLocation`  
  
 `1     Tire Spec 1  AXZZ217                 27`  
  
 `3     Tire Spec 2  AXW9R411                38`  
  
### <a name="g-updating-a-table-by-using-a-column-set"></a>G. Actualizar una tabla usando un conjunto de columnas  
 En el ejemplo siguiente se actualiza el tercer registro con nuevos valores para las dos columnas dispersas que usa la fila.  
  
```  
UPDATE DocumentStoreWithColumnSet  
SET SpecialPurposeColumns = '<ProductionSpecification>ZZ285W</ProductionSpecification><ProductionLocation>38</ProductionLocation>'  
WHERE DocID = 3 ;  
GO  
```  
  
> [!IMPORTANT]  
>  Una instrucción UPDATE que usa un conjunto de columnas actualiza todas las columnas dispersas de la tabla. Los valores de las columnas dispersas a las que no se hace referencia se actualizan a NULL.  
  
 En el ejemplo siguiente se actualiza el tercer registro, pero solo se especifica el valor de una de las dos columnas rellenadas. La segunda columna, `ProductionLocation` , no está incluida en la instrucción `UPDATE` y se actualiza a NULL.  
  
```  
UPDATE DocumentStoreWithColumnSet  
SET SpecialPurposeColumns = '<ProductionSpecification>ZZ285W</ProductionSpecification>'  
WHERE DocID = 3 ;  
GO  
```  
  
## <a name="see-also"></a>Ver también  
 [Usar columnas dispersas](../../relational-databases/tables/use-sparse-columns.md)  
  
  
