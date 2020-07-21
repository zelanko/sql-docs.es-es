---
title: Documentar modelos de minería de datos (complementos de minería de datos para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- documenting models
- mining structures, managing
- mining models, managing
- model properties
ms.assetid: 0a663e11-e40c-4708-ad18-fabb6c976fa4
author: minewiskan
ms.author: owend
ms.openlocfilehash: 92ed5c43fa2b7484485b915d42946121487386d9
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/08/2020
ms.locfileid: "84528491"
---
# <a name="documenting-mining-models-data-mining-add-ins-for-excel"></a>Documentar modelos de minería de datos (Complementos de minería de datos para Excel)
  ![Botón Documentar modelo, cinta de opciones Minería de datos](media/dmc-docmodel.gif "Botón Documentar modelo, cinta de opciones Minería de datos")  
  
 El Asistente para **documentar modelo** crea un informe que proporciona información útil sobre los modelos de minería de datos que ha creado. Si documenta un modelo, podrá realizar un seguimiento de los datos usados para generarlo, obtener información adicional sobre el momento en que se procesó y realizar un seguimiento de los cambios en los parámetros que afectan a los resultados del mismo.  
  
## <a name="using-the-document-model-wizard"></a>Usar el asistente para Documentar modelo  
  
1.  Haga clic en la pestaña **minería de datos** .  
  
2.  En el grupo **uso del modelo** , haga clic en modelo de **documento**.  
  
3.  En el cuadro de diálogo **Seleccionar modelo** , seleccione el modelo en el que desea generar el informe y, a continuación, haga clic en **siguiente**. Debe ejecutar el Asistente para **documentar modelo** por separado para cada modelo que desee documentar.  
  
4.  En el cuadro de diálogo **seleccionar detalles** de la documentación, elija una de estas dos opciones: **información completa** o **información de Resumen**.  
  
5.  Haga clic en **Finalizar**  
  
6.  El asistente crea automáticamente una nueva hoja de cálculo que contiene el informe especificado, titulado **documentación del modelo**,  
  
## <a name="understanding-the-report"></a>Descripción del informe  
 En el momento de crear un informe para documentar un modelo de minería de datos, puede optar por crear un resumen, que contiene información básica como el nombre y la descripción del modelo, o un informe completo, que contiene detalles sobre la estructura subyacente e información avanzada sobre el modelo de minería de datos.  
  
 Dependiendo del algoritmo usado para crear el modelo, se proporcionan tipos de información diferentes. Por ejemplo, en un modelo de asociación, estará más interesado en conocer el número de conjuntos de elementos y reglas que se han generado. Para un modelo de agrupación en clústeres, el número de clústeres es más interesante.  
  
 En la tabla siguiente aparecen las opciones y la información que se proporciona en el informe para cada opción.  
  
> [!NOTE]  
>  De forma predeterminada, las columnas del informe tienen un tamaño determinado. Por tanto, si algún nombre de columna o valor es muy largo, podría no estar visible o podría aparecer como ### en Excel. Para que hacer que los valores estén visibles, puede cambiar el tamaño de la fila. Si la celda está seleccionada, puede hacer clic y arrastrar las flechas dobles situadas en el extremo derecho de la barra de fórmulas para mostrar la cadena o el valor completo.  
  
### <a name="summary-report"></a>Informe de resumen  
  
||||  
|-|-|-|  
|**Metadata**|Nombre del modelo<br /><br /> Descripción del modelo<br /><br /> Nombre del algoritmo<br /><br /> Fecha del último procesamiento||  
|**Resultados del modelo**|Asociación|Número de conjuntos de elementos<br /><br /> Número de reglas|  
||Agrupación en clústeres|Número de clústeres<br /><br /> Compatibilidad con el clúster|  
||Árbol de decisión|Número de árboles<br /><br /> Número de nodos en cada árbol|  
||Regresión lineal|Número de árboles (siempre 1)<br /><br /> Número de nodos (siempre 1)|  
||Bayes Naive|Atributos importantes|  
||Red neuronal|Número de nodos de entrada<br /><br /> Número de nodos de salida<br /><br /> Número de nodos ocultos|  
||Agrupación en clústeres de secuencia|Número de clústeres|  
  
### <a name="complete-report"></a>Informe completo  
 El informe completo contiene todo lo que está en el informe de resumen además de información detallada sobre las columnas de datos usadas en el modelo y los resultados del análisis:  
  
||||  
|-|-|-|  
|**Metadata**|Metadatos del modelo|Parámetros de algoritmo y valores|  
||Metadatos de columna|Nombre de la columna<br /><br /> Uso<br /><br /> Tipo de datos<br /><br /> Tipo de contenido<br /><br /> Valores (lista de valores discretos o rango de valores)|  
|**Estadísticas del modelo**|Columnas continuas|Valor medio<br /><br /> Valor mínimo<br /><br /> Valor máximo<br /><br /> Error cuadrático medio<br /><br /> Desviación media<br /><br /> Logaritmo<br /><br /> Fórmula de regresión (solo para modelos de regresión lineal)|  
||Columnas discretas [DMX]|Número sin errores<br /><br /> Número con errores<br /><br /> Logaritmo<br /><br /> Mejora respecto al modelo predictivo|  
  
> [!NOTE]  
>  Puede documentar cualquier tipo de modelo compatible con SQL Server Analysis Services. Por consiguiente, la tabla contiene algunos tipos de modelos que no se pueden crear con las Herramientas de análisis de tabla ni con los asistentes del Cliente de minería de datos. Sin embargo, puede crear todos los tipos de modelos mediante el **Editor de consultas avanzadas de minería de datos**. Para obtener más información, vea [&#40;de consultas SQL Server complementos de minería de datos&#41;](query-sql-server-data-mining-add-ins.md).  
  
## <a name="see-also"></a>Consulte también  
 [Implementar y escalar modelos de minería de datos &#40;complementos de minería de datos para Excel&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)  
  
  
