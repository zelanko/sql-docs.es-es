---
title: Planear la compatibilidad con informes de mapa | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 5ddc97a7-7ee5-475d-bc49-3b814dce7e19
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: df796e2dd4e132164f00716a9cb12f7b498d8984
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66108079"
---
# <a name="plan-for-map-report-support"></a>Planear la compatibilidad de informe de mapa
  [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)]admite informes de mapas que usan orígenes de datos espaciales. Los datos espaciales pueden proceder de bases de datos de SQL Server, de archivos de forma ESRI o de la galería de mapas que se instala con Reporting Services o con el Generador de informes. Un mapa también puede mostrar un fondo de mosaicos de mapa de Bing. Un autor de informes puede crear un informe que especifique datos espaciales o mosaicos de mapa de Bing como dinámicos y recuperados en el tiempo de ejecución o como estáticos e incrustados en la definición de informe.  
  
## <a name="support-for-bing-maps"></a>Compatibilidad con Bing Maps  
 Los mapas pueden incluir un nivel de fondo que muestra los mosaicos de mapa de Bing. Para ver un informe publicado que tenga una capa de mosaicos de mapas, el servidor de informes debe estar configurado para recuperar mosaicos de los servicios web de Bing Maps. Para más información, consulte [RSReportServer Configuration File](report-server/rsreportserver-config-configuration-file.md).  
  
 En cada informe, sus autores pueden especificar si se utiliza una conexión de Capa de sockets seguros (SSL) para recuperar los mosaicos del servidor de mosaicos. Para ello, en el panel Propiedades de la capa de mosaico, deben establecer la propiedad booleana UseSecureConnection en `true`.  
  
> [!NOTE]  
>   Para obtener más información sobre el uso de mosaicos de Bing Maps en un informe, vea [Condiciones adicionales de uso](https://go.microsoft.com/fwlink/?LinkId=151371) y [Declaración de privacidad](https://go.microsoft.com/fwlink/?LinkId=151372).  
  
## <a name="report-design-recommendations"></a>Recomendaciones de diseño de informes  
 Un buen diseño de los informes de mapas requiere que su autor evalúe los pros y los contras entre los datos espaciales estáticos y dinámicos, y que encuentre un equilibrio que sirva para los usuarios del informe. Los elementos de mapa incrustados pueden aumentar considerablemente el tamaño de la definición de informe, pero reducen el tiempo necesario para ver el informe de mapa. Los elementos de mapa dinámicos reducen el tamaño de la definición de informe, pero aumentan el tiempo necesario para procesar y ver el mapa. El autor del informe debe buscar el equilibrio adecuado entre estos aspectos opuestos.  
  
 Si el tamaño de la definición de informe constituye un problema, como administrador del servidor de informes, puede recomendar a los diseñadores de informes que reduzcan la cantidad de datos espaciales en una definición de informe.  
  
 En las siguientes condiciones, los elementos de mapa están incrustados en la definición de informe:  
  
-   Cuando se crea el informe, el origen de datos espaciales está en el sistema de archivos local. Esto incluye los datos espaciales de la Galería de mapas o de los archivos de forma ESRI que se han instalado localmente. De forma predeterminada, el asistente para mapas y el asistente para capas de mapa incrustan datos espaciales a partir de orígenes de datos en el sistema de archivos local.  
  
-   El autor del informe elige la opción para incrustar manualmente los datos espaciales en el informe.  
  
 Para ayudar a reducir el tamaño de las definiciones de informe que tienen los mapas, los autores de informes pueden usan una o varias de las siguientes opciones:  
  
-   Desde el Diseñador de informes en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], agregue orígenes de datos espaciales que sean archivos de forma ESRI al proyecto del servidor de informes. Al implementar el proyecto, los archivos de forma ESRI se publican en el servidor de informes además del informe. Cuando el autor del informe ejecuta el Asistente para mapas, puede especificar un origen de datos espaciales desde el proyecto del servidor de informes y los elementos de mapa no se incrustan en las definiciones de informe de forma predeterminada.  
  
-   Desde el Generador de informes, agregue orígenes de datos espaciales que sean archivos de forma ESRI seleccionándolos en el servidor de informes. Cuando el autor del informe ejecuta el Asistente para mapas, puede buscar y seleccionar un origen de datos espaciales desde el proyecto del servidor de informes y los elementos de mapa no se incrustan en las definiciones de informe de forma predeterminada.  
  
-   Cuando los datos de mapa deban ser incrustados, ajuste el centro de la ventanilla y el nivel de zoom para incluir solo los datos de mapa necesarios para el informe.  
  
 Para obtener más información, [Maps &#40;generador de informes y SSRS&#41;](report-design/maps-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte también  
 [Solucionar problemas de los informes: informes de mapa &#40;Generador de informes y SSRS&#41;](report-design/troubleshoot-reports-map-reports-report-builder-and-ssrs.md)  
  
  
