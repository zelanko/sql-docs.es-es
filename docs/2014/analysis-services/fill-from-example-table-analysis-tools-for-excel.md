---
title: Rellenar desde ejemplo (herramientas de análisis de tabla para Excel) | Documentos de Microsoft
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Table Analysis tools
- fill from example
ms.assetid: dac57d8f-1c65-4878-8ea0-9c680df5e4fb
caps.latest.revision: 20
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 56c92cd4cdc4cf3306ce0877f3e046c626e6f883
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36204290"
---
# <a name="fill-from-example-table-analysis-tools-for-excel"></a>Rellenar desde ejemplo (Herramientas de análisis de tabla para Excel)
  ![Botón rellenar desde ejemplo de herramientas de análisis de tabla](media/tat-fillex.gif "botón rellenar desde ejemplo de herramientas de análisis de tabla")  
  
 El **rellenar desde ejemplo** herramienta le ayuda a crear nuevas columnas de datos en función de los valores existentes.  
  
 Por ejemplo, suponga que los datos contienen una **cantidad de compra** columna, una **cantidad de pedidos** columna y un **cliente preferente** columna que se basa en algunas fórmulas utilizando el otras columnas. Si el **cliente preferente** columna contiene muchas filas en blanco, podría utilizar el **cantidad de compra** y **cantidad de pedidos** columnas como entradas para deducir los valores que faltan. La herramienta analiza los patrones existentes en los datos junto con los ejemplos especificados y predice a qué categoría se debe asignar cada cliente.  
  
 Si no está satisfecho con los resultados, puede precisarlos proporcionando más ejemplos.  
  
## <a name="using-the-fill-from-example-tool"></a>Usar la herramienta Rellenar desde ejemplo  
  
1.  En el **analizar** la cinta de opciones, haga clic en **rellenar desde ejemplo**.  
  
2.  La herramienta elegirá automáticamente la columna que va a rellenar basándose en el análisis de los datos, y el usuario podrá aceptar o invalidar esta sugerencia.  
  
3.  Cree una columna para los nuevos datos y escriba ejemplos de los datos que desea predecir. Asegúrese de que existe al menos un ejemplo para cada valor que desea predecir. Si está rellenando datos en una columna existente, seleccione la columna a la que le faltan valores.  
  
4.  Si lo desea, haga clic en **elegir las columnas que se usará en el análisis**. En el **selección avanzada de columnas** cuadro de diálogo, especifique las columnas que tienen más probabilidades de ser útiles al rellenar los datos que faltan.  
  
     Por ejemplo, si sabe por experiencia que existe un efecto causal entre una columna y la columna con valores ausentes, puede anular la selección de otras columnas para obtener mejores resultados.  
  
     Haga clic en **Aceptar**.  
  
5.  Haga clic en **Ejecutar**.  
  
     Una vez completado análisis, la herramienta crea un nuevo **patrones** hoja de cálculo que contiene los resultados del análisis. El informe enumera las reglas o influenciadores clave que se encontraron y muestra la probabilidad para cada regla.  
  
     Asimismo, la herramienta agrega automáticamente una columna con los nuevos valores a la tabla de datos original. Puede revisar los valores y compararlos con el original.  
  
### <a name="requirements"></a>Requisitos  
 Sólo puede trabajar con datos en columnas. Si la serie que desea rellenar está almacenada en una fila, puede usar la función Pegar, Transponer de Excel para cambiar los datos a un formato de columna.  
  
## <a name="understanding-the-pattern-report"></a>Descripción del informe de patrones  
 Al ejecutar el **rellenar desde ejemplo** herramienta, se crea un informe que proporciona más información sobre los patrones que se detectaron. Estos patrones se usan para extrapolar nuevos valores de datos.  
  
 El informe de patrones muestra los influenciadores clave de cada valor que se predijo. Cada influenciador o regla se describe como una combinación de una columna, el valor de la misma y el impacto relativo de la regla en la predicción.  
  
 Por ejemplo, si intentaba rellenar una hoja de cálculo que mostraba la distancia en el envío de pedidos, lógicamente podría esperar que el destino tuviera un fuerte impacto en el valor de la distancia en el envío. En este caso, el informe contendría la siguiente fila:  
  
|columna|Valor|Favorece|Impacto relativo|  
|------------|-----------|------------|---------------------|  
|StateProvinceCode|AB|>500 kilómetros|80%|  
  
 Esto significa que el valor AB de la **StateProvinceCode** columna fuertemente predice una distancia de envío de > 500 kilómetros.  
  
 Normalmente, las predicciones se basan en patrones que son mucho más complejos que este ejemplo y el informe puede contener muchas filas de reglas para cada predicción. El efecto de todas las reglas se combina para obtener el valor de predicción.  
  
> [!NOTE]  
>  **Impacto relativo** se muestra como una barra sombreada. Cuanto más larga es la barra, mayor es la probabilidad de que esa regla sirva para predecir el valor rellenado.  
  
 La herramienta también agrega una nueva columna a la tabla de datos original, denominada \<nombre de columna > extendido.  
  
 Si la columna de datos original contenía un valor, éste se copia en la nueva columna. Sin embargo, si la columna original contenía una celda en blanco, la nueva columna contendrá el valor predicho por el asistente.  
  
## <a name="related-tools-and-information"></a>Información y herramientas relacionadas  
 También puede usar el [explorar datos](explore-data-sql-server-data-mining-add-ins.md) asistente, disponible en el cliente de minería de datos para Excel, para examinar la distribución de valores en una columna de Excel. Para obtener más información, consulte [explorador y limpieza de datos](exploring-and-cleaning-data.md).  
  
## <a name="see-also"></a>Vea también  
 [Herramientas de análisis de tabla para Excel](table-analysis-tools-for-excel.md)  
  
  