---
title: Documentar modelos de minería de datos (datos de complementos de minería de datos para Excel) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- documenting models
- mining structures, managing
- mining models, managing
- model properties
ms.assetid: 0a663e11-e40c-4708-ad18-fabb6c976fa4
caps.latest.revision: 18
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: a093deb3764c154ae45596ad64d2805aa6d00d88
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36110849"
---
# <a name="documenting-mining-models-data-mining-add-ins-for-excel"></a>Documentar modelos de minería de datos (Complementos de minería de datos para Excel)
  ![Botón de modelo de documento, cinta de opciones de minería de datos](media/dmc-docmodel.gif "botón documentar modelo, cinta de opciones de minería de datos")  
  
 El **documento modelo** asistente crea un informe que proporciona información útil acerca de los modelos de minería de datos que ha creado. Si documenta un modelo, podrá realizar un seguimiento de los datos usados para generarlo, obtener información adicional sobre el momento en que se procesó y realizar un seguimiento de los cambios en los parámetros que afectan a los resultados del mismo.  
  
## <a name="using-the-document-model-wizard"></a>Usar el asistente para Documentar modelo  
  
1.  Haga clic en el **minería de datos** ficha.  
  
2.  En el **uso del modelo** grupo, haga clic en **documento modelo**.  
  
3.  En el **Seleccionar modelo** cuadro de diálogo, seleccione el modelo en el que al informe y, a continuación, haga clic en **siguiente**. Debe ejecutar el **documento modelo** asistente por separado para cada modelo que desee en un documento.  
  
4.  En el **seleccionar detalles de la documentación** diálogo cuadro, elija una de estas dos opciones: **información completa** o **información de resumen**.  
  
5.  Haga clic en **Finalizar**.  
  
6.  El asistente crea automáticamente una nueva hoja de cálculo que contiene el informe especificado, denominado **documentación del modelo de**,  
  
## <a name="understanding-the-report"></a>Descripción del informe  
 En el momento de crear un informe para documentar un modelo de minería de datos, puede optar por crear un resumen, que contiene información básica como el nombre y la descripción del modelo, o un informe completo, que contiene detalles sobre la estructura subyacente e información avanzada sobre el modelo de minería de datos.  
  
 Dependiendo del algoritmo usado para crear el modelo, se proporcionan tipos de información diferentes. Por ejemplo, en un modelo de asociación, estará más interesado en conocer el número de conjuntos de elementos y reglas que se han generado. Para un modelo de agrupación en clústeres, el número de clústeres es más interesante.  
  
 En la tabla siguiente aparecen las opciones y la información que se proporciona en el informe para cada opción.  
  
> [!NOTE]  
>  De forma predeterminada, las columnas del informe tienen un tamaño determinado. Por tanto, si algún nombre de columna o valor es muy largo, podría no estar visible o podría aparecer como ### en Excel. Para que hacer que los valores estén visibles, puede cambiar el tamaño de la fila. Si la celda está seleccionada, puede hacer clic y arrastrar las flechas dobles situadas en el extremo derecho de la barra de fórmulas para mostrar la cadena o el valor completo.  
  
### <a name="summary-report"></a>Informe de resumen  
  
||||  
|-|-|-|  
|**Metadatos**|Nombre del modelo<br /><br /> Descripción del modelo<br /><br /> Nombre del algoritmo<br /><br /> Fecha del último procesamiento||  
|**Resultados del modelo**|Asociación|Número de conjuntos de elementos<br /><br /> Número de reglas|  
||Agrupación en clústeres|Número de clústeres<br /><br /> Compatibilidad con el clúster|  
||Árbol de decisión|Número de árboles<br /><br /> Número de nodos en cada árbol|  
||Regresión lineal|Número de árboles (siempre 1)<br /><br /> Número de nodos (siempre 1)|  
||naive Bayes|Atributos importantes|  
||Red neuronal|Número de nodos de entrada<br /><br /> Número de nodos de salida<br /><br /> Número de nodos ocultos|  
||Agrupación en clústeres de secuencia|Número de clústeres|  
  
### <a name="complete-report"></a>Informe completo  
 El informe completo contiene todo lo que está en el informe de resumen además de información detallada sobre las columnas de datos usadas en el modelo y los resultados del análisis:  
  
||||  
|-|-|-|  
|**Metadatos**|Metadatos del modelo|Parámetros de algoritmo y valores|  
||Metadatos de columna|Nombre de columna<br /><br /> Uso<br /><br /> Tipo de datos<br /><br /> Tipo de contenido<br /><br /> Valores (lista de valores discretos o rango de valores)|  
|**Estadísticas del modelo**|Columnas continuas|Valor promedio<br /><br /> Valor mínimo<br /><br /> Valor máximo<br /><br /> Error cuadrático medio<br /><br /> Desviación media<br /><br /> Logaritmo<br /><br /> Fórmula de regresión (solo para modelos de regresión lineal)|  
||Columnas discretas [DMX]|Número sin errores<br /><br /> Número con errores<br /><br /> Logaritmo<br /><br /> Mejora respecto al modelo predictivo|  
  
> [!NOTE]  
>  Puede documentar cualquier tipo de modelo compatible con SQL Server Analysis Services. Por consiguiente, la tabla contiene algunos tipos de modelos que no se pueden crear con las Herramientas de análisis de tabla ni con los asistentes del Cliente de minería de datos. Sin embargo, puede crear todos los tipos de modelo mediante el **Editor de consultas avanzadas de minería de datos**. Para obtener más información, consulte [consulta &#40;complementos de minería de datos de SQL Server&#41;](query-sql-server-data-mining-add-ins.md).  
  
## <a name="see-also"></a>Vea también  
 [Implementar y ampliar modelos de minería de datos &#40;datos complementos de minería de datos para Excel&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)  
  
  