---
title: Novedades de Analysis Services de SQL Server de 2017 | Documentos de Microsoft
ms.date: 10/27/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.topic: article
ms.assetid: 1eb6afc9-76ed-45a2-a188-374a4fc23224
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 14ce5d9110f49ce155e89a96e1f72618f2879661
ms.openlocfilehash: 68410430d97a0e3033e17deb7d03a0ba8fecd436
ms.contentlocale: es-es
ms.lasthandoff: 11/08/2017

---
# <a name="whats-new-in-sql-server-2017-analysis-services"></a>Novedades de Analysis Services de SQL Server de 2017
[!INCLUDE[ssas-appliesto-sql2017](../includes/ssas-appliesto-sql2017.md)]

Analysis Services de SQL Server de 2017 vea algunas de las mejoras más importantes desde SQL Server 2012. Compilar el correcto funcionamiento de modo Tabular (que inicialmente se introdujo en SQL Server 2012 Analysis Services), esta versión hace que los modelos tabulares más eficaces que nunca.

Modo multidimensional y Power Pivot para el modo de SharePoint son una grapa para muchas de las implementaciones de Analysis Services. En el ciclo de vida del producto de Analysis Services, estos modos son consolidados. No hay ninguna característica nueva para cada uno de estos modos en esta versión. Sin embargo, se incluyen correcciones de errores y mejoras de rendimiento.

Las características descritas aquí se incluyen en Analysis Services de SQL Server de 2017. Pero para sacar provecho de ellas, también debe usar las versiones más recientes de [SQL Server Data Tools](../ssdt/download-sql-server-data-tools-ssdt.md) (SSDT) y [SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md) (SSMS). SSDT y SSMS se actualiza mensualmente con características nuevas y mejoradas que normalmente coincidan con la nueva funcionalidad en SQL Server.  

Aunque es importante obtener información sobre las nuevas características, también es importante saber lo que se está en desuso y ya no disponible en esta versión y las versiones futuras. No olvide desproteger [compatibilidad con versiones anteriores (SQL Server 2017 Analysis Services)](analysis-services-backward-compatibility-sql2017.md).

¡Eche un vistazo a algunas de las nuevas características claves de esta versión.

## <a name="1400-compatibility-level-for-tabular-models"></a>Nivel de compatibilidad 1400 para modelos tabulares.
  Para beneficiarse de muchas de las nuevas características y funcionalidad descrita aquí, deben establecerse o actualizados al nivel de compatibilidad 1400 los modelos tabulares nuevos o existentes. Los modelos con el nivel de compatibilidad 1400 no pueden implementarse en SQL Server 2016 SP1 o versiones anteriores, ni degradarse a niveles de compatibilidad inferiores. Para obtener más información, consulte [nivel de compatibilidad para los modelos tabulares de Analysis Services](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md).
  
En SSDT, puede seleccionar el nuevo nivel de compatibilidad 1400 al crear proyectos de modelos tabulares. 

![AS_NewTabular1400Project](../analysis-services/media/as-newtabular1400project.png)


Para actualizar un modelo tabular existente en SSDT, en el Explorador de soluciones, haga clic en **Model.bim**y, a continuación, en **propiedades**, establezca el **nivel de compatibilidad** propiedad  **SQL Server de 2017 (1400)**. 

![AS_Model_Properties](../analysis-services/media/as-model-properties.png)

Es importante tener en cuenta que, una vez que se actualiza un modelo existente a 1400, no se puede cambiar. Asegúrese de mantener una copia de seguridad de la base de datos de modelo de 1200.

## <a name="modern-get-data-experience"></a>Experiencia moderna de Obtener datos
En cuanto a la importación de datos de orígenes de datos en los modelos tabulares, SQL Server Data Tools (SSDT) presenta el moderno **obtener datos** experiencia para los modelos en el nivel de compatibilidad de 1400. Esta característica nueva se basa en una funcionalidad similar de Power BI Desktop y Microsoft Excel 2016. La experiencia de obtener datos moderna proporciona capacidades de mashup de datos y transformación de datos gran mediante el generador de consultas de obtener datos y expresiones de M.

