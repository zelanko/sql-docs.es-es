---
title: Grupos de cálculo en los modelos tabulares de Analysis Services | Microsoft Docs
ms.date: 06/09/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: abc1f51d21613676fd94271f931e1a7692cc1efc
ms.sourcegitcommit: 96090bb369ca8aba364c2e7f60b37165e5af28fc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/10/2019
ms.locfileid: "66822691"
---
# <a name="calculation-groups-preview"></a>Grupos de cálculo (versión preliminar)
 
[!INCLUDE[ssas-appliesto-sql2019-aas](../../includes/ssas-appliesto-sql2019-aas.md)]

Grupos de cálculo pueden reducir significativamente el número de medidas redundantes mediante la agrupación de las expresiones de medida común como *elementos cálculo*. Se admiten grupos de cálculo en Azure Analysis Services y SQL Server Analysis Services 2019 tabular se modela en la 1470 y versiones posteriores [ivel](compatibility-level-for-tabular-models-in-analysis-services.md). Los modelos en el nivel de compatibilidad 1470 están actualmente en **Preview**.  

En este artículo se explica: 

> [!div class="checklist"]
> * Ventajas 
> * Cómo funcionan los grupos de cálculo
> * Cadenas de formato dinámico
> * Prioridad
> * Herramientas
> * Limitaciones



## <a name="benefits"></a>Ventajas

Grupos de cálculo de solucionar un problema en modelos complejos, donde puede haber una proliferación de medidas redundantes con los mismos cálculos - más comunes con los cálculos de inteligencia de tiempo. Por ejemplo, un analista de ventas desea ver los totales de ventas y pedidos por mes hasta la fecha (MTD), quarter-to-date (QTD), año hasta la fecha (año actual), ordena year-to-date para el año anterior (PY) y así sucesivamente. El Modelador de datos tiene que crear medidas independientes para cada cálculo, que puede dar lugar a docenas de medidas. Para el usuario, esto puede significar tener que ordenar a través de tantas medidas y aplicarlas individualmente a su informe. 

En primer lugar, echemos un vistazo a cómo aparecen los grupos de cálculo a los usuarios en una herramienta informes como Power BI. A continuación, le echamos un vistazo a lo que constituye un grupo de cálculo y cómo se crean en un modelo.

Los grupos de cálculo se muestran en los clientes de informes como una tabla con una sola columna. La columna no es como una columna normal o una dimensión, en su lugar representa uno o varios cálculos reutilizables, o *elementos cálculo* que pueden aplicarse a cualquier medida ya agregado al filtro de valores para una visualización.

En la siguiente animación, un usuario está analizando los datos de ventas durante los años 2012 y 2013. Antes de aplicar un grupo de cálculo, la medida base común **ventas** calcula una suma de ventas totales para cada mes. A continuación, el usuario desea aplicar cálculos de inteligencia de tiempo para obtener los totales de ventas por mes hasta la fecha del trimestre hasta la fecha de año hasta la fecha y así sucesivamente. Sin grupos de cálculo, el usuario tendría que seleccionar medidas de inteligencia de tiempo individuales.

Con un grupo de cálculo, en este ejemplo se denomina **inteligencia de tiempo**, cuando el usuario arrastra el **calcular el tiempo** elemento a la **columnas** área, cada elemento de cálculo de filtro aparece como una columna independiente. Se calculan los valores para cada fila de la medida base, **ventas**.  

![Grupo de cálculo que se va a aplicar en Power BI](media/calculation-groups/calc-groups-pbi.gif)


Grupos de cálculo trabajar con **explícita** medidas DAX. En este ejemplo, **ventas** es una medida explícita que ya ha creado en el modelo. Grupos de cálculo no funcionan con las medidas implícitas de DAX. Por ejemplo, en Power BI, las medidas implícitas se crean cuando un usuario arrastra las columnas de objetos visuales para ver los valores agregados, sin necesidad de crear una medida explícita. En este momento, Power BI genera DAX para medidas implícitas que se escriben como en línea los cálculos de DAX - lo que significa que las medidas implícitas no se pueden trabajar con grupos de cálculo. Se ha introducido una nueva propiedad de modelo visible en el modelo de objetos tabulares (TOM), **DiscourageImplicitMeasures**. Actualmente, con el fin de crear grupos de cálculo de esta propiedad debe establecerse **true**. Cuando se establece en true, Power BI Desktop en Live Connect deshabilita el modo de creación de las medidas implícitas.

