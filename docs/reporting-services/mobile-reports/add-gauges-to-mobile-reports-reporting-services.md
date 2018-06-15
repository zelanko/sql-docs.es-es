---
title: Agregar medidores a informes para dispositivos móviles | Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: mobile-reports
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 76d8fc8f-c37f-44d3-ab44-45fbeed4e064
caps.latest.revision: 5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 985bde62deff88231ff889e1f403ad82edc55a0d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "33019422"
---
# <a name="add-gauges-to-mobile-reports--reporting-services"></a>Agregar medidores a informes para dispositivos móviles | Reporting Services
Los medidores son los elementos visuales más básicos y más ampliamente usados en los informes para dispositivos móviles. Muestran un valor único de un conjunto de datos: solo el valor, o bien el valor comparado con un objetivo.

![PBI_SSMRP_Gauges](../../reporting-services/mobile-reports/media/pbi-ssmrp-gauges.png)  
  
*Visualizaciones de medidores en la pestaña Diseño*  
  
Todos los medidores del Publicador de informes móviles de SQL Server tienen al menos una propiedad en común: un valor principal, establecido en un campo numérico de una de las tablas de datos del informe para dispositivos móviles.  

Todos los medidores, excepto el medidor de número, pueden mostrar también una comparación (o *valor diferencial*), esto es, la relación entre el valor principal y un valor de comparación. El valor de comparación suele ser el objetivo, mientras que el indicador es un indicador visual del progreso hacia ese objetivo, o el valor diferencial entre el valor real y el objetivo.

Los medidores solo pueden representar un valor agregado de su valor principal y un valor agregado de su valor de comparación. Las agregaciones de medidor son estándar: suma, promedio, mínimo, máximo, etc. El valor de medidor predeterminado es una suma, que muestra el total de todos los valores incluidos en los datos filtrados actuales disponibles para el control de medidor. 

Los valores de medidor se pueden filtrar conectándolos a navegadores en el informe para dispositivos móviles. 

## <a name="set-the-main-and-comparison-values-for-a-gauge"></a>Establecer los valores principal y de comparación de un medidor

1. Arrastre un medidor desde la pestaña **Diseño** a la cuadrícula de diseño y dele el tamaño que quiera.

2. Obtenga [datos de Excel o de un conjunto de datos compartido](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md).

3. Seleccione la pestaña **Datos** y, en el panel **Propiedades de los datos** , en **Valor principal** , seleccione una tabla de datos y un campo numérico.

3. En cualquier medidor (salvo el de número), en el panel **Propiedades de los datos** , en **Valor de comparación** , seleccione una tabla de datos y un campo numérico.

4. [Opcional] Para cambiar la agregación, seleccione **Opciones** y, luego, seleccione otra agregación.
   
   >**Nota:** si cambia la agregación del valor principal, probablemente también quiera hacer lo propio con el valor de comparación, aunque en algunos casos se pueden combinar diferentes métodos de agregación.  

## <a name="filter-a-gauge"></a>Filtrar un medidor
  
Si el informe para dispositivos móviles tiene navegadores, puede enlazar un medidor a uno o varios de ellos para filtrarlos. Puede enlazar el valor principal y el valor de comparación de un medidor a uno o más navegadores diferentes, dando lugar a opciones infinitas para los medidores.  

1. Seleccione un medidor y, en la pestaña **Datos** , en el panel **Propiedades de los datos** , seleccione **Opciones** junto a **Valor principal** o **Valor de comparación**.

2. En Filtrado por, seleccione el navegador en el que quiera filtrar el medidor.

   ![mobile-report-gauge-navigator](../../reporting-services/mobile-reports/media/mobile-report-gauge-navigator.png)
 
## <a name="set-visual-properties-for-a-gauge"></a>Establecer las propiedades visuales de un medidor
  
Además de las propiedades de datos que conectan elementos de medidor a campos de datos, hay también un número de propiedades funcionales y visuales que se pueden personalizar. 

### <a name="set-value-direction-high-or-low-is-better"></a>Establecer la dirección del valor: valores altos o bajos como mejor opción
* Seleccione un medidor y, en la pestaña **Diseño** , en el panel **Propiedades de los elementos visuales** , establezca **Dirección del valor** en **Los valores altos son mejores** o **Los valores bajos son mejores**. 

La opción**Los valores altos son mejores** pone los valores positivos de color verde, lo que indica un cambio positivo deseable, o los valores bajos de color rojo, lo que indica un cambio negativo no deseable. 

Los colores de **Los valores altos son mejores** se establecen a la inversa.

La propiedad de dirección del valor atañe únicamente a los elementos de medidor que admiten valores de comparación. El color del medidor viene determinado por el signo del entero diferencial y la configuración de la propiedad de dirección del valor.  
  
### <a name="set-range-stops-for-a-gauge"></a>Establecer las detenciones de rango de un medidor
La segunda propiedad específica del medidor que no es de datos es range stops (detenciones de rango). 

* Seleccione un medidor y, en la pestaña **Diseño** , en el panel **Propiedades de los elementos visuales** , seleccione **Detenciones de rango**.

Con las detenciones de rango se establece el porcentaje del valor de comparación en el que debe presentarse la visualización como dentro del objetivo (verde), neutral (ámbar) y fuera del objetivo (rojo), siendo el objetivo un valor de comparación del medidor. De nuevo, solo los medidores con valores de comparación admiten detenciones de rango.  

### <a name="format-the-numbers-in-the-gauge"></a>Dar formato a los números en el medidor  
Otra propiedad del elemento de medidor que no es de datos y una compartida por muchos otros elementos es number format (formato de número). 

* Seleccione un medidor y, en la pestaña **Diseño** , en el panel **Propiedades de los elementos visuales** , seleccione **Detenciones de rango**.

Determina el formato de los números que aparecen en el medidor (por ejemplo, moneda, porcentaje, hora o general). El formato de número se establece en cada elemento del informe para dispositivos móviles.
  
### <a name="see-also"></a>Vea también 

* [Creación y publicación de informes móviles con el Publicador de informes móviles de SQL Server](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)
* [Mapas en informes para dispositivos móviles de Reporting Services](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)
* [Navegadores en informes para dispositivos móviles de Reporting Services](../../reporting-services/mobile-reports/add-navigators-to-reporting-services-mobile-reports.md)
* [Visualizaciones de informes para dispositivos móviles de Reporting Services](../../reporting-services/mobile-reports/add-visualizations-to-reporting-services-mobile-reports.md)
* [Cuadrículas de datos en informes para dispositivos móviles de Reporting Services](../../reporting-services/mobile-reports/add-data-grids-to-mobile-reports-reporting-services.md) 
