---
title: Rellenar a partir de ejemplo (herramientas de análisis de tabla para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Table Analysis tools
- fill from example
ms.assetid: dac57d8f-1c65-4878-8ea0-9c680df5e4fb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d1e09e439469f23412c84ea7bab65c0aa748f286
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66081316"
---
# <a name="fill-from-example-table-analysis-tools-for-excel"></a>Rellenar desde ejemplo (Herramientas de análisis de tabla para Excel)
  ![Botón Rellenar desde ejemplo, Herramientas de análisis de tabla](media/tat-fillex.gif "Botón Rellenar desde ejemplo, Herramientas de análisis de tabla")  
  
 La herramienta **rellenar desde ejemplo** le ayuda a generar nuevas columnas de datos en función de los valores existentes.  
  
 Por ejemplo, suponga que los datos contienen una columna de importe de la **compra** , una columna de **cantidad de pedidos** y una columna de **cliente Premier** que se basa en alguna fórmula con las demás columnas. Si la columna de **cliente Premier** contiene muchas filas en blanco, podría usar las columnas **importe de compra** y **cantidad de pedidos** como entradas para deducir los valores que faltan. La herramienta analiza los patrones existentes en los datos junto con los ejemplos especificados y predice a qué categoría se debe asignar cada cliente.  
  
 Si no está satisfecho con los resultados, puede precisarlos proporcionando más ejemplos.  
  
## <a name="using-the-fill-from-example-tool"></a>Usar la herramienta Rellenar desde ejemplo  
  
1.  En la cinta de opciones **analizar** , haga clic en **rellenar desde ejemplo**.  
  
2.  La herramienta elegirá automáticamente la columna que va a rellenar basándose en el análisis de los datos, y el usuario podrá aceptar o invalidar esta sugerencia.  
  
3.  Cree una columna para los nuevos datos y escriba ejemplos de los datos que desea predecir. Asegúrese de que existe al menos un ejemplo para cada valor que desea predecir. Si está rellenando datos en una columna existente, seleccione la columna a la que le faltan valores.  
  
4.  Opcionalmente, haga clic en **elegir las columnas que se van a usar en el análisis**. En el cuadro de diálogo **selección avanzada de columnas** , especifique las columnas que es más probable que sean útiles al rellenar los datos que faltan.  
  
     Por ejemplo, si sabe por experiencia que existe un efecto causal entre una columna y la columna con valores ausentes, puede anular la selección de otras columnas para obtener mejores resultados.  
  
     Haga clic en **OK**.  
  
5.  Haga clic en **Ejecutar**.  
  
     Una vez completado el análisis, la herramienta crea una nueva hoja de cálculo de **modelos** que contiene los resultados del análisis. El informe enumera las reglas o influenciadores clave que se encontraron y muestra la probabilidad para cada regla.  
  
     Asimismo, la herramienta agrega automáticamente una columna con los nuevos valores a la tabla de datos original. Puede revisar los valores y compararlos con el original.  
  
### <a name="requirements"></a>Requisitos  
 Sólo puede trabajar con datos en columnas. Si la serie que desea rellenar está almacenada en una fila, puede usar la función Pegar, Transponer de Excel para cambiar los datos a un formato de columna.  
  
## <a name="understanding-the-pattern-report"></a>Descripción del informe de patrones  
 Al ejecutar la herramienta **rellenar desde ejemplo** , se crea un informe que proporciona más información sobre los patrones detectados. Estos patrones se usan para extrapolar nuevos valores de datos.  
  
 El informe de patrones muestra los influenciadores clave de cada valor que se predijo. Cada influenciador o regla se describe como una combinación de una columna, el valor de la misma y el impacto relativo de la regla en la predicción.  
  
 Por ejemplo, si intentaba rellenar una hoja de cálculo que mostraba la distancia en el envío de pedidos, lógicamente podría esperar que el destino tuviera un fuerte impacto en el valor de la distancia en el envío. En este caso, el informe contendría la siguiente fila:  
  
|Columna|Value|Favorece|Impacto relativo|  
|------------|-----------|------------|---------------------|  
|StateProvinceCode|AB|>500 kilómetros|80 %|  
  
 Esto significa que el valor AB de la columna **StateProvinceCode** predice fuertemente una distancia de envío de >500 kilómetros.  
  
 Normalmente, las predicciones se basan en patrones que son mucho más complejos que este ejemplo y el informe puede contener muchas filas de reglas para cada predicción. El efecto de todas las reglas se combina para obtener el valor de predicción.  
  
> [!NOTE]  
>  El **impacto relativo** se muestra como una barra sombreada. Cuanto más larga es la barra, mayor es la probabilidad de que esa regla sirva para predecir el valor rellenado.  
  
 La herramienta también agrega una nueva columna a la tabla de datos original, \<con el nombre de columna> Extended.  
  
 Si la columna de datos original contenía un valor, éste se copia en la nueva columna. Sin embargo, si la columna original contenía una celda en blanco, la nueva columna contendrá el valor predicho por el asistente.  
  
## <a name="related-tools-and-information"></a>Información y herramientas relacionadas  
 También puede usar el Asistente para [explorar datos](explore-data-sql-server-data-mining-add-ins.md) , disponible en el cliente de minería de datos para Excel, para examinar la distribución de valores en una columna de Excel. Para obtener más información, vea [explorar y limpiar datos](exploring-and-cleaning-data.md).  
  
## <a name="see-also"></a>Consulte también  
 [Herramientas de análisis de tabla para Excel](table-analysis-tools-for-excel.md)  
  
  