## <a name="how-they-work"></a>Cómo funcionan

Ahora que ha visto cómo benefician a los usuarios los grupos de cálculo, echemos un vistazo a cómo se crea el ejemplo de grupo de cálculo de inteligencia de tiempo mostrado.

Antes de entrar en detalles, vamos a introducir algunas nuevas funciones de DAX específicamente para los grupos de cálculo: 

[SELECTEDMEASURE](https://docs.microsoft.com/dax/selectedmeasure-function-dax) : se utilizan expresiones para los elementos de cálculo hacer referencia a la medida que se encuentra actualmente en el contexto. En este ejemplo, la medida Sales.

[SELECTEDMEASURENAME](https://docs.microsoft.com/dax/selectedmeasurename-function-dax) : se utilizan expresiones para los elementos de cálculo determinar la medida que se encuentra en el contexto por su nombre.

[ISSELECTEDMEASURE](https://docs.microsoft.com/dax/isselectedmeasure-function-dax) : se utilizan expresiones para los elementos de cálculo determinar la medida que se encuentra en el contexto se especifica en una lista de medidas.

[SELECTEDMEASUREFORMATSTRING](https://docs.microsoft.com/dax/selectedmeasurefromatstring-function-dax) : se utilizan expresiones para los elementos de cálculo recuperar la cadena de formato de la medida que se encuentra en el contexto.

### <a name="time-intelligence-example"></a>Ejemplo de inteligencia de tiempo

Nombre de la tabla - **inteligencia de tiempo**   
Nombre de columna - **cálculo de tiempo**   
Prioridad - **20**   

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

**PY QTD**

```dax
CALCULATE(
    SELECTEDMEASURE(),
    SAMEPERIODLASTYEAR(DimDate[Date]),
    'Time Intelligence'[Time Calculation] = "QTD"
)
```

**PY HASTA LA FECHA**

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

Para probar este grupo de cálculo, puede ejecutar una consulta de DAX en SSMS o abierto [Studio DAX](http://daxstudio.org/). YOY y YOY % se omiten en este ejemplo de consulta.

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

#### <a name="time-intelligence-query-return"></a>Devolver la consulta de inteligencia de tiempo

La tabla devuelta muestra los cálculos para cada cálculo elemento aplicado. Por ejemplo, puede ver que hasta la fecha de marzo de 2012 es la suma de enero, febrero y marzo de 2012.

![Valor devuelto de la consulta](media/calculation-groups/calc-groups-query-return.png)


## <a name="dynamic-format-strings"></a>Cadenas de formato dinámico

*Cadenas de formato dinámico* con cálculo de los grupos permiten aplicación condicional de cadenas de formato a las medidas sin obligarles a devolver las cadenas.

Los modelos tabulares admiten el formato dinámico de medidas mediante el uso de DAX [formato](https://docs.microsoft.com/dax/format-function-dax) función. Sin embargo, la función de formato tiene la desventaja de devolver una cadena, forzar las medidas que estarían numéricas que también se devuelven como una cadena. Esto puede tener algunas limitaciones, como no funciona con la mayoría de los objetos visuales de Power BI según valores numéricos, como los gráficos.

### <a name="dynamic-format-strings-for-time-intelligence"></a>Cadenas de formato dinámicas para la inteligencia de tiempo

Si observamos el ejemplo de inteligencia de tiempo mostrado anteriormente, el cálculo de todos los elementos excepto **YOY %** debe tener el formato de la medida actual en contexto. Por ejemplo, **YTD** calcula la medida Sales base debe ser moneda. Si se tratara de un grupo de cálculo para algo como una medida de base de pedidos, el formato sería numérico. **YOY %** , sin embargo, debe ser un porcentaje independientemente del formato de la medida base.

Para **YOY %** , es posible invalidar la cadena de formato estableciendo la propiedad de expresión de cadena de formato en **0,00%;-0.00%; 0,00%** . Para obtener más información acerca de las propiedades de expresión de cadena de formato, vea [propiedades de celdas MDX: contenido de la cadena de formato](../multidimensional-models/mdx/mdx-cell-properties-format-string-contents.md#numeric-values).

En este objeto visual de matriz en Power BI, verá **ventas actual/YOY** y **pedidos actual/YOY** conservar sus cadenas de formato de la medida base respectivo. **Ventas YOY %** y **ordena YOY %** , sin embargo, reemplaza la cadena de formato para usar *porcentaje* formato.

![Inteligencia de tiempo en el objeto visual de matriz](media/calculation-groups/calc-groups-dynamicstring-timeintel.png)

### <a name="dynamic-format-strings-for-currency-conversion"></a>Cadenas de formato dinámicas para la conversión de moneda

Las cadenas de formato dinámico proporcionan la conversión de moneda fácil. Tenga en cuenta el siguiente modelo de datos de Adventure Works. Se modela para *uno a varios* tal como se define mediante la conversión de moneda [tipos de conversión](../currency-conversions-analysis-services.md#conversion-types).

![Tipo de divisa en modelos tabulares](media/calculation-groups/calc-groups-currency-conversion.png)

Un **FormatString** columna se agrega a la **DimCurrency** de tabla y se rellena con cadenas de formato para las monedas correspondientes.

![Columna de cadena de formato](media/calculation-groups/calc-groups-formatstringcolumn.png)

En este ejemplo, el siguiente grupo de cálculo, a continuación, se define como:

### <a name="currency-conversion-example"></a>Ejemplo de conversión de moneda

Nombre de la tabla - **conversión de moneda**   
Nombre de columna - **cálculo de conversión**   
Prioridad - **5**   

#### <a name="calculation-items-for-currency-conversion"></a>Elementos de cálculo para la conversión de moneda

**Ninguna conversión**

```dax
SELECTEDMEASURE()
```

**Convertir moneda**

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
La expresión de cadena de formato debe devolver una cadena escalar. Usa el nuevo [SELECTEDMEASUREFORMATSTRING](https://docs.microsoft.com/dax/selectedmeasurefromatstring-function-dax) función Revertir a la cadena de formato de la medida base si hay varias monedas en contexto de filtro.

La siguiente animación muestra la conversión de moneda formato dinámico de la **ventas** medida en un informe.

![Cadena de formato dinámico de conversión de moneda aplicada](media/calculation-groups/calc-groups-dynamic-format-string.gif)

## <a name="precedence"></a>Prioridad

Prioridad es una propiedad definida para un grupo de cálculo. Especifica el orden de evaluación cuando hay más de un grupo de cálculo. Un número mayor indica mayor prioridad, lo que significa que se va a evaluar antes de los grupos de cálculo con una prioridad más baja.

Para este ejemplo, se deberá utilizar el mismo modelo que el anterior ejemplo de inteligencia de tiempo, pero también agregar una **promedios** grupo de cálculo. El grupo de cálculo de promedios contiene cálculos promedio que son independientes de inteligencia de tiempo tradicional en que no cambian el contexto de filtro de fecha, sino simplemente promedio cálculos dentro de él.

En este ejemplo, se define un cálculo de promedio diario. Cálculos como barriles promedio de aceite por día son comunes en aplicaciones de petróleo y gas. Otros ejemplos de negocio comunes incluyen promedio de ventas de tienda en el sector minorista.

Mientras que estos cálculos se calculan con independencia de los cálculos de inteligencia de tiempo, también puede ser un requisito para combinarlos. Por ejemplo, un usuario desee ver barriles aceite al día hasta la fecha para ver la tarifa diaria de petróleo desde el principio del año hasta la fecha actual. En este escenario, se debe establecer la prioridad para los elementos de cálculo.

### <a name="averages-example"></a>Ejemplo de promedios

Nombre de tabla es **promedios**.   
Nombre de columna es **calcular el promedio**.   
Es la prioridad **10**.   

#### <a name="calculation-items-for-averages"></a>Elementos de cálculo de promedios

**Ningún medio**

```dax
SELECTEDMEASURE()
```

**Promedio diario**

```dax
DIVIDE(SELECTEDMEASURE(), COUNTROWS(DimDate))
```

Este es un ejemplo de una consulta DAX y la tabla devuelta:

#### <a name="averages-query"></a>Consulta de promedios

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

#### <a name="averages-query-return"></a>Consulta de promedios devuelto

![Valor devuelto de la consulta](media/calculation-groups/calc-groups-ytd-daily-avg.png)

En la tabla siguiente se muestra cómo se calculan los valores de marzo de 2012.


|Nombre de columna  |Cálculo |
|---------|---------|
|YTD     |    Suma de ventas de enero, febrero, marzo de 2012<br />= 495,364 + 506,994 + 373,483     |
|Promedio diario    |     Ventas dividido por el número de días en marzo de 2012 de marzo<br />= 373,483 / 31       |
|Promedio diario hasta la fecha     | Hasta la fecha de marzo de 2012 dividido por el número de días en enero, febrero y marzo<br />=  1,375,841 / (31 + 29 + 31)       |

Esta es la definición del elemento de cálculo hasta la fecha, aplicada con la prioridad de **20**.

```dax
CALCULATE(SELECTEDMEASURE(), DATESYTD(DimDate[Date]))
```

Aquí es diario promedio, precedencia de **10**.

```dax
DIVIDE(SELECTEDMEASURE(), COUNTROWS(DimDate))
```

Puesto que la prioridad del grupo de cálculo de inteligencia de tiempo es mayor que el del grupo de cálculo promedios, se aplica como ampliamente como sea posible. El cálculo de media diaria de hasta la fecha aplica hasta la fecha para el numerador y el denominador (recuento de días) del cálculo de promedio diario.

Esto es equivalente a la siguiente expresión:

```dax
CALCULATE(DIVIDE(SELECTEDMEASURE(), COUNTROWS(DimDate)), DATESYTD(DimDate[Date]))
```

No esta expresión:

```dax
DIVIDE(CALCULATE(SELECTEDMEASURE(), DATESYTD(DimDate[Date])), COUNTROWS(DimDate)))
```

## <a name="sideways-recursion"></a>Recursividad hacia un lado

En el ejemplo de inteligencia de tiempo anterior, algunos de los elementos de cálculo hacen referencia a otros usuarios en el mismo grupo de cálculo. Esto se denomina *recursividad hacia*. Por ejemplo, **YOY %** hace referencia a ambos **YOY** y **PY**.

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

En este caso, ambas expresiones se evalúan por separado porque usan distintos calcular las instrucciones. No se admiten otros tipos de recursividad.

## <a name="single-calculation-item-in-filter-context"></a>Elemento de cálculo solo en el contexto de filtro

En nuestro ejemplo de inteligencia de tiempo, el **PY YTD** elemento de cálculo tiene un único calcular la expresión:

```dax
CALCULATE(
    SELECTEDMEASURE(),
    SAMEPERIODLASTYEAR(DimDate[Date]),
    'Time Intelligence'[Time Calculation] = "YTD"
)
```

El argumento hasta la fecha a la función CALCULATE() reemplaza el contexto de filtro para reutilizar la lógica ya definida en el elemento de cálculo hasta la fecha. No es posible aplicar PY y hasta la fecha en una evaluación única. Los grupos de cálculo son *solo aplicar* si es un elemento único cálculo desde el grupo de cálculo en el contexto de filtro.

## <a name="mdx-support"></a>Compatibilidad con MDX

Grupos de cálculo admiten consultas de datos MDX (expresiones multidimensionales). Esto significa, los usuarios de Microsoft Excel, los modelos de datos tabulares de consulta mediante MDX, puede aprovechar al máximo de grupos de cálculo en la hoja de cálculo de las tablas dinámicas y gráficos.

## <a name="tools"></a>Herramientas

Grupos de cálculo no se admiten todavía en Visual Studio con las extensiones de Analysis Services de SQL Server Data Tools. Sin embargo, se pueden crear grupos de cálculo mediante el uso de Tabular Model Scripting Language (TMSL) o el código abierto [Editor Tabular](https://github.com/otykier/TabularEditor).

## <a name="limitations"></a>Limitaciones

[Seguridad de nivel de objeto](object-level-security.md) (OLS) definido en el cálculo de las tablas de grupo no se admite. Sin embargo, se pueden definir OLS en otras tablas en el mismo modelo. Si un elemento de cálculo hace referencia a un objeto protegido OLS, se devuelve un error genérico.

[Seguridad de nivel de fila](roles-ssas-tabular.md#bkmk_rowfliters) (RLS) no se admite. Puede definir RLS en las tablas en el mismo modelo, pero no en los propios grupos de cálculo (directa o indirectamente).

[Expresiones de filas de detalle](../tutorial-tabular-1400/as-supplemental-lesson-detail-rows.md) no son compatibles con grupos de cálculo.

## <a name="see-also"></a>Vea también  

[DAX en modelos tabulares](understanding-dax-in-tabular-models-ssas-tabular.md)   
[Referencia de DAX](https://docs.microsoft.com/dax/data-analysis-expressions-dax-reference)  
