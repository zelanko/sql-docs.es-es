---
title: Explorar datos (datos de SQL Server a los complementos de minería de datos) | Documentos de Microsoft
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
- data preparation
- histogram [data mining]
- data visualization
ms.assetid: 714845a9-4c27-461a-9ba3-149e1e818386
caps.latest.revision: 20
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: c648fba4cf47f117eb5dd04b76b5d7f0cb4f17c0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36109117"
---
# <a name="explore-data-sql-server-data-mining-add-ins"></a>Explorar datos (Complementos de minería de datos de SQL Server)
  ![Asistente para datos de explorar](media/dmc-explore.gif "Asistente para explorar datos")  
  
 El **explorar datos** asistente le ayudará a conocer el tipo y la cantidad de datos en la tabla de datos. El asistente representa de forma gráfica la distribución y los valores para las columnas seleccionadas, por columnas. Después, puede probar a cambiar la forma en que se agrupan los datos o copiar el gráfico que muestra el contenido en un libro de Excel para revisarlo.  
  
 Si los datos contienen datos numéricos continuos, puede alternar entre estas dos vistas:  
  
-   **Gráfico de líneas.** Este gráfico de líneas representa gráficamente los valores de datos en el eje X y el número de casos en el eje Y.  
  
-   **Gráfico de barras.** Este gráfico agrupa los valores por el número de casos correspondientes a cada valor.  
  
 Cuando el asistente encuentra grupos en los datos, usa la distribución real de los valores de datos. Por tanto, el gráfico de barras no muestra los valores numéricos según los típicos marcadores de eje numérico con números enteros como 10 o 100. En su lugar, los intervalos que se muestran en el gráfico de barras se asemejarían a valores como 43 521-55 603 (para la columna Income).  
  
 Si desea agrupar los datos en otros intervalos, debería hacerlo en Excel antes de analizar los datos. O bien, se pueden cambiar las etiquetas de los datos mediante el uso de la [cambiar etiquetas](relabel-sql-server-data-mining-add-ins.md) asistente.  
  
## <a name="using-the-explore-data-wizard"></a>Usar el Asistente para explorar datos  
  
1.  En el **minería de datos** la cinta de opciones, haga clic en **explorar datos**.  
  
2.  En el **Seleccionar origen** cuadro de diálogo, seleccione la tabla o el rango de celdas que contiene los datos.  
  
3.  En el **Seleccionar columna** diálogo cuadro, elija la columna que se va a analizar, a partir de los datos de ejemplo que se muestran en el panel.  
  
4.  En el **explorar datos** diálogo cuadro, elija los tipos de gráfico para mostrar la distribución de datos.  
  
5.  Si lo desea, puede agregar nuevas columnas a los datos, cambiar la manera en que se segmentan los datos o copiar el gráfico en Excel.  
  
### <a name="requirements"></a>Requisitos  
 Para usar el **explorar datos** asistente, los datos deben encontrarse en una tabla de datos de Excel.   
  
## <a name="see-also"></a>Vea también  
 [Lista de comprobación de preparación para la minería de datos](checklist-of-preparation-for-data-mining.md)  
  
  