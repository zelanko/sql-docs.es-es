---
title: Novedades de SQL Server 2017 Analysis Services | Microsoft Docs
ms.date: 03/08/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 711b577b737b48012e1bed0a52ba599cf17b3d8f
ms.sourcegitcommit: 0a7beb2f51e48889b4a85f7c896fb650b208eb36
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/09/2019
ms.locfileid: "57685762"
---
# <a name="whats-new-in-sql-server-2017-analysis-services"></a>Novedades de SQL Server 2017 Analysis Services
[!INCLUDE[ssas-appliesto-sql2017](../includes/ssas-appliesto-sql2017.md)]

SQL Server 2017 Analysis Services vea algunas de las mejoras más importantes desde SQL Server 2012. Cuando se crean en el éxito de modo Tabular (introdujo por primera vez en SQL Server 2012 Analysis Services), esta versión, los modelos tabulares más poderosa que nunca.

Modo multidimensional y Power Pivot para el modo de SharePoint son un elemento esencial para muchas implementaciones de Analysis Services. En el ciclo de vida del producto de Analysis Services, están maduros estos modos. No hay ninguna característica nueva para cada uno de estos modos en esta versión. Sin embargo, se incluyen correcciones de errores y mejoras de rendimiento.

Las características descritas aquí se incluyen en SQL Server 2017 Analysis Services. Pero para sacar provecho de ellas, también debe usar las versiones más recientes de [SQL Server Data Tools](../ssdt/download-sql-server-data-tools-ssdt.md) (SSDT) y [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md) (SSMS). SSDT y SSMS se actualiza mensualmente con nuevas y mejoradas características que normalmente coincidan con la nueva funcionalidad en SQL Server.  

Si bien es importante obtener información sobre las nuevas características, también es importante saber lo que se está en desuso y ya no se incluye en esta versión y las versiones futuras. Asegúrese de consultar [compatibilidad con versiones anteriores (SQL Server 2017 Analysis Services)](analysis-services-backward-compatibility-sql2017.md).

Echemos un vistazo a algunas de las nuevas características clave en esta versión.

## <a name="1400-compatibility-level-for-tabular-models"></a>Nivel de compatibilidad 1400 para modelos tabulares.
  Para aprovechar muchas de las nuevas características y funcionalidad que se describe aquí, deben establecerse modelos tabulares nuevos o existentes o actualizar al nivel de compatibilidad 1400. Los modelos con el nivel de compatibilidad 1400 no pueden implementarse en SQL Server 2016 SP1 o versiones anteriores, ni degradarse a niveles de compatibilidad inferiores. Para obtener más información, consulte [nivel de compatibilidad para modelos tabulares de Analysis Services](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md).
  
En SSDT, puede seleccionar el nuevo nivel de compatibilidad 1400 al crear proyectos de modelos tabulares. 

![AS_NewTabular1400Project](../analysis-services/media/as-newtabular1400project.png)


Para actualizar un modelo tabular existente en SSDT, en el Explorador de soluciones, haga clic en **Model.bim**y, a continuación, en **propiedades**, establezca el **ivel** propiedad  **SQL Server 2017 (1400)**. 

![AS_Model_Properties](../analysis-services/media/as-model-properties.png)

Es importante tener en cuenta que, una vez que actualice un modelo existente a 1400, no se puede cambiar. No olvide guardar una copia de seguridad de la base de datos del modelo 1200.

## <a name="modern-get-data-experience"></a>Experiencia moderna de Obtener datos
Cuando se trata de importar datos de orígenes de datos en los modelos tabulares, SQL Server Data Tools (SSDT) presenta la versión moderna **obtener datos** experiencia para los modelos en el nivel de compatibilidad 1400. Esta característica nueva se basa en una funcionalidad similar de Power BI Desktop y Microsoft Excel 2016. La experiencia moderna de obtener datos proporciona capacidades de mashup de datos y transformación de datos gran mediante el generador de consultas de obtención de datos y expresiones de M.

La experiencia moderna de obtener datos proporciona compatibilidad para una amplia gama de orígenes de datos. A partir de ahora, las actualizaciones incluirá compatibilidad para conocer mucho más.

![AS_Get_Data_in_SSDT](../analysis-services/media/as-get-data-in-ssdt.png)

 Una interfaz de usuario intuitiva y eficaz facilita la selección de los datos y las capacidades de transformación/mashup de datos más fáciles que nunca.

![Mashup avanzada](../analysis-services/media/as-get-data-advanced.png)


Experimente la moderna de obtener datos y capacidades de mashup de M no se aplican a upraded de modelos tabulares existentes desde el nivel de compatibilidad 1200 1400. La nueva experiencia solo se aplica a los modelos nuevos creados en el nivel de compatibilidad 1400.

