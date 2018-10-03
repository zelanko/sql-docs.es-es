---
title: Agregar navegadores a informes móviles de Reporting Services
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: e141f50e-49a9-46c6-983c-f656013aa07c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 27060715a2d616dd99e294175163ad74b54a17b9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47740163"
---
# <a name="add-navigators-to-reporting-services-mobile-reports"></a>Add navigators to Reporting Services mobile reports
En el [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)], se agregan *navegadores* para filtrar los datos de las visualizaciones por tiempo o por selección. 

Los navegadores son similares a las segmentaciones en Power BI y las tablas dinámicas de Excel, pero también tienen algunos rasgos únicos.

Los**navegadores basados en tiempo** filtran las tablas mediante la selección de las filas que se encuentran en un intervalo de tiempo específico. 

Los**navegadores basados en selección** filtran las tablas mediante la selección de aquellas filas que contienen un valor de columna concreto que coincide con el valor de clave seleccionado o, en el caso de los árboles jerárquicos, aquellas filas en las que un valor de columna concreto pertenece al subárbol del valor de clave seleccionado. Hay dos tipos de navegadores de selección:
* Las listas de selección son tablas de una sola columna que se pueden usar para filtrar el informe móvil, similar a las segmentaciones en Power BI y Excel.
* Las cuadrículas de cuadro de mandos también filtran el informe móvil y pueden contener 
  
## <a name="time-navigators"></a>Navegadores de tiempo   
  
Como su nombre indica, el navegador de tiempo se usa para filtrar un intervalo de datos delimitado por un intervalo de tiempo.   
  
![SSMRP_TimeNav](../../reporting-services/mobile-reports/media/ssmrp-timenav.png)  
*Los cuatro gráficos de líneas de la izquierda se establecen en Valores preestablecidos del rango de tiempo. El gráfico de líneas de la derecha es el filtro.*  
  