La experiencia de obtener datos moderna proporciona compatibilidad para una amplia gama de orígenes de datos. En el futuro, las actualizaciones incluyen compatibilidad con incluso más.

![AS_Get_Data_in_SSDT](../analysis-services/media/as-get-data-in-ssdt.png)

 Una interfaz de usuario intuitiva y eficaz facilita la selección de los datos y las capacidades de transformación/mashup de datos más fácil que nunca.

![Mashup avanzado](../analysis-services/media/as-get-data-advanced.png)


Obtener datos moderna experiencia y capacidades de mashup de M no se aplican a upraded de los modelos tabulares existente desde el nivel de compatibilidad de 1200 1400. La nueva experiencia solo se aplica a los modelos nuevos que se crean en el nivel de compatibilidad de 1400.

## <a name="encoding-hints"></a>Sugerencias de codificación
Esta versión presenta sugerencias de codificación, una característica avanzada que se utiliza para optimizar el procesamiento (actualización de datos) de los modelos tabulares de gran tamaño en memoria. Para entender mejor la codificación, vea [rendimiento para la optimización de los modelos tabulares en SQL Server 2012 Analysis Services](https://msdn.microsoft.com/library/dn393915.aspx) notas del producto para comprender mejor la codificación.

* Codificación del valor proporciona un mejor rendimiento de las consultas para las columnas que normalmente se usan únicamente para las agregaciones.

* Codificación de hash es preferible columnas group by (a menudo valores de tabla de dimensiones) y claves externas. Las columnas de cadena siempre son hash codificado.

Las columnas numéricas pueden utilizar cualquiera de estos métodos de codificación. Cuando Analysis Services inicia el procesamiento de una tabla, si bien la tabla está vacía (con o sin particiones) o se realiza una operación de procesamiento de la tabla completa, se toman los valores de ejemplos para que cada columna determinar si se debe aplicar la codificación de hash o valor numérico . De forma predeterminada, la codificación del valor se elige cuando el ejemplo de valores distintos en la columna es lo suficientemente grande: en caso contrario, la codificación de hash normalmente proporciona una mejor compresión. Es posible que Analysis Services cambiar el método de codificación después de la columna se ha procesado parcialmente basándose en obtener más información sobre la distribución de datos y reinicie el proceso de codificación; Sin embargo, esto aumenta el tiempo de procesamiento y es ineficaz. Las notas del producto ajuste del rendimiento describen recodificación con más detalle y cómo detectar mediante SQL Server Profiler.

Sugerencias de codificación permiten el Modelador especificar una preferencia para el método de codificación tiene conocimiento previo de generación de perfiles de datos o en respuesta a volver a codificar los eventos de seguimiento. Puesto que la agregación de las columnas con codificación hash es más lenta de sobre columnas valor codificado, codificación de valor se puede especificar como una sugerencia para estas columnas. No se garantiza que se aplica la preferencia. Es una sugerencia en lugar de una configuración. Para especificar una sugerencia de codificación, establezca la propiedad EncodingHint en la columna. Los valores posibles son "Default", "Valor" y "Hash". El siguiente fragmento de JSON en función de metadatos desde el archivo Model.bim especifica el valor de codificación para la columna de importe de ventas.

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
Además de las medidas, las tablas también tienen una propiedad para definir una expresión de filas de detalles. La propiedad **Expresión de filas de detalles predeterminada** actúa como valor predeterminado para todas las medidas de la tabla. Las medidas que no tiene su propia expresión definida hereda la expresión de la tabla y mostrar el conjunto definido para la tabla de filas. Esto permite reutilizar expresiones y nuevas medidas que se agrega a la tabla automáticamente más tarde hereda la expresión.

![AS_Default_Detail_Rows_Expression](../analysis-services/media/as-default-detail-rows-expression.png)
 
#### <a name="detailrows-dax-function"></a>Función DAX DETAILROWS
En esta versión se incluye una nueva función DAX `DETAILROWS` que devuelve el conjunto de filas definido por la expresión de filas de detalles. Funciona de forma similar a la instrucción `DRILLTHROUGH` en MDX, que también es compatible con las expresiones de filas de detalles definidas en modelos tabulares.

La siguiente consulta DAX devuelve el conjunto de filas definido por la expresión de filas de detalles para la medida o su tabla. Si no se define ninguna expresión, se devuelven los datos de la tabla de ventas por Internet, ya que es la tabla que contiene la medida.

```
EVALUATE DETAILROWS([Internet Total Sales])
```

## <a name="object-level-security"></a>Seguridad de nivel de objeto
Esta versión introduce [seguridad de nivel de objeto](../analysis-services/tabular-models/object-level-security.md) para tablas y columnas. Además de restringir el acceso a los datos de tabla y columna, se pueden proteger los nombres de tablas y columnas confidenciales. Esto ayuda a impedir que un usuario malintencionado detecte la existencia de una tabla.

Seguridad de nivel de objeto debe establecerse con el modelo de objeto Tabular (TOM), Tabular Model Scripting Language (TMSL) o los metadatos basados en JSON. 

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
[DMV](../analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md) son consultas en SQL Server Profiler que devuelven información acerca de las operaciones del servidor local y el estado del servidor.
Esta versión incluye mejoras en [vistas de administración dinámica](https://docs.microsoft.com/sql/analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services) (DMV) para los modelos tabulares en los niveles de compatibilidad 1200 y 1400.

[DISCOVER_CALC_DEPENDENCY](../analysis-services/schema-rowsets/xml/discover-calc-dependency-rowset.md) ahora funciona con los modelos tabulares de 1200 y 1400. Los modelos tabulares 1400 mostrar las dependencias entre las particiones de M, expresiones de M y orígenes de datos estructurados. Para obtener más información, consulte el [blog de Analysis Services](https://blogs.msdn.microsoft.com/analysisservices/2017/07/17/whats-new-in-sql-server-2017-rc1-for-analysis-services/).

[MDSCHEMA_MEASUREGROUP_DIMENSIONS](../analysis-services/schema-rowsets/ole-db-olap/mdschema-measuregroup-dimensions-rowset.md) mejoras se incluyen para esta DMV, que se usa con diversas herramientas de cliente para mostrar las dimensiones de medida. Por ejemplo, la característica de exploración en las tablas dinámicas de Excel permite al usuario entre detalles a dimensiones relacionadas con las medidas seleccionadas. Esta versión corrige las columnas de cardinalidad, que anteriormente estaban que muestra valores incorrectos.

## <a name="dax-enhancements"></a>Mejoras de DAX
Esta versión incluye compatibilidad con nuevas funciones de DAX y funcionalidad. Para aprovechar las ventajas, debe usar la versión más reciente de SSDT. Para obtener más información, consulte [funciones DAX nuevas](https://msdn.microsoft.com/library/mt704075.aspx).

Uno de los componentes más importantes de la nueva funcionalidad DAX es la nueva [operador IN / función CONTAINSROW](https://msdn.microsoft.com/library/mt842621.aspx) para las expresiones de DAX. Esto es similar al operador [`TSQL IN`](https://msdn.microsoft.com/library/ms177682.aspx) que se suele usar para especificar varios valores en una cláusula `WHERE` .

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

* Reutilización de la jerarquía y la columna aparece en ubicaciones más relevantes en la lista de campos de Power BI.
* Relaciones de fecha para crear fácilmente las relaciones a las dimensiones de fecha en función de los campos de fecha.
* Opción de instalación predeterminada para Analysis Services ahora es para el modo tabular.
* Nuevos orígenes de datos de obtener datos (Power Query).
* Editor DAX para SSDT.
* Orígenes de datos de DirectQuery existentes se admiten para M de consultas.
* Mejoras de SSMS, por ejemplo, ver, modificar y compatibilidad con scripting para orígenes de datos estructurados.



## <a name="see-also"></a>Vea también
[Notas de la versión SQL Server de 2017](../sql-server/sql-server-2017-release-notes.md)   
[Novedades de SQL Server 2017](../sql-server/what-s-new-in-sql-server-2017.md)

