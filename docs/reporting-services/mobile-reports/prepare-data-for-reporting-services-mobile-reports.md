---
title: Preparar datos para informes móviles de Reporting Services | Microsoft Docs
ms.date: 02/08/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: 8adce9ad-6a08-4d20-b1cf-d3c45544d8de
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 9ded496c3509420d54325dc054e018048ede0732
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62499930"
---
# <a name="prepare-data-for-reporting-services-mobile-reports"></a>Preparar datos para informes de Reporting Services móviles
  
[!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-long.md)] admite un número de operaciones de datos complejas, como el filtrado, la agregación y la segmentación de tiempo. En este artículo se ofrecen algunos puntos a tener en cuenta al preparar los datos. Agregar previamente datos puede optimizar tanto la creación como el uso de informes móviles y algunos diseños de informes móviles lo requieren.   
  
## <a name="date-and-time-formats"></a>Formatos de fecha y hora 
Al trabajar con intervalos de fecha y hora para usarlos en un informe móvil, especialmente con TimeNavigator, es importante dar formato correctamente a la columna de fecha y hora para que el [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] pueda identificarla como tal. Estos son algunos ejemplos de formatos de fecha y hora válidos:  
  
    05/01/2009    
    2009-05-01    
    05/01/2009 14:57:32.8    
    2009-05-01 14:57:32.8    
    2009-05-01T14:57:32.8375298-04:00    
    5/01/2008 14:57:32.80 -07:00    
    1 May 2008 2:57:32.8 PM    
    Fri, 15 May 2009 20:10:57 GMT    
  
Los conjuntos de datos basados en la fecha y hora se pueden describir, en la mayoría de los casos, mediante uno o varios intervalos de fecha y hora, como, por ejemplo, cada hora, diariamente, mensualmente, trimestralmente y anualmente. [!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] puede combinar varias tablas de diferente granularidad y mostrarlas en un único informe móvil. En cambio, tenga en cuenta los intervalos relevantes de los conjuntos de datos originales, ya que pueden ayudar a la hora de decidir qué opciones del filtro de fecha y hora presentar al usuario en el informe móvil final.  

Los campos de fecha en modelos tabulares y multidimensionales de [!INCLUDE[ssASnoversion_md](../../includes/ssasnoversion-md.md)] pueden perder su formato de fecha en conjuntos de datos compartidos. Para obtener una solución que mantenga su formato, vea [Conservar el formato de fecha para Analysis Services en los informes móviles](../../reporting-services/mobile-reports/retain-date-formatting-for-analysis-services-in-mobile-reports.md) .
  
## <a name="preparing-filter-data"></a>Preparar los datos del filtro ##  
[!INCLUDE[PRODUCT_NAME](../../includes/ss-mobilereptpub-short.md)] puede filtrar datos basándose tanto en los campos de fecha y hora como en los campos clave. Aunque los campos clave pueden ser numéricos, en la mayoría de los casos, son un id. o un valor de cadena. Para preparar un campo de filtro para usarlo con un elemento de navegador, como la lista de selección, la clave del filtro debe ser una sola columna en la tabla de datos. De este modo, puede agrupar las filas de la tabla según el valor de la columna del filtro. Tener varias columnas que contengan claves de filtro diferentes o criterios de filtro permite que se usen conjuntamente informes móviles con varios navegadores de filtro jerárquica o individualmente.  
  
| Sector  | País   | Region    |  
| ------------- | ------------- | ------------- |  
| Bancos     | AFGANISTÁN   | ASIA      |  
| Servicios comerciales y profesionales | AFGANISTÁN | ASIA |  
| Alimentación, bebidas y tabaco | AFGANISTÁN | ASIA |  
| Multimedia | AFGANISTÁN | ASIA |  
| Productos farmacéuticos | AFGANISTÁN | ASIA |  
| Comida y venta al por menor básica | ALBANIA | EUROPA |  
  
  
También se pueden estructurar jerárquicamente los filtros basados en claves para usarlos con una lista de selección en una estructura de árbol. Para preparar los datos para usarlos en este tipo de escenario, cree una tabla de búsqueda que describa la estructura jerárquica. Use una estructura de tabla que incluya una columna Key y una columna Parent Key para indicar si un nodo pertenece a la jerarquía general.  
  
En esta tabla, los elementos ParentKey aparecen primero en la columna ItemKey, después se muestran en la columna ParentItemKey junto a sus elementos secundarios.   
  
|ItemKey    | ParentItemKey |  
| ------------- | ------------- |  
| Datos financieros    |   |  
| Sectores   |   |  
| Básicos del consumidor |    |  
| Consumo discrecional |  |     
| Asistencia sanitaria   |   |  
| Tecnologías de la información |  |  
| Bancos | Datos financieros |  
| Inmobiliaria | Datos financieros |  
| Finanzas diversificadas |  Datos financieros |   
| Seguros |   Datos financieros |  
| Servicios comerciales y profesionales |  Sectores |  
| Bienes de capital |   Sectores |  
| Transporte |  Sectores |  
| Alimentación, bebidas y tabaco |    Básicos del consumidor |  
| Comida y venta al por menor básica |    Básicos del consumidor |  
| Hogar y productos personales | Básicos del consumidor |  
| Multimedia | Consumo discrecional |  
| Automóviles y componentes |  Consumo discrecional |  
| Ropa y bienes de consumo duradero |Consumo discrecional |  
| Servicios del consumidor |   Consumo discrecional |  
| Venta al por menor | Consumo discrecional |  
| Productos farmacéuticos   | Asistencia sanitaria |  
| Equipo y servicios de asistencia sanitaria |    Asistencia sanitaria |  
| Software y servicios | Tecnologías de la información |  
| Equipos y hardware de tecnología   | Tecnologías de la información |  
| Servicios de telecomunicaciones |Tecnologías de la información |  
  
### <a name="see-also"></a>Vea también  
- [Preparación de los datos de Excel para informes móviles de Reporting Services](../../reporting-services/mobile-reports/prepare-excel-data-for-reporting-services-mobile-reports.md)  
- [Conservar el formato de fecha para Analysis Services en los informes móviles](../../reporting-services/mobile-reports/retain-date-formatting-for-analysis-services-in-mobile-reports.md)
- [Creación y publicación de informes móviles con el Publicador de informes móviles de SQL Server](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)
  
  
  

