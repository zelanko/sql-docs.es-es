---
title: Explorar datos (complementos de minería de datos de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data preparation
- histogram [data mining]
- data visualization
ms.assetid: 714845a9-4c27-461a-9ba3-149e1e818386
author: minewiskan
ms.author: owend
ms.openlocfilehash: 4a20484a85b459dad58e5e6687a6cc34a093b130
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/08/2020
ms.locfileid: "84528361"
---
# <a name="explore-data-sql-server-data-mining-add-ins"></a>Explorar datos (Complementos de minería de datos de SQL Server)
  ![Asistente para explorar datos](media/dmc-explore.gif "Asistente para explorar datos")  
  
 El Asistente para **explorar datos** le ayuda a comprender el tipo y la cantidad de datos de la tabla de datos. El asistente representa de forma gráfica la distribución y los valores para las columnas seleccionadas, por columnas. Después, puede probar a cambiar la forma en que se agrupan los datos o copiar el gráfico que muestra el contenido en un libro de Excel para revisarlo.  
  
 Si los datos contienen datos numéricos continuos, puede alternar entre estas dos vistas:  
  
-   **Gráfico de líneas.** Este gráfico de líneas representa gráficamente los valores de datos en el eje X y el número de casos en el eje Y.  
  
-   **Gráfico de barras.** Este gráfico agrupa los valores por el número de casos correspondientes a cada valor.  
  
 Cuando el asistente encuentra grupos en los datos, usa la distribución real de los valores de datos. Por tanto, el gráfico de barras no muestra los valores numéricos según los típicos marcadores de eje numérico con números enteros como 10 o 100. En su lugar, los intervalos que se muestran en el gráfico de barras se asemejarían a valores como 43 521-55 603 (para la columna Income).  
  
 Si desea agrupar los datos en otros intervalos, debería hacerlo en Excel antes de analizar los datos. O bien, puede cambiar la etiqueta de los datos mediante el Asistente para cambiar [etiquetas](relabel-sql-server-data-mining-add-ins.md) .  
  
## <a name="using-the-explore-data-wizard"></a>Usar el Asistente para explorar datos  
  
1.  En la cinta de opciones **minería de datos** , haga clic en **explorar datos**.  
  
2.  En el cuadro de diálogo **Seleccionar origen** , seleccione la tabla o el rango de celdas que contiene los datos.  
  
3.  En el cuadro de diálogo **Seleccionar columna** , elija la columna que se va a analizar, en los datos de ejemplo que se muestran en el panel.  
  
4.  En el cuadro de diálogo **explorar datos** , elija los tipos de gráficos para mostrar la distribución de los datos.  
  
5.  Si lo desea, puede agregar nuevas columnas a los datos, cambiar la manera en que se segmentan los datos o copiar el gráfico en Excel.  
  
### <a name="requirements"></a>Requisitos  
 Para usar el Asistente para **explorar datos** , los datos deben estar en una tabla de datos de Excel.   
  
## <a name="see-also"></a>Consulte también  
 [Lista de comprobación de la preparación para la minería de datos](checklist-of-preparation-for-data-mining.md)  
  
  