Al ver el informe en vista previa o en el portal web de [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , puede arrastrar las flechas del navegador de tiempo para filtrar el resto del informe.  
  
![SSMRP_TimeNavPreview](../../reporting-services/mobile-reports/media/ssmrp-timenavpreview.png)  
  
De forma predeterminada, el navegador de tiempo filtra todos los elementos de visuales del informe que están conectados con datos basados en el tiempo. Si una tabla contiene más de una columna de tiempo, solo la primera se usa para filtrar. La tabla de la serie impulsa la visualización insertada y determina el intervalo de fechas general del informe móvil.  
  
Puede desconectar una visualización del navegador de tiempo.   
1. Seleccione la visualización y, después, seleccione la pestaña **Datos** .  
2. En **Propiedades de los datos**, seleccione **Opciones**.  
3. Desactive la casilla **Filtrado por** .  
  
   ![SSMRP_ClearTimeFilter](../../reporting-services/mobile-reports/media/ssmrp-cleartimefilter.png)  
  
## <a name="selection-lists"></a>Listas de selección   
  
La lista de selección filtra los datos de un informe móvil mediante la comparación del valor seleccionado en la lista con el valor de una columna especificada para cada fila de una tabla filtrada. 

1. Desde la pestaña **Diseño** , arrastre **Lista de selección** a la superficie de diseño y cambie el tamaño de la forma que quiera.

2. Seleccione la pestaña **Datos** y, en el panel **Propiedades de los datos** en **Claves**, seleccione la tabla y la columna que serán el filtro. 

3. En **Etiquetas**, seleccione la columna con la etiqueta que se mostrará. La columna de clave y la columna de etiqueta pueden ser la misma.  
  
   En el caso de datos jerárquicos de árbol, debe seleccionar una columna de clave principal.  
  
4. Una vez configuradas las propiedades de los datos, en **Tables Filtered by Selection List**(Tablas filtradas por lista de selección), seleccione las tablas que se van a filtrar y la columna por la que se va a filtrar. Esta columna debe comparar los valores con la columna de clave de la lista de selección. 

Para cada visualización del informe móvil en la que quiere que la lista de selección actúe como filtro:

1. Seleccione la visualización, seleccione la pestaña **Datos** y, en el panel **Propiedades de los datos** , seleccione **Opciones** junto al nombre del campo.

   ![mobile-report-set-selection-list](../../reporting-services/mobile-reports/media/mobile-report-set-selection-list.png)

2. En **Filtrado por**, seleccione la lista de selección.

Cuando se ve el informe móvil en vista previa o en el portal web de [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] y se selecciona un valor en la lista de selección, se filtran las demás visualizaciones del informe móvil.

![mobile-report-selection-list-filtering](../../reporting-services/mobile-reports/media/mobile-report-selection-list-filtering.png) 
     
## <a name="scorecard-grid"></a>Cuadrícula de cuadro de mandos  
  
El filtro de cuadrícula de cuadro de mandos funciona de manera muy similar al filtro de lista de selección, pero también muestra columnas de valor e indicadores de puntuación, que equivalen a los indicadores de una cuadrícula de datos del indicador. Después de seleccionar las columnas de clave, etiqueta y clave principal opcional, debe seleccionar una tabla de entrada y una columna para proporcionar el cuadro de mandos con datos. La columna de datos de cuadro de mandos debe poder filtrarse por la columna de clave.  

1. Desde la pestaña **Diseño** , arrastre **Cuadrícula de cuadro de mandos** a la superficie de diseño y cambie el tamaño de la forma que quiera.

2. Seleccione la pestaña **Datos** y, en el panel **Propiedades de los datos** en **Claves**, seleccione la tabla y la columna que serán el filtro. 

3. En **Etiquetas**, seleccione la columna con la etiqueta que se mostrará. La columna de clave y la columna de etiqueta pueden ser la misma.  
  
4. Para agregar un indicador de puntuación, seleccione **Agregar puntuación** en el panel **Columnas de datos**.   
  
5. Asigne un nombre al indicador de puntuación y seleccione **Opciones** para establecer las mismas propiedades que haya establecido para un indicador de una cuadrícula de datos:  
  
   * Tipo de medidor
   * Campo de valor
   * Campo de comparación
   * Dirección del valor
  
6. Para agregar un indicador de valor, seleccione **Agregar valor** en el panel **Columnas de datos**.

7. Póngale el nombre que desee al indicador, elija la columna de origen en la tabla y seleccione cómo se le dará formato.  

   ![mobile-report-scorecard-grid-data-properties](../../reporting-services/mobile-reports/media/mobile-report-scorecard-grid-data-properties.png)

8. Una vez configuradas las propiedades de los datos, en **Tables Filtered by Selection List**(Tablas filtradas por lista de selección), seleccione las tablas que se van a filtrar y la columna por la que se va a filtrar. Esta columna debe comparar los valores con la columna de clave de la lista de selección. 

Cuando se ve el informe móvil en vista previa o en el portal web de [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] y se selecciona un valor en la cuadrícula de cuadro de mandos, se filtran las demás visualizaciones del informe móvil.

![mobile-report-scorecard-grid](../../reporting-services/mobile-reports/media/mobile-report-scorecard-grid.png)
    
## <a name="set-which-visualizations-are-filtered"></a>Configurar qué visualizaciones se filtran  
  
Los elementos de la galería están configurados para usar filtros haciendo clic en el botón de opciones de una entrada concreta de la vista de datos. Los filtros se habilitan mediante la casilla correspondiente.  

Puede decidir qué visualizaciones del informe móvil filtrará un navegador:

1. Seleccione la visualización, seleccione la pestaña **Datos** y, en el panel **Propiedades de los datos** , seleccione **Opciones** junto al nombre del campo.

   ![mobile-report-set-selection-list](../../reporting-services/mobile-reports/media/mobile-report-set-selection-list.png)

2. En **Filtrado por**, seleccione el navegador. Cada visualización se puede filtrar mediante varios navegadores.
  
## <a name="cascading-filters"></a>Filtros en cascada   
  
Los filtros también pueden actuar en cascada para que el valor seleccionado de uno filtre los valores disponibles en un segundo. Para que los filtros actúen en cascada, aplíquelos a la columna de clave como lo haría con un elemento de galería regular.  

### <a name="see-also"></a>Vea también 
  
* [Mapas de informes móviles de Reporting Services](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)
* [Visualizaciones de informes para dispositivos móviles de Reporting Services](../../reporting-services/mobile-reports/add-visualizations-to-reporting-services-mobile-reports.md)
* [Agregar medidores a informes móviles | Reporting Services](../../reporting-services/mobile-reports/add-gauges-to-mobile-reports-reporting-services.md)
* [Agregar cuadrículas de datos a informes móviles | Reporting Services](../../reporting-services/mobile-reports/add-data-grids-to-mobile-reports-reporting-services.md)  
