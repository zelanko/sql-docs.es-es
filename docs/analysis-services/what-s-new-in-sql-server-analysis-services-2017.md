---
title: "¿Qué &#39; s nuevo en Analysis Services de SQL Server de 2017 | Documentos de Microsoft"
ms.custom: 
ms.date: 07/27/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 1eb6afc9-76ed-45a2-a188-374a4fc23224
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 572af6f86f015c88141bb6e78b781b5825be155c
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="what39s-new-in-sql-server-2017-analysis-services"></a>¿Qué &#39; s nuevo en Analysis Services de SQL Server de 2017
[!INCLUDE[tsql-appliesto-ssvNxt-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]


## <a name="sql-server-2017-analysis-services-rc2"></a>SQL Server de 2017 Analysis Services RC2
No hay características nuevas en esta versión. Mejoras en esta versión incluyen correcciones de errores y rendimiento.

## <a name="sql-server-2017-analysis-services-rc1"></a>Analysis Services RC1 SQL Server de 2017
No hay ninguna característica nueva en esta versión, sin embargo, esta versión incluye mejoras adicionales de [vistas de administración dinámica](https://docs.microsoft.com/sql/analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services) (DMV) para los modelos tabulares en los niveles de compatibilidad 1200 y 1400.

DISCOVER_CALC_DEPENDENCY ahora funciona con los modelos tabulares de 1200 y 1400. Los modelos tabulares 1400 mostrar las dependencias entre las particiones de M, expresiones de M y orígenes de datos estructurados. Para obtener más información, consulte el [blog de Analysis Services](https://blogs.msdn.microsoft.com/analysisservices/).

MDSCHEMA_MEASUREGROUP_DIMENSIONS mejoras se incluyen para esta DMV, que se usa con diversas herramientas de cliente para mostrar las dimensiones de medida. Por ejemplo, la característica de exploración en las tablas dinámicas de Excel permite al usuario entre detalles a dimensiones relacionadas con las medidas seleccionadas. Esta versión corrige las columnas de cardinalidad, que anteriormente estaban que muestra valores incorrectos.

## <a name="sql-server-analysis-services-ctp-21"></a>Analysis Services SQL Server CTP 2.1
No hay características nuevas en esta versión. Mejoras en esta versión incluyen correcciones de errores y rendimiento y mejoras a [vistas de administración dinámica](https://docs.microsoft.com/sql/analysis-services/instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services) (DMV). DMV son consultas en SQL Server Profiler que devuelven información acerca de las operaciones del servidor local y el estado del servidor. Para obtener más información, consulte el [blog de Analysis Services](https://blogs.msdn.microsoft.com/analysisservices/).

## <a name="sql-server-analysis-services-ctp-20"></a>SQL Server Analysis Services en CTP 2.0
Esta versión tiene muchas mejoras nuevas para un modelo tabular, incluidos:

* Seguridad de nivel de objeto para proteger los metadatos de los modelos tabulares.
* Mejoras de rendimiento de transacción para una experiencia de desarrollador mayor capacidad de respuesta.
* Mejoras de la vista de administración dinámica para los modelos 1200 y 1400 Habilitar análisis de dependencias y los informes.
* Mejoras en la experiencia de creación para las expresiones de filas de detalle.
* Jerarquía y la columna volver a usar para aparecer en ubicaciones más relevantes en la lista de campos de Power BI.
* Relaciones de fecha para crear fácilmente las relaciones a las dimensiones de fecha en función de los campos de fecha.
* Opción de instalación predeterminada para Analysis Services ahora es para el modo tabular.
* Nuevos orígenes de datos de obtener datos (Power Qery).
* Editor DAX para SSDT.
* Orígenes de datos de DirectQuery existentes se admiten para M de consultas.
* Mejoras de SSMS, por ejemplo, ver, modificar y compatibilidad con scripting para orígenes de datos estructurados.

Para obtener más detalles sobre esta versión de CTP 2.0, consulte el [blog de Analysis Services](https://blogs.msdn.microsoft.com/analysisservices/).

## <a name="sql-server-analysis-services-on-windows-ctp-14"></a>SQL Server Analysis Services en Windows CTP 1.4
[SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/sql-server-data-tools-ssdt-release-candidate) y [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms-release-candidate) versiones preliminares coincidan con versiones preliminares de SQL Server 2017. Asegúrese de usar la versión más reciente para obtener nuevas características. Para obtener más información, consulte el [blog de Analysis Services](https://blogs.msdn.microsoft.com/analysisservices/).



## <a name="sql-server-analysis-services-on-windows-ctp-13"></a>SQL Server Analysis Services en CTP 1.3 de Windows

### <a name="encoding-hints"></a>Sugerencias de codificación

Esta versión presenta sugerencias de codificación, una característica avanzada que se utiliza para optimizar el procesamiento (actualización de datos) de los modelos tabulares de gran tamaño en memoria. Para entender mejor la codificación, vea [rendimiento para la optimización de los modelos tabulares en SQL Server 2012 Analysis Services](https://msdn.microsoft.com/library/dn393915.aspx) notas del producto para comprender mejor la codificación. El proceso de codificación que se describen aquí se aplica en el CTP 1.3.

* Codificación del valor proporciona un mejor rendimiento de las consultas para las columnas que normalmente se usan únicamente para las agregaciones.

* Codificación de hash es preferible columnas group by (a menudo valores de tabla de dimensiones) y claves externas. Las columnas de cadena siempre son hash codificado.

Las columnas numéricas pueden utilizar cualquiera de estos métodos de codificación. Cuando Analysis Services inicia el procesamiento de una tabla, si bien la tabla está vacía (con o sin particiones) o se realiza una operación de procesamiento de la tabla completa, se toman los valores de ejemplos para que cada columna determinar si se debe aplicar la codificación de hash o valor numérico . De forma predeterminada, la codificación del valor se elige cuando el ejemplo de valores distintos en la columna es lo suficientemente grande; en caso contrario, la codificación de hash suelen proporcionar una mejor compresión. Es posible que Analysis Services cambiar el método de codificación después de la columna se ha procesado parcialmente basándose en obtener más información sobre la distribución de datos y reinicie el proceso de codificación. Por supuesto, esto aumenta el tiempo de procesamiento y es ineficaz. Las notas del producto ajuste del rendimiento describen recodificación con más detalle y cómo detectar mediante SQL Server Profiler.

Sugerencias de codificación en la CTP 1.3 permiten el Modelador especificar una preferencia para el método de codificación tiene conocimiento previo de generación de perfiles de datos o en respuesta a volver a codificar los eventos de seguimiento. Puesto que la agregación de las columnas con codificación hash es más lenta de sobre columnas valor codificado, codificación de valor se puede especificar como una sugerencia para estas columnas. No se garantiza que se aplicará la preferencia; por lo tanto, es una sugerencia en lugar de una configuración. Para especificar una sugerencia de codificación, establezca la propiedad EncodingHint en la columna. Los valores posibles son "Default", "Valor" y "Hash". En el momento de escribir este artículo, la propiedad no se expone todavía en SSDT, por lo que debe establecerse con el modelo de objeto Tabular (TOM), Tabular Model Scripting Language (TMSL) o los metadatos basados en JSON. El siguiente fragmento de JSON en función de metadatos desde el archivo Model.bim especifica el valor de codificación para la columna de importe de ventas.

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

### <a name="extended-events-not-working-in-ctp-13"></a>No funciona en CTP 1.3 de eventos extendidos
Eventos extendidos de SSAS no funcionan en CTP 1.3. Una corrección está planeada en la siguiente versión de CTP.

## <a name="sql-server-analysis-services-on-windows-ctp-12"></a>SQL Server Analysis Services en Windows CTP 1.2

No hay características nuevas en esta versión. Las mejoras incluyen corrección de errores y mejoras de rendimiento.

La versión preliminar más reciente de SQL Server Data Tools (SSDT), que coincide con la versión de CTP de 2017 SQL Server 1.2, mejora la nueva experiencia moderna de obtener datos introducida en CTP 1.1 con nuevo menú de editor de consultas y la funcionalidad de acceso rápido. 

## <a name="sql-server-analysis-services-on-windows-ctp-11"></a>SQL Server Analysis Services en Windows CTP 1.1 

Esta versión incluye mejoras para los modelos tabulares. 

### <a name="1400-compatibility-level-for-tabular-models"></a>Nivel de compatibilidad&1400; para modelos tabulares
  Para aprovechar las ventajas que ofrecen las características y las funcionalidades descritas en este artículo, los modelos tabulares nuevos o existentes deben establecerse en el nivel de compatibilidad 1400. Los modelos con el nivel de compatibilidad 1400 no pueden implementarse en SQL Server 2016 SP1 o versiones anteriores, ni degradarse a niveles de compatibilidad inferiores.
  
  Para crear proyectos de modelos tabulares con el nivel de compatibilidad 1400 o actualizar proyectos existentes a dicho nivel, descargue e instale una **versión preliminar** de [SQL Server Data Tools (SSDT) 17.0 RC2](https://go.microsoft.com/fwlink?LinkId=837939). 
  
En SSDT, puede seleccionar el nuevo nivel de compatibilidad 1400 al crear proyectos de modelos tabulares. 

![AS_NewTabular1400Project](../analysis-services/media/as-newtabular1400project.png)

>[!NOTE]
> El área de trabajo integrada en la versión de diciembre de SQL Server Data Tools (SSDT) es compatible con el nivel de compatibilidad 1400. Si crea proyectos de modelos tabulares en una instancia de servidor del área de trabajo, dicha instancia y cualquier instancia en la que implemente deben ser de [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] CTP 1.1. 

Para actualizar un modelo tabular existente en SSDT, en el Explorador de soluciones, haga clic en **Model.bim**y, a continuación, en **propiedades**, establezca el **nivel de compatibilidad** propiedad  **SQL Server de 2017 (1400)**. 

![AS_Model_Properties](../analysis-services/media/as-model-properties.png)

### <a name="modern-get-data-experience"></a>Experiencia moderna de Obtener datos
La versión preliminar más reciente de SQL Server Data Tools (SSDT), que coincide con la versión [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] CTP 1.1, incluye una experiencia moderna de **Obtener datos** para los modelos tabulares en el nivel de compatibilidad 1400. Esta característica nueva se basa en una funcionalidad similar de Power BI Desktop y Microsoft Excel 2016.

![AS_Get_Data_in_SSDT](../analysis-services/media/as-get-data-in-ssdt.png)

>[!NOTE]
> En esta versión, se admite un número limitado de orígenes de datos. Las actualizaciones futuras serán compatibles con funcionalidades y orígenes de datos adicionales.

Para obtener más información sobre la experiencia moderna de Obtener datos, consulte el [Blog del equipo de Analysis Services](https://blogs.msdn.microsoft.com/analysisservices/2016/12/16/introducing-a-modern-get-data-experience-for-sql-server-2017-on-windows-ctp-1-1-for-analysis-services/).

## <a name="ragged-hierarchies"></a>Jerarquías desiguales
En los modelos tabulares, puede modelar jerarquías de elementos primarios y secundarios. Las jerarquías con un número diferente de niveles suelen denominarse jerarquías desiguales. De forma predeterminada, las jerarquías desiguales se muestran con espacios en blanco para los niveles situados por debajo del elemento secundario más bajo. Este es un ejemplo de una jerarquía desigual en un organigrama:

![AS_Ragged_Hierarchy](../analysis-services/media/as-ragged-hierarchy.png)

En esta versión se incluye la propiedad **Ocultar miembros** . Puede establecer la propiedad **Ocultar miembros** de una jerarquía en **Hide blank members**(Ocultar miembros en blanco).

![AS_Hide_Blank_Members](../analysis-services/media/as-hide-blank-members.png)

 >[!NOTE]
 > Los miembros en blanco del modelo se representan mediante un valor DAX en blanco, en lugar de una cadena vacía.

Cuando se establece en **Hide blank members**(Ocultar miembros en blanco) y se implementa el modelo, se muestra una versión de la jerarquía más fácil de leer en los clientes de informes, como Excel.

![AS_Non_Ragged_Hierarchy](../analysis-services/media/as-non-ragged-hierarchy.png)

### <a name="detail-rows"></a>Filas de detalles
Ahora puede definir un conjunto de filas personalizado que contribuya a un valor de medida. La opción Filas de detalles es similar a la acción de obtención de detalles predeterminada de los modelos multidimensionales. Permite a los usuarios finales ver la información con más detalle que el nivel agregado. 

En la siguiente tabla de dinámica se muestran las ventas totales por Internet por año del modelo tabular de ejemplo de Adventure Works. Para ver las filas de detalles, haga clic con el botón derecho en una celda con un valor agregado de la medida y, después, haga clic en **Mostrar detalles** .

![AS_Show_Details](../analysis-services/media/as-show-details.png)

De forma predeterminada, se muestran los datos asociados en la tabla de ventas por Internet. Este comportamiento limitado no suele ser significativo para el usuario, ya que la tabla podría no tener las columnas necesarias para mostrar información útil, como el nombre del cliente y la información del pedido. Con Filas de detalles, puede especificar una propiedad **Expresión de filas de detalles** para las medidas.

#### <a name="detail-rows-expression-property-for-measures"></a>Propiedad Expresión de filas de detalles para medidas
La propiedad **Expresión de filas de detalles** para las medidas permite a los autores de modelos personalizar las columnas y las filas que se devuelven al usuario final.

![AS_Detail_Rows_Expression_Property](../analysis-services/media/as-detail-rows-expression-property.png)

La función DAX [SELECTCOLUMNS](https://msdn.microsoft.com/library/mt761759.aspx) se usará normalmente en una expresión de filas de detalles. En el ejemplo siguiente se definen las columnas que se devuelven para las filas de la tabla de ventas por Internet del modelo tabular de ejemplo de Adventure Works:

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
Además de las medidas, las tablas también tienen una propiedad para definir una expresión de filas de detalles. La propiedad **Expresión de filas de detalles predeterminada** actúa como valor predeterminado para todas las medidas de la tabla. Las medidas que no tienen su propia expresión definida heredan la expresión la tabla y muestran el conjunto de filas definido para la tabla. Esto permite reutilizar las expresiones, y las medidas nuevas que se agreguen a la tabla más adelante heredarán automáticamente la expresión.

![AS_Default_Detail_Rows_Expression](../analysis-services/media/as-default-detail-rows-expression.png)
 
#### <a name="detailrows-dax-function"></a>Función DAX DETAILROWS
En esta versión se incluye una nueva función DAX `DETAILROWS` que devuelve el conjunto de filas definido por la expresión de filas de detalles. Funciona de forma similar a la instrucción `DRILLTHROUGH` en MDX, que también es compatible con las expresiones de filas de detalles definidas en modelos tabulares.

La siguiente consulta DAX devuelve el conjunto de filas definido por la expresión de filas de detalles para la medida o su tabla. Si no se define ninguna expresión, se devuelven los datos de la tabla de ventas por Internet, ya que es la tabla que contiene la medida.

```
EVALUATE DETAILROWS([Internet Total Sales])
```

## <a name="dax-enhancements"></a>Mejoras de DAX
Esta versión incluye un operador `IN` para expresiones DAX. Esto es similar al operador [`TSQL IN`](https://msdn.microsoft.com/library/ms177682.aspx) que se suele usar para especificar varios valores en una cláusula `WHERE` .

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


## <a name="table-level-security"></a>Seguridad de nivel de tabla
Esta versión incluye seguridad de nivel de tabla. Además de restringir el acceso a datos de la tabla, se pueden proteger nombres de tablas confidenciales. Esto ayuda a impedir que un usuario malintencionado detecte la existencia de una tabla.

La seguridad de nivel de tabla se debe establecer mediante metadatos basados en JSON, Tabular Model Scripting Language (TMSL) o el modelo de objetos tabulares (TOM). 

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