## <a name="encoding-hints"></a>Sugerencias de codificación
Esta versión presenta sugerencias de codificación, una característica avanzada que se usa para optimizar el procesamiento (actualización de datos) de los modelos tabulares en memoria grandes. Para entender mejor la codificación, vea [Performance Tuning de modelos tabulares en SQL Server 2012 Analysis Services](https://msdn.microsoft.com/library/dn393915.aspx) notas del producto para comprender mejor la codificación.

* Codificación del valor proporciona un mejor rendimiento de las consultas para las columnas que solo se usan normalmente para las agregaciones.

* Codificación hash es preferible para las columnas de group by (a menudo valores de tabla de dimensiones) y las claves externas. Las columnas de cadena siempre son hash codificado.

Las columnas numéricas pueden utilizar cualquiera de estos métodos de codificación. Cuando Analysis Services empieza a procesar una tabla, si bien la tabla está vacía (con o sin particiones) o se realiza una operación de procesamiento de la tabla completa, se toman valores de ejemplo para que cada columna determinar si se debe aplicar codificación de hash o valor numérico . De forma predeterminada, la codificación del valor se elige cuando el ejemplo de valores distintos en la columna es lo suficientemente grande como; en caso contrario, normalmente codificación hash proporciona una mejor compresión. Es posible que Analysis Services cambiar el método de codificación después de la columna se ha procesado parcialmente basándose en más información sobre la distribución de datos y reiniciar el proceso de codificación Sin embargo, esto aumenta el tiempo de procesamiento y es ineficaz. Las notas del producto de optimización del rendimiento trata de volver a codificar con más detalle y describen cómo detectar mediante SQL Server Profiler.

Sugerencias de codificación permiten el Modelador especificar una preferencia para el método de codificación tiene conocimiento previo de generación de perfiles de datos o en respuesta a volver a codificar los eventos de seguimiento. Puesto que la agregación con las columnas con codificación hash es más lento de a través de las columnas de valor codificado, valor de codificación puede especificarse como una sugerencia para estas columnas. No se garantiza que se aplica la preferencia. Es una sugerencia en lugar de una configuración. Para especificar una sugerencia de codificación, establezca la propiedad EncodingHint en la columna. Los valores posibles son "Default", "Value" y "Hash". El siguiente fragmento de metadatos basados en JSON desde el archivo Model.bim especifica el valor de codificación para la columna Sales Amount.

```
{
    "name": "Sales Amount",
    "dataType": "decimal",
    "sourceColumn": "SalesAmount",
    "formatString": "\\$#,0.00;(\\$#,0.00);\\$#,0.00",
    "sourceProviderType": "Currency",
    "encodingHint": "Value"
}
```

## <a name="ragged-hierarchies"></a>Jerarquías desiguales
En los modelos tabulares, puede modelar jerarquías de elementos primarios y secundarios. Las jerarquías con un número diferente de niveles suelen denominarse jerarquías desiguales. De forma predeterminada, las jerarquías desiguales se muestran con espacios en blanco para los niveles situados por debajo del elemento secundario más bajo. Este es un ejemplo de una jerarquía desigual en un organigrama:

![AS_Ragged_Hierarchy](../analysis-services/media/as-ragged-hierarchy.png)

En esta versión se incluye la propiedad **Ocultar miembros** . Puede establecer la propiedad **Ocultar miembros** de una jerarquía en **Hide blank members**(Ocultar miembros en blanco).

![AS_Hide_Blank_Members](../analysis-services/media/as-hide-blank-members.png)

 >[!NOTE]
 > Los miembros en blanco del modelo se representan mediante un valor DAX en blanco, en lugar de una cadena vacía.

Cuando se establece en **Hide blank members**(Ocultar miembros en blanco) y se implementa el modelo, se muestra una versión de la jerarquía más fácil de leer en los clientes de informes, como Excel.

![AS_Non_Ragged_Hierarchy](../analysis-services/media/as-non-ragged-hierarchy.png)


## <a name="detail-rows"></a>Filas de detalles
Ahora puede definir un conjunto de filas personalizado que contribuya a un valor de medida. La opción Filas de detalles es similar a la acción de obtención de detalles predeterminada de los modelos multidimensionales. Permite a los usuarios finales ver la información con más detalle que el nivel agregado. 

En la siguiente tabla de dinámica se muestran las ventas totales por Internet por año del modelo tabular de ejemplo de Adventure Works. Para ver las filas de detalles, haga clic con el botón derecho en una celda con un valor agregado de la medida y, después, haga clic en **Mostrar detalles** .

![AS_Show_Details](../analysis-services/media/as-show-details.png)

De forma predeterminada, se muestran los datos asociados en la tabla de ventas por Internet. Este comportamiento limitado no suele ser significativo para el usuario, ya que la tabla podría no tener las columnas necesarias para mostrar información útil, como el nombre del cliente y la información del pedido. Con Filas de detalles, puede especificar una propiedad **Expresión de filas de detalles** para las medidas.

#### <a name="detail-rows-expression-property-for-measures"></a>Propiedad Expresión de filas de detalles para medidas
La propiedad **Expresión de filas de detalles** para las medidas permite a los autores de modelos personalizar las columnas y las filas que se devuelven al usuario final.

![AS_Detail_Rows_Expression_Property](../analysis-services/media/as-detail-rows-expression-property.png)

El [SELECTCOLUMNS](https://msdn.microsoft.com/library/mt761759.aspx) función DAX se usa normalmente en una expresión de filas de detalle. En el ejemplo siguiente se definen las columnas que se devuelven para las filas de la tabla de ventas por Internet del modelo tabular de ejemplo de Adventure Works:

```
SELECTCOLUMNS(
    'Internet Sales',
    "Customer First Name", RELATED( Customer[Last Name]),
    "Customer Last Name", RELATED( Customer[First Name]),
    "Order Date", 'Internet Sales'[Order Date],
    "Internet Total Sales", [Internet Total Sales]
)
```

Una vez que se ha definido la propiedad y se ha implementado el modelo, se devuelve un conjunto de filas personalizado cuando el usuario selecciona **Mostrar detalles**. Se respeta automáticamente el contexto de filtro de la celda que se ha seleccionado. En este ejemplo, solo se muestran las filas del valor 2010:

![AS_Detail_Rows](../analysis-services/media/as-detail-rows.png)

#### <a name="default-detail-rows-expression-property-for-tables"></a>Propiedad Expresión de filas de detalles predeterminada para tablas
Además de las medidas, las tablas también tienen una propiedad para definir una expresión de filas de detalles. La propiedad **Expresión de filas de detalles predeterminada** actúa como valor predeterminado para todas las medidas de la tabla. Las medidas que no tienen su propia expresión definida hereda de la expresión de la tabla y mostrar el conjunto de filas definido para la tabla. Esto permite reutilizar las expresiones y nuevas medidas que se agregan a la tabla automáticamente más tarde hereda la expresión.

![AS_Default_Detail_Rows_Expression](../analysis-services/media/as-default-detail-rows-expression.png)
 
#### <a name="detailrows-dax-function"></a>Función DAX DETAILROWS
En esta versión se incluye una nueva función DAX `DETAILROWS` que devuelve el conjunto de filas definido por la expresión de filas de detalles. Funciona de forma similar a la instrucción `DRILLTHROUGH` en MDX, que también es compatible con las expresiones de filas de detalles definidas en modelos tabulares.

La siguiente consulta DAX devuelve el conjunto de filas definido por la expresión de filas de detalles para la medida o su tabla. Si no se define ninguna expresión, se devuelven los datos de la tabla de ventas por Internet, ya que es la tabla que contiene la medida.

```
EVALUATE DETAILROWS([Internet Total Sales])
```

## <a name="object-level-security"></a>Seguridad de nivel de objeto
Esta versión presenta [seguridad de nivel de objeto](../analysis-services/tabular-models/object-level-security.md) para tablas y columnas. Además de restringir el acceso a los datos de tabla y columna, se pueden proteger nombres de tablas y columnas confidenciales. Esto ayuda a impedir que un usuario malintencionado detecte la existencia de una tabla.

Seguridad de nivel de objeto se debe establecer mediante metadatos basados en JSON, Tabular Model Scripting Language (TMSL) o el modelo de objetos tabulares (TOM). 

Por ejemplo, el código siguiente ayuda a proteger la tabla Product del modelo tabular de ejemplo de Adventure Works. Para ello, establece la propiedad **MetadataPermission** de la clase **TablePermission** en **None**.

```
//Find the Users role in Adventure Works and secure the Product table
ModelRole role = db.Model.Roles.Find("Users");
Table productTable = db.Model.Tables.Find("Product");
if (role != null && productTable != null)
{
    TablePermission tablePermission;
    if (role.TablePermissions.Contains(productTable.Name))
    {
        tablePermission = role.TablePermissions[productTable.Name];
    }
    else
    {
        tablePermission = new TablePermission();
        role.TablePermissions.Add(tablePermission);
        tablePermission.Table = productTable;
    }
    tablePermission.MetadataPermission = MetadataPermission.None;
}
db.Update(UpdateOptions.ExpandFull);
```

## <a name="dynamic-management-views-dmvs"></a>Vistas de administración dinámica (DMV)
[DMV](../analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md) son consultas en SQL Server Profiler que devuelven información sobre las operaciones del servidor local y el estado del servidor.
Esta versión incluye mejoras a [vistas de administración dinámica](https://docs.microsoft.com/sql/analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services) (DMV) para los modelos tabulares en los niveles de compatibilidad 1200 y 1400.

[DISCOVER_CALC_DEPENDENCY](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-calc-dependency-rowset) ahora funciona con los modelos tabulares 1200 y 1400. Los modelos tabulares 1400 mostrar las dependencias entre las particiones de M, expresiones de M y orígenes de datos estructurados. Para obtener más información, consulte el [blog de Analysis Services](https://blogs.msdn.microsoft.com/analysisservices/2017/07/17/whats-new-in-sql-server-2017-rc1-for-analysis-services/).

[MDSCHEMA_MEASUREGROUP_DIMENSIONS](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/mdschema-measuregroup-dimensions-rowset) mejoras se incluyen para esta DMV, que se usa por diversas herramientas de cliente para mostrar la dimensionalidad de medida. Por ejemplo, la característica de exploración en las tablas dinámicas de Excel permite al usuario para la exploración entre a dimensiones relacionadas con las medidas seleccionadas. Esta versión corrige las columnas de la cardinalidad, que anteriormente se mostraban valores incorrectos.

## <a name="dax-enhancements"></a>Mejoras de DAX
Esta versión incluye compatibilidad con nuevas funciones de DAX y funciones. Con el fin de aprovechar las ventajas, deberá usar la versión más reciente de SSDT. Para obtener más información, consulte [funciones DAX nuevas](https://msdn.microsoft.com/library/mt704075.aspx).

Una de las partes más importantes de las nuevas funciones DAX es el nuevo [operador IN Function CONTAINSROW](https://msdn.microsoft.com/library/mt842621.aspx) para expresiones DAX. Esto es similar al operador [`TSQL IN`](https://msdn.microsoft.com/library/ms177682.aspx) que se suele usar para especificar varios valores en una cláusula `WHERE` .

Antes, lo habitual era especificar filtros de valores múltiples mediante el operador lógico `OR` , como en la expresión de medida siguiente:

```
Filtered Sales:=CALCULATE (
        [Internet Total Sales],
                 'Product'[Color] = "Red"
            || 'Product'[Color] = "Blue"
            || 'Product'[Color] = "Black"
    )
```

Esto se ha simplificado mediante el operador `IN` :
```
Filtered Sales:=CALCULATE (
        [Internet Total Sales], 'Product'[Color] IN { "Red", "Blue", "Black" }
    )
```

En este caso, el operador `IN` hace referencia a una tabla de una sola columna con tres filas, una para cada uno de los colores especificados. Observe que la sintaxis del constructor de tabla usa llaves.

El operador `IN` es funcionalmente equivalente a la función `CONTAINSROW` :
```
Filtered Sales:=CALCULATE (
        [Internet Total Sales], CONTAINSROW({ "Red", "Blue", "Black" }, 'Product'[Color])
    )
```

El operador `IN` también se puede usar eficazmente con constructores de tabla. Por ejemplo, la medida siguiente filtra por combinaciones de colores y categorías de producto:
```
Filtered Sales:=CALCULATE (
        [Internet Total Sales],
        FILTER( ALL('Product'),
              ( 'Product'[Color] = "Red"   && Product[Product Category Name] = "Accessories" )
         || ( 'Product'[Color] = "Blue"  && Product[Product Category Name] = "Bikes" )
         || ( 'Product'[Color] = "Black" && Product[Product Category Name] = "Clothing" )
        )
    )
```

Con el nuevo operador `IN` , la expresión de medida anterior ahora es equivalente a la siguiente:
```
Filtered Sales:=CALCULATE (
        [Internet Total Sales],
        FILTER( ALL('Product'),
            ('Product'[Color], Product[Product Category Name]) IN
            { ( "Red", "Accessories" ), ( "Blue", "Bikes" ), ( "Black", "Clothing" ) }
        )
    )
```

## <a name="additional-improvements"></a>Mejoras adicionales
Además de todas las características nuevas, Analysis Services, SSDT y SSMS también incluyen las siguientes mejoras:

* Reutilización de la jerarquía y la columna aparece en ubicaciones más útiles en la lista de campos de Power BI.
* Relaciones de fecha para crear fácilmente relaciones a las dimensiones de fecha en función de los campos de fecha.
* Opción de instalación predeterminada de Analysis Services es ahora para el modo tabular.
* Nuevos orígenes de datos obtener datos (Power Query).
* Editor DAX para SSDT.
* Compatibilidad con orígenes de datos DirectQuery existentes M de consultas.
* Mejoras de SSMS, como ver, editar y compatibilidad de scripting de orígenes de datos estructurados.



## <a name="see-also"></a>Vea también
[Notas de la versión SQL Server 2017](../sql-server/sql-server-2017-release-notes.md)   
[Novedades de SQL Server 2017](../sql-server/what-s-new-in-sql-server-2017.md)
