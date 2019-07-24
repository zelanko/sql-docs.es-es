---
title: Grupos de cálculo en Analysis Services modelos tabulares | Microsoft Docs
ms.date: 07/24/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: af63f41555a021fc720c7d1e15778265fe7de500
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419530"
---
# <a name="calculation-groups-preview"></a>Grupos de cálculo (versión preliminar)
 
[!INCLUDE[ssas-appliesto-sql2019-aas](../../includes/ssas-appliesto-sql2019-aas.md)]

Los grupos de cálculo pueden reducir significativamente el número de medidas redundantes mediante la agrupación de expresiones de medida comunes como *elementos de cálculo*. Los grupos de cálculo se admiten en los modelos tabulares Azure Analysis Services y SQL Server Analysis Services 2019 en el [nivel de compatibilidad](compatibility-level-for-tabular-models-in-analysis-services.md)1470 y superior. Los modelos con el nivel de compatibilidad 1470 se encuentran actualmente en **versión preliminar**.  

En este artículo se explica: 

> [!div class="checklist"]
> * Ventajas 
> * Cómo funcionan los grupos de cálculos
> * Cadenas de formato dinámico
> * Pide
> * Prioridad
> * Herramientas
> * Limitaciones



## <a name="benefits"></a>Ventajas

Los grupos de cálculo abordan un problema en modelos complejos en los que puede haber una proliferación de medidas redundantes usando los mismos cálculos: más comunes con los cálculos de inteligencia de tiempo. Por ejemplo, un analista de ventas desea ver los totales de ventas y pedidos por mes hasta la fecha (MTD), el trimestre hasta la fecha (hasta), el año hasta la fecha (en el año), los pedidos del año anterior (PY), etc. El modelador de datos tiene que crear medidas independientes para cada cálculo, lo que puede conducir a docenas de medidas. Para el usuario, esto puede significar tener que ordenar por tantas medidas y aplicarlas individualmente a su informe. 

En primer lugar, echemos un vistazo a cómo aparecen los grupos de cálculos para los usuarios en una herramienta de informes como Power BI. A continuación, echaremos un vistazo a lo que conforma un grupo de cálculo y cómo se crean en un modelo.

Los grupos de cálculo se muestran en los clientes de informes como una tabla con una sola columna. La columna no es como una columna o dimensión típica, sino que representa uno o más cálculos reutilizables, o *elementos de cálculo* que se pueden aplicar a cualquier medida ya agregada al filtro de valores para una visualización.

En la siguiente animación, un usuario está analizando los datos de ventas de los años 2012 y 2013. Antes de aplicar un grupo de cálculo, la medida base común **ventas** calcula una suma de las ventas totales de cada mes. A continuación, el usuario desea aplicar cálculos de inteligencia de tiempo para obtener los totales de ventas para el mes hasta la fecha, el trimestre hasta la fecha, el año hasta la fecha, etc. Sin grupos de cálculo, el usuario tendría que seleccionar medidas de inteligencia de tiempo individuales.

Con un grupo de cálculo, en este ejemplo denominado **inteligencia de tiempo**, cuando el usuario arrastra el elemento de cálculo de **tiempo** al área de filtro de **columnas** , cada elemento de cálculo aparece como una columna independiente. Los valores de cada fila se calculan a partir de la medida base, **sales**.  

![Grupo de cálculo que se va a aplicar en Power BI](media/calculation-groups/calc-groups-pbi.gif)


Los grupos de cálculo  funcionan con medidas Dax explícitas. En este ejemplo, **sales** es una medida explícita ya creada en el modelo. Los grupos de cálculo no funcionan con medidas DAX implícitas. Por ejemplo, en Power BI las medidas implícitas se crean cuando un usuario arrastra las columnas a objetos visuales para ver los valores agregados, sin crear una medida explícita. En este momento, Power BI genera DAX para las medidas implícitas escritas como cálculos DAX en línea, lo que significa que las medidas implícitas no pueden funcionar con grupos de cálculo. Se ha introducido una nueva propiedad de modelo visible en el modelo de objetos tabulares (TOM), **DiscourageImplicitMeasures**. Actualmente, para crear grupos de cálculo, esta propiedad debe establecerse en **true**. Cuando se establece en true, Power BI Desktop en el modo de conexión dinámica deshabilita la creación de medidas implícitas.

