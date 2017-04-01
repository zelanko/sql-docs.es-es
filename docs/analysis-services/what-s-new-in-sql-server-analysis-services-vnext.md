---
title: "Novedades de SQL Server Analysis Services vNext | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-vnext"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1eb6afc9-76ed-45a2-a188-374a4fc23224
caps.latest.revision: 17
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 13
---
# Novedades de SQL Server Analysis Services vNext
[!INCLUDE[tsql-appliesto-ssvNxt-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssvnxt-xxxx-xxxx-xxx.md)]

## <a name="sql-server-analysis-services-on-windows-ctp-12"></a>SQL Server Analysis Services en Windows CTP 1.2

No hay características nuevas en esta versión. Las mejoras incluyen corrección de errores y mejoras de rendimiento.

La versión preliminar más reciente de SQL Server Data Tools (SSDT), que coincide con SQL Server vNext CTP 1.2, mejora con la nueva experiencia moderna de Get Data presentada en CTP 1.1 con un nuevo menú del editor de consultas y una funcionalidad de acceso rápido. 

## <a name="sql-server-analysis-services-on-windows-ctp-11"></a>SQL Server Analysis Services en Windows CTP 1.1 

Esta versión incluye mejoras para los modelos tabulares. 

### <a name="1400-compatibility-level-for-tabular-models"></a>Nivel de compatibilidad&1400; para modelos tabulares
  Para aprovechar las ventajas que ofrecen las características y las funcionalidades descritas en este artículo, los modelos tabulares nuevos o existentes deben establecerse en el nivel de compatibilidad 1400. Los modelos con el nivel de compatibilidad 1400 no pueden implementarse en SQL Server 2016 SP1 o versiones anteriores, ni degradarse a niveles de compatibilidad inferiores.
  
  Para crear proyectos de modelos tabulares con el nivel de compatibilidad 1400 o actualizar proyectos existentes a dicho nivel, descargue e instale una **versión preliminar** de [SQL Server Data Tools (SSDT) 17.0 RC2](https://go.microsoft.com/fwlink?LinkId=837939). 
  
En SSDT, puede seleccionar el nuevo nivel de compatibilidad 1400 al crear proyectos de modelos tabulares. 

![AS_NewTabular1400Project](../analysis-services/media/as-newtabular1400project.png)

>[!NOTE] El área de trabajo integrada en la versión de diciembre de SQL Server Data Tools (SSDT) es compatible con el nivel de compatibilidad 1400. Si crea proyectos de modelos tabulares en una instancia de servidor del área de trabajo, dicha instancia y cualquier instancia en la que implemente deben ser de [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] CTP 1.1. 

Para actualizar un modelo tabular existente en SSDT, en el Explorador de soluciones, haga clic con el botón derecho en **Model.bim** y, después, en **Propiedades**, establezca la propiedad **Nivel de compatibilidad** en **SQL Server vNext (1400)**. 

![AS_Model_Properties](../analysis-services/media/as-model-properties.png)

### <a name="modern-get-data-experience"></a>Experiencia moderna de Obtener datos
La versión preliminar más reciente de SQL Server Data Tools (SSDT), que coincide con la versión [!INCLUDE[ssSQLv14_md](../includes/sssqlv14-md.md)] CTP 1.1, incluye una experiencia moderna de **Obtener datos** para los modelos tabulares en el nivel de compatibilidad 1400. Esta característica nueva se basa en una funcionalidad similar de Power BI Desktop y Microsoft Excel 2016.

![AS_Get_Data_in_SSDT](../analysis-services/media/as-get-data-in-ssdt.png)

>[!NOTE] En esta versión, se admite un número limitado de orígenes de datos. Las actualizaciones futuras serán compatibles con funcionalidades y orígenes de datos adicionales.

Para obtener más información sobre la experiencia moderna de Obtener datos, consulte el [Blog del equipo de Analysis Services](https://blogs.msdn.microsoft.com/analysisservices/2016/12/16/introducing-a-modern-get-data-experience-for-sql-server-vnext-on-windows-ctp-1-1-for-analysis-services/).

## <a name="ragged-hierarchies"></a>Jerarquías desiguales
En los modelos tabulares, puede modelar jerarquías de elementos primarios y secundarios. Las jerarquías con un número diferente de niveles suelen denominarse jerarquías desiguales. De forma predeterminada, las jerarquías desiguales se muestran con espacios en blanco para los niveles situados por debajo del elemento secundario más bajo. Este es un ejemplo de una jerarquía desigual en un organigrama:

![AS_Ragged_Hierarchy](../analysis-services/media/as-ragged-hierarchy.png)

En esta versión se incluye la propiedad **Ocultar miembros**. Puede establecer la propiedad **Ocultar miembros** de una jerarquía en **Hide blank members** (Ocultar miembros en blanco).

![AS_Hide_Blank_Members](../analysis-services/media/as-hide-blank-members.png)

 >[!NOTE] Los miembros en blanco del modelo se representan mediante un valor DAX en blanco, en lugar de una cadena vacía.

Cuando se establece en **Hide blank members** (Ocultar miembros en blanco) y se implementa el modelo, se muestra una versión de la jerarquía más fácil de leer en los clientes de informes, como Excel.

![AS_Non_Ragged_Hierarchy](../analysis-services/media/as-non-ragged-hierarchy.png)

### <a name="detail-rows"></a>Filas de detalles
Ahora puede definir un conjunto de filas personalizado que contribuya a un valor de medida. La opción Filas de detalles es similar a la acción de obtención de detalles predeterminada de los modelos multidimensionales. Permite a los usuarios finales ver la información con más detalle que el nivel agregado. 

En la siguiente tabla de dinámica se muestran las ventas totales por Internet por año del modelo tabular de ejemplo de Adventure Works. Para ver las filas de detalles, haga clic con el botón derecho en una celda con un valor agregado de la medida y, después, haga clic en **Mostrar detalles**.

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
Esta versión incluye un operador `IN` para expresiones DAX. Esto es similar al operador [`TSQL IN`](https://msdn.microsoft.com/library/ms177682.aspx) que se suele usar para especificar varios valores en una cláusula `WHERE`.

Antes, lo habitual era especificar filtros de valores múltiples mediante el operador lógico `OR`, como en la expresión de medida siguiente:

```
Filtered Sales:=CALCULATE (
        [Internet Total Sales],
                 'Product'[Color] = "Red"
            || 'Product'[Color] = "Blue"
            || 'Product'[Color] = "Black"
    )
```

Esto se ha simplificado mediante el operador `IN`:
```
Filtered Sales:=CALCULATE (
        [Internet Total Sales], 'Product'[Color] IN { "Red", "Blue", "Black" }
    )
```

En este caso, el operador `IN` hace referencia a una tabla de una sola columna con tres filas, una para cada uno de los colores especificados. Observe que la sintaxis del constructor de tabla usa llaves.

El operador `IN` es funcionalmente equivalente a la función `CONTAINSROW`:
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

Con el nuevo operador `IN`, la expresión de medida anterior ahora es equivalente a la siguiente:
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
## <a name="future-updates"></a>Actualizaciones futuras
En versiones futuras se incluirán mejoras adicionales. Este artículo se actualizará con anuncios importantes sobre las características nuevas de SQL Server vNext.
