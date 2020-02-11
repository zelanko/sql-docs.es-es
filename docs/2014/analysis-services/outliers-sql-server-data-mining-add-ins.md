---
title: Valores atípicos (SQL Server complementos de minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- exceptions [data mining]
- data preparation
- outliers [data mining]
- data cleaning
ms.assetid: e6fa7c62-4005-4792-9211-3b699377a517
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3043c8f63433396f059f5c456512ad4ba2bffd93
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66072135"
---
# <a name="outliers-sql-server-data-mining-add-ins"></a>Valores atípicos (Complementos de minería de datos de SQL Server)
  ![Asistente para quitar valores atípicos, cinta de opciones Minería de datos](media/dmc-outliers.gif "Asistente para quitar valores atípicos, cinta de opciones Minería de datos")  
  
 Un valor *atípico* significa un valor de datos que es problemático por cualquiera de los siguientes motivos:  
  
-   El valor está fuera del intervalo esperado.  
  
-   Es posible que los datos se hayan especificado de forma incorrecta.  
  
-   El valor es un valor ausente.  
  
-   Los datos consisten en un espacio u otra cadena de tipo NULL.  
  
-   El valor es preciso pero está tan alejado de la distribución que puede afectar significativamente al modelo.  
  
 El Cliente de minería de datos para Excel le ayuda a detectar estos datos y a actualizar los valores o a suprimirlos. Por ejemplo, puede reemplazar los valores atípicos por una media aritmética o puede eliminar las filas que sean susceptibles de contener valores erróneos.  
  
## <a name="handling-outliers"></a>Tratar los valores atípicos  
 El Asistente para **quitar valores atípicos** ofrece varias herramientas para administrar los valores atípicos de forma adecuada:  
  
-   Primero, puede explorar los datos para entender mejor la distribución de los valores y la relación de los valores atípicos con los otros datos.  
  
     Por ejemplo, puede usar la tarea **explorar datos** para revisar y corregir los valores. El Asistente para **quitar valores atípicos** también muestra un gráfico, ya sea un gráfico de líneas o de barras, para ayudarle a entender la distribución de todos los valores.  
  
-   A continuación, puede usar el asistente **valores atípicos** para quitar o cambiar valores atípicos. El método que use dependerá de si los valores son discretos o continuos.  
  
     El asistente muestra los valores discretos en un gráfico de barras, donde cada barra representa un valor concreto y el alto de la barra indica el número de casos para cada valor. Deslizando el control de umbral en el gráfico, puede cortar barras que representen grupos de valores extremos o potencialmente erróneos.  
  
-   El asistente muestra los valores continuos en un gráfico de barras o en un gráfico de líneas. En el gráfico de líneas, el valor está representado en el eje X y el recuento de los valores en el eje Y.  
  
     Puede controlar si desea quitar o mantener los valores de los extremos inferior y superior del gráfico cambiando los valores **mínimo** y **máximo** , o deslizando las barras. Cuando se cambia la configuración de valor mínimo y máximo, los datos que se van a eliminar se muestran con un sombreado en el gráfico.  
  
 Una vez seleccionados los valores atípicos con los que va a trabajar, debe indicar al asistente cómo tiene que tratar dichos valores. Puede eliminar las filas que contienen los valores atípicos o puede especificar un valor de reemplazo, como un valor promedio, un valor NULL u otro valor de su elección.  
  
 Finalmente, el asistente le da algunas opciones para mostrar los nuevos datos. Puede reemplazar los datos originales por valores nuevos, agregar a la tabla una nueva columna que contenga los nuevos valores, o crear una nueva hoja de cálculo que contenga los datos actualizados.  
  
### <a name="using-the-outlier-wizard"></a>Usar el Asistente para quitar valores atípicos  
  
1.  En la cinta de opciones **minería de datos** , haga clic en **limpiar datos**y seleccione **valores atípicos**.  
  
2.  En el cuadro de diálogo **seleccionar datos de origen** , seleccione una tabla de datos de Excel o un rango de celdas y haga clic en **siguiente**.  
  
    > [!WARNING]  
    >  No puede usar el asistente **valores atípicos** en datos externos, a menos que lo copie primero en Excel.  
  
3.  En el cuadro de diálogo **Seleccionar columna** , seleccione una **sola** columna.  
  
     Haga clic en **Next**.  
  
4.  En el cuadro de diálogo **especificar umbrales** , revise la distribución de los datos.  
  
    -   Si la columna contiene valores discretos, el asistente muestra un histograma que contiene el recuento para cada valor discreto.  
  
         Suponiendo que los valores atípicos son valores raros, puede filtrarlos cambiando el valor **mínimo** .  
  
    -   Si la columna contiene datos numéricos, puede hacer clic en el botón **ver como discreto** o en el botón **ver como numérico** para alternar entre ver los valores en un gráfico de barras o en un gráfico de líneas.  
  
5.  En el cuadro de diálogo **especificar umbrales** , elija el intervalo de datos que desea mantener escribiendo un valor mínimo y máximo, o arrastrando las barras deslizantes. Haga clic en **Next**.  
  
6.  En el cuadro de diálogo **control de valores atípicos** , especifique si desea eliminar o reemplazar los valores y haga clic en **siguiente**.  
  
7.  En el cuadro de diálogo **Seleccionar destino** , especifique dónde desea que se guarden los nuevos datos.  
  
### <a name="related-options"></a>Opciones relacionadas  
 El asistente proporciona estas opciones:  
  
|**Opciones**|**Comentario**|  
|-----------------|-----------------|  
|**Seleccionar columna**|Solo se puede trabajar con una columna cada vez.|  
|**Especificar el tratamiento de los umbrales**|Establezca un umbral usando **mínimo** para excluir los valores que se encuentran en menos filas que el valor de umbral.<br /><br /> Inicialmente, el valor **mínimo** es igual al valor con el menor número de filas y no se puede hacer que el mínimo sea menor que ese valor.|  
|**Tratamiento de valores atípicos**|Si decide eliminar los valores atípicos, puede o cambiar los datos de la hoja de cálculo actual o bien crear una copia de los datos en una nueva hoja de cálculo.|  
  
## <a name="see-also"></a>Consulte también  
 [Explorar datos &#40;SQL Server complementos de minería de datos&#41;](explore-data-sql-server-data-mining-add-ins.md)  
  
  
