---
title: "Agregar cuadrículas de datos a informes para dispositivos móviles | Reporting Services | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.service: 
ms.component: mobile-reports
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fe98a970-90d3-44d1-9189-9141c237f141
caps.latest.revision: "4"
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 656c40ea8c8bc7d20fd2fe9de0a189f451731ae5
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2018
---
# <a name="add-data-grids-to-mobile-reports--reporting-services"></a>Agregar cuadrículas de datos a informes para dispositivos móviles | Reporting Services
A veces, la mejor forma de visualizar los datos es, simplemente, verlos. Obtenga más información sobre las tres *cuadrículas de datos*, o tablas, que existen para mostrar datos en el [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)]:
* Cuadrícula de datos simple
* Cuadrícula de datos del indicador
* Cuadrícula de datos del gráfico

## <a name="simple-data-grid"></a>Cuadrícula de datos simple
La cuadrícula de datos simple, que es el elemento más básico, puede mostrar varias columnas de datos con formato y encabezados personalizados. 

![mobile-report-simple-data-grid](../../reporting-services/mobile-reports/media/mobile-report-simple-data-grid.png)

Después de agregar una cuadrícula de datos a la superficie de diseño, se puede conectar a los datos reales.

1. Arrastre una cuadrícula de datos simple desde la pestaña **Diseño** a la cuadrícula de diseño y dele el tamaño que quiera.

2. Obtenga [datos de Excel o de un conjunto de datos compartido](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md).

3. Seleccione la pestaña **Datos** y, en el panel **Propiedades de los datos** , en **Datos para la vista de cuadrícula** , seleccione una tabla de datos.

4. En el panel **Columnas** , seleccione las columnas que quiera. Reordénelas, cámbielas de nombre y defina su formato y agregación. 

 
##  <a name="indicator-data-grid"></a>Cuadrícula de datos del indicador
Puede agregar columnas con medidores en una cuadrícula de datos del indicador.

![mobile-report-indicator-data-grid](../../reporting-services/mobile-reports/media/mobile-report-indicator-data-grid.png)

1. Arrastre una cuadrícula de datos del indicador desde la pestaña **Diseño** a la cuadrícula de diseño y dele el tamaño que quiera.

2. En la pestaña **Datos** , en el panel **Columnas** , seleccione **Agregar columna de medidor**. 

3. Seleccione **Opciones**y, luego, seleccione un **Tipo de indicador**. 

4. Establezca los campos **Valor** y **Comparación** y la **Dirección del valor**, exactamente a como lo haría con los [medidores que se agregan directamente a un informe para dispositivos móviles](../../reporting-services/mobile-reports/add-gauges-to-mobile-reports-reporting-services.md).

Automáticamente, la cuadrícula de datos incluirá en el medidor solo los datos específicos de esa fila de la cuadrícula de datos.  

## <a name="chart-data-grid"></a>Cuadrícula de datos del gráfico
Puede agregar columnas con medidores o con gráficos a una cuadrícula de datos del gráfico. 

![mobile-report-chart-data-grid](../../reporting-services/mobile-reports/media/mobile-report-chart-data-grid.png)

Cuando se agrega una columna de gráfico a una cuadrícula de datos, hay que agregar una tabla de datos aparte que proporcione datos relativos al gráfico en cada fila. Esta segunda tabla de datos debe compartir un campo con la tabla de datos principal para vincular cada fila a los datos de gráfico correspondientes. 

1. Arrastre una cuadrícula de datos del gráfico desde la pestaña **Diseño** a la cuadrícula de diseño y dele el tamaño que quiera.

2. En la pestaña **Datos** , en el panel **Columnas** , seleccione **Agregar columna de gráfico**. 

3. Obtenga [datos de Excel o de un conjunto de datos compartido](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md) para agregar una segunda tabla de datos que comparta un campo con la tabla de datos principal (si no lo ha hecho ya).

4. En **Propiedades de los datos**, seleccione la tabla de datos principal en **Datos para la vista de cuadrícula**y, luego, seleccione la segunda tabla en **Datos de referencia para visualizaciones de gráficos**.

5. Seleccione **Opciones**y, luego, seleccione un **Tipo de gráfico**.
 
6. Seleccione **Chart data field**(Campo de datos del gráfico), **Búsqueda de origen**y **Búsqueda de destino**. 
   Estas tres propiedades determinan el modo en el que la cuadrícula de datos proporciona datos a cada gráfico de la columna.
   
   *   **Búsqueda de origen** se establece en un campo en la tabla de datos de **Datos para la vista de cuadrícula**. Este campo actúa como un filtro por fila que se aplica a la tabla de datos de referencia del gráfico con el fin de proporcionar datos al gráfico incrustado para cada fila. 
   * **Búsqueda de destino** es el campo de la tabla de datos de **Datos de referencia para visualizaciones de gráficos**. Los datos del gráfico de cada fila se combinarán en esos dos campos.   
   * **Chart data field** (Campo de datos del gráfico) determina la métrica de la tabla de datos **Datos de referencia para visualizaciones de gráficos** que se usará como valor del eje y o como serie en el gráfico de cada fila.  

## <a name="see-also"></a>Vea también 
* [Mapas de informes móviles de Reporting Services](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)
* [Navegadores en informes para dispositivos móviles de Reporting Services](../../reporting-services/mobile-reports/add-navigators-to-reporting-services-mobile-reports.md)
* [Visualizaciones de informes para dispositivos móviles de Reporting Services](../../reporting-services/mobile-reports/add-visualizations-to-reporting-services-mobile-reports.md)
* [Medidores en informes para dispositivos móviles de Reporting Services](../../reporting-services/mobile-reports/add-gauges-to-mobile-reports-reporting-services.md)  
 
  