## <a name="how-they-work"></a>Cómo funcionan

Ahora que ha visto cómo los grupos de cálculo benefician a los usuarios, echemos un vistazo a cómo se crea el ejemplo de grupo de cálculo de inteligencia de tiempo.

Antes de entrar en los detalles, vamos a introducir algunas nuevas funciones de DAX específicamente para los grupos de cálculo: 

[SELECTEDMEASURE](https://docs.microsoft.com/dax/selectedmeasure-function-dax) : lo usan las expresiones para que los elementos de cálculo hagan referencia a la medida que está actualmente en contexto. En este ejemplo, la medida sales.

[SELECTEDMEASURENAME](https://docs.microsoft.com/dax/selectedmeasurename-function-dax) : lo usan las expresiones para los elementos de cálculo para determinar la medida que está en contexto por nombre.

[ISSELECTEDMEASURE](https://docs.microsoft.com/dax/isselectedmeasure-function-dax) : lo usan las expresiones para los elementos de cálculo para determinar la medida que se encuentra en contexto se especifica en una lista de medidas.

[SELECTEDMEASUREFORMATSTRING](https://docs.microsoft.com/dax/selectedmeasureformatstring-function-dax) : lo usan las expresiones para que los elementos de cálculo recuperen la cadena de formato de la medida que está en contexto.

### <a name="time-intelligence-example"></a>Ejemplo de inteligencia de tiempo

Nombre de tabla- **inteligencia de tiempo**   
Cálculo de nombre de columna- **tiempo**   
Precedencia- **20**   

#### <a name="time-intelligence-calculation-items"></a>Elementos de cálculo de inteligencia de tiempo

**Current**

```dax
SELECTEDMEASURE()
```

**MTD**

```dax
CALCULATE(SELECTEDMEASURE(), DATESMTD(DimDate[Date]))
```

**QTD**

```dax
CALCULATE(SELECTEDMEASURE(), DATESQTD(DimDate[Date]))
```

**YTD**

```dax
CALCULATE(SELECTEDMEASURE(), DATESYTD(DimDate[Date]))
```

**PY**

```dax
CALCULATE(SELECTEDMEASURE(), SAMEPERIODLASTYEAR(DimDate[Date]))
```

**PY MTD**

```dax
CALCULATE(
    SELECTEDMEASURE(),
    SAMEPERIODLASTYEAR(DimDate[Date]),
    'Time Intelligence'[Time Calculation] = "MTD"
)
```

**PY HASTA**

```dax
CALCULATE(
    SELECTEDMEASURE(),
    SAMEPERIODLASTYEAR(DimDate[Date]),
    'Time Intelligence'[Time Calculation] = "QTD"
)
```

**PY EN AÑO**

```dax
CALCULATE(
    SELECTEDMEASURE(),
    SAMEPERIODLASTYEAR(DimDate[Date]),
    'Time Intelligence'[Time Calculation] = "YTD"
)
```

**YOY**

```dax
SELECTEDMEASURE() –
CALCULATE(
    SELECTEDMEASURE(),
    'Time Intelligence'[Time Calculation] = "PY"
)
```

**YOY%**

```dax
DIVIDE(
    CALCULATE(
        SELECTEDMEASURE(),
        'Time Intelligence'[Time Calculation]="YOY"
    ),
    CALCULATE(
        SELECTEDMEASURE(),
        'Time Intelligence'[Time Calculation]="PY"
    ),
)
```

Para probar este grupo de cálculo, puede ejecutar una consulta DAX en SSMS o en [Dax Studio](http://daxstudio.org/)de código abierto. YOY y YOY% se omiten en este ejemplo de consulta.

#### <a name="time-intelligence-query"></a>Consulta de inteligencia de tiempo

```dax
EVALUATE
CALCULATETABLE (
    SUMMARIZECOLUMNS (
        DimDate[CalendarYear],
        DimDate[EnglishMonthName],
        "Current", CALCULATE ( [Sales], 'Time Intelligence'[Time Calculation] = "Current" ),
        "QTD",     CALCULATE ( [Sales], 'Time Intelligence'[Time Calculation] = "QTD" ),
        "YTD",     CALCULATE ( [Sales], 'Time Intelligence'[Time Calculation] = "YTD" ),
        "PY",      CALCULATE ( [Sales], 'Time Intelligence'[Time Calculation] = "PY" ),
        "PY QTD",  CALCULATE ( [Sales], 'Time Intelligence'[Time Calculation] = "PY QTD" ),
        "PY YTD",  CALCULATE ( [Sales], 'Time Intelligence'[Time Calculation] = "PY YTD" )
    ),
    DimDate[CalendarYear] IN { 2012, 2013 }
)
```

#### <a name="time-intelligence-query-return"></a>Devolución de consulta de inteligencia de tiempo

La tabla devuelta muestra los cálculos de cada elemento de cálculo aplicado. Por ejemplo, puede ver hasta para marzo de 2012 es la suma de enero, febrero y marzo de 2012.

![Devolución de consulta](media/calculation-groups/calc-groups-query-return.png)


## <a name="dynamic-format-strings"></a>Cadenas de formato dinámico

Las *cadenas de formato dinámico* con grupos de cálculo permiten la aplicación condicional de cadenas de formato a medidas sin forzar a que devuelvan cadenas.

Los modelos tabulares admiten el formato dinámico de medidas mediante la función de [formato](https://docs.microsoft.com/dax/format-function-dax) de Dax. Sin embargo, la función FORMAT tiene la desventaja de devolver una cadena, forzando medidas que, de otro modo, serían numéricas para devolverse también como una cadena. Esto puede tener algunas limitaciones, como no trabajar con la mayoría de los objetos visuales de Power BI en función de los valores numéricos, como los gráficos.

### <a name="dynamic-format-strings-for-time-intelligence"></a>Cadenas de formato dinámico para la inteligencia de tiempo

Si observamos el ejemplo de inteligencia de tiempo mostrado anteriormente, todos los elementos de cálculo excepto **YOY%** deben usar el formato de la medida actual en contexto. Por ejemplo, el **año actual** calculado en la medida sales base debe ser Currency. Si se trata de un grupo de cálculo para algo como una medida base de pedidos, el formato sería numérico. No obstante, el **YOY%** debe ser un porcentaje, independientemente del formato de la medida base.

En el caso de **YOY%** , podemos invalidar la cadena de formato estableciendo la propiedad de expresión de cadena de formato en **0,00%;-0,00%; 0,00%** . Para obtener más información acerca de las propiedades de expresión de cadena de formato, consulte [propiedades de celda MDX-formato de contenido de cadena](../multidimensional-models/mdx/mdx-cell-properties-format-string-contents.md#numeric-values).

En este visual matriz en Power BI, verá **sales Current/YOY** y **Orders Current/YOY** retiene sus correspondientes cadenas de formato de medida base. **Sales YOY%** y **Orders YOY%** , sin embargo, reemplaza la cadena de formato para usar el formato de *porcentaje* .

![Inteligencia de tiempo en el visual de matriz](media/calculation-groups/calc-groups-dynamicstring-timeintel.png)

### <a name="dynamic-format-strings-for-currency-conversion"></a>Cadenas de formato dinámico para la conversión de moneda

Las cadenas de formato dinámico proporcionan una conversión de moneda sencilla. Considere el siguiente modelo de datos de Adventure Works. Se modela para la conversión de moneda *uno a varios* , tal y como se define en los [tipos de conversión](../currency-conversions-analysis-services.md#conversion-types).

![Tasa de moneda en el modelo tabular](media/calculation-groups/calc-groups-currency-conversion.png)

Se agrega una columna **FormatString** a la tabla **DimCurrency** y se rellena con las cadenas de formato de las monedas respectivas.

![Columna de cadena de formato](media/calculation-groups/calc-groups-formatstringcolumn.png)

En este ejemplo, el siguiente grupo de cálculo se define como:

### <a name="currency-conversion-example"></a>Ejemplo de conversión de moneda

Nombre de tabla: **conversión de moneda**   
Nombre de columna: **cálculo de conversión**   
Precedencia- **5**   

#### <a name="calculation-items-for-currency-conversion"></a>Elementos de cálculo para la conversión de moneda

**Sin conversión**

```dax
SELECTEDMEASURE()
```

**Moneda convertida**

```dax
IF(
    //Check one currency in context & not US Dollar, which is the pivot currency:
    SELECTEDVALUE( DimCurrency[CurrencyName], "US Dollar" ) = "US Dollar",
    SELECTEDMEASURE(),
    SUMX(
        VALUES(DimDate[Date]),
        CALCULATE( DIVIDE( SELECTEDMEASURE(), MAX(FactCurrencyRate[EndOfDayRate]) ) )
    )
)
```

Expresión de cadena de formato

```dax
SELECTEDVALUE(
    DimCurrency[FormatString],
    SELECTEDMEASUREFORMATSTRING()
)
```
La expresión de cadena de formato debe devolver una cadena escalar. Usa la nueva función [SELECTEDMEASUREFORMATSTRING](https://docs.microsoft.com/dax/selectedmeasureformatstring-function-dax) para revertir a la cadena de formato de medida base si hay varias monedas en el contexto de filtro.

La animación siguiente muestra la conversión de moneda de formato dinámico de la medida de **ventas** en un informe.

![Cadena de formato dinámico de conversión de moneda aplicada](media/calculation-groups/calc-groups-dynamic-format-string.gif)

## <a name="precedence"></a>Prioridad

Precedencia es una propiedad definida para un grupo de cálculo. Especifica el orden de evaluación cuando hay más de un grupo de cálculo. Un número mayor indica mayor prioridad, lo que significa que se evaluará antes que los grupos de cálculo con menor precedencia.

En este ejemplo, usaremos el mismo modelo que el ejemplo de inteligencia de tiempo anterior, pero también agregaremos un grupo de cálculo de promedios. El grupo de cálculo de promedios contiene el promedio de cálculos que son independientes de la inteligencia de tiempo tradicional en que no cambian el contexto de filtro de fecha, sino que solo aplican cálculos de promedio.

En este ejemplo, se define un cálculo de promedio diario. Los cálculos como, por ejemplo, los barriles medios de aceite al día son comunes en las aplicaciones de petróleo y gas. Otros ejemplos empresariales comunes incluyen la media de ventas de la tienda en el comercio minorista.

Aunque estos cálculos se calculan independientemente de los cálculos de inteligencia de tiempo, puede ser necesario combinarlos. Por ejemplo, es posible que un usuario desee ver los barriles de aceite al día de la semana para ver la tasa de aceite diaria desde el principio del año hasta la fecha actual. En este escenario, se debe establecer la prioridad de los elementos de cálculo.

### <a name="averages-example"></a>Ejemplo de promedios

El nombre de tabla es promedios.   
El nombre de la columna es el **cálculo medio**.   
La prioridad es **10**.   

#### <a name="calculation-items-for-averages"></a>Elementos de cálculo de promedios

**Sin promedio**

```dax
SELECTEDMEASURE()
```

**Media diaria**

```dax
DIVIDE(SELECTEDMEASURE(), COUNTROWS(DimDate))
```

A continuación se muestra un ejemplo de una consulta DAX y una tabla devuelta:

#### <a name="averages-query"></a>Promedio de consulta

```dax
EVALUATE
    CALCULATETABLE (
        SUMMARIZECOLUMNS (
        DimDate[CalendarYear],
        DimDate[EnglishMonthName],
        "Sales", CALCULATE (
            [Sales],
            'Time Intelligence'[Time Calculation] = "Current",
            'Averages'[Average Calculation] = "No Average"
        ),
        "YTD", CALCULATE (
            [Sales],
            'Time Intelligence'[Time Calculation] = "YTD",
            'Averages'[Average Calculation] = "No Average"
        ),
        "Daily Average", CALCULATE (
            [Sales],
            'Time Intelligence'[Time Calculation] = "Current",
            'Averages'[Average Calculation] = "Daily Average"
        ),
        "YTD Daily Average", CALCULATE (
            [Sales],
            'Time Intelligence'[Time Calculation] = "YTD",
            'Averages'[Average Calculation] = "Daily Average"
        )
    ),
    DimDate[CalendarYear] = 2012
)
```

#### <a name="averages-query-return"></a>Promedio de devolución de consulta

![Devolución de consulta](media/calculation-groups/calc-groups-ytd-daily-avg.png)

En la tabla siguiente se muestra cómo se calculan los valores de marzo de 2012.


|Nombre de columna  |Cálculo |
|---------|---------|
|YTD     |    Suma de ventas de Jan, Feb, mar 2012<br />= 495.364 + 506.994 + 373.483     |
|Media diaria    |     Ventas para marzo 2012 dividido entre el número de días de marzo<br />= 373.483/31       |
|Promedio diario actual     | HASTA el 1 de marzo de 2012 dividido entre el número de días de enero, febrero y marzo<br />= 1.375.841/(31 + 29 + 31)       |

Esta es la definición del elemento de cálculo del año actual, aplicado con prioridad de **20**.

```dax
CALCULATE(SELECTEDMEASURE(), DATESYTD(DimDate[Date]))
```

Esta es la media diaria, aplicada con una prioridad de **10**.

```dax
DIVIDE(SELECTEDMEASURE(), COUNTROWS(DimDate))
```

Dado que la precedencia del grupo de cálculo de inteligencia de tiempo es mayor que la del grupo de cálculo de promedios, se aplica de la manera más amplia posible. El cálculo de la media diaria del año actual se aplica al año actual al numerador y al denominador (recuento de días) del cálculo del promedio diario.

Esto es equivalente a la siguiente expresión:

```dax
CALCULATE(DIVIDE(SELECTEDMEASURE(), COUNTROWS(DimDate)), DATESYTD(DimDate[Date]))
```

No es esta expresión:

```dax
DIVIDE(CALCULATE(SELECTEDMEASURE(), DATESYTD(DimDate[Date])), COUNTROWS(DimDate)))
```

## <a name="sideways-recursion"></a>Recursividad lateral

En el ejemplo de inteligencia de tiempo anterior, algunos de los elementos de cálculo hacen referencia a otros en el mismo grupo de cálculo. Esto se denomina *recursividad lateral*. Por ejemplo, **YOY%** hace referencia tanto a **YOY** como a **py**.

```dax
DIVIDE(
    CALCULATE(
        SELECTEDMEASURE(),
        'Time Intelligence'[Time Calculation]="YOY"
    ),
    CALCULATE(
        SELECTEDMEASURE(),
        'Time Intelligence'[Time Calculation]="PY"
    ),
)
```

En este caso, ambas expresiones se evalúan por separado porque usan instrucciones calculadas diferentes. No se admiten otros tipos de recursividad.

## <a name="single-calculation-item-in-filter-context"></a>Elemento de cálculo único en el contexto de filtro

En nuestro ejemplo de inteligencia de tiempo, el elemento de cálculo de actualización del **año actual** tiene una sola expresión Calculate:

```dax
CALCULATE(
    SELECTEDMEASURE(),
    SAMEPERIODLASTYEAR(DimDate[Date]),
    'Time Intelligence'[Time Calculation] = "YTD"
)
```

El argumento del año actual para la función CALCULAte () reemplaza el contexto de filtro para reutilizar la lógica ya definida en el elemento de cálculo del año actual. No es posible aplicar PY y el año actual en una sola evaluación. Los grupos de cálculo *solo* se aplican si un solo elemento de cálculo del grupo de cálculo está en el contexto de filtro.

## <a name="mdx-support"></a>Compatibilidad con MDX

Los grupos de cálculo admiten consultas de expresiones de datos multidimensionales (MDX). Esto significa que los usuarios de Microsoft Excel, que consultan modelos de datos tabulares mediante MDX, pueden aprovechar al máximo los grupos de cálculo en tablas dinámicas y gráficos de hojas de cálculo.

## <a name="tools"></a>Herramientas

Todavía no se admiten grupos de cálculo en SQL Server Data Tools, Visual Studio con extensiones de Analysis Services. Sin embargo, los grupos de cálculo se pueden crear mediante tabular Model scripting Language (TMSL) o el [Editor tabular](https://github.com/otykier/TabularEditor)de código abierto.

## <a name="limitations"></a>Limitaciones

[Seguridad de nivel de objeto](object-level-security.md) (OLS) definido en las tablas de grupo de cálculo no se admite. Sin embargo, OLS se puede definir en otras tablas del mismo modelo. Si un elemento de cálculo hace referencia a un objeto protegido de OLS, se devuelve un error genérico.

[Seguridad de nivel de fila](roles-ssas-tabular.md#bkmk_rowfliters) (RLS) no se admite. Puede definir RLS en las tablas del mismo modelo, pero no en los propios grupos de cálculo (directa o indirectamente).

## <a name="see-also"></a>Vea también  

[DAX en modelos tabulares](understanding-dax-in-tabular-models-ssas-tabular.md)   
[Referencia de DAX](https://docs.microsoft.com/dax/data-analysis-expressions-dax-reference)  
