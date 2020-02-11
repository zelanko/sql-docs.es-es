---
title: Cuadro de diálogo Propiedades de ventanilla de mapa, general | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.mapviewport.general.f1
- "10505"
ms.assetid: 6c9c773e-5c56-4571-95ed-8a157cfdfe52
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 8ec0aaa051ba317cd05a9784c80fb997f5fa19e6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66108235"
---
# <a name="map-viewport-properties-dialog-box-general"></a>Cuadro de diálogo Propiedades de ventanilla de mapa, General
  Seleccione **General** en el cuadro de diálogo **Propiedades de ventanilla de mapa** para cambiar las opciones del sistema de coordenadas, la proyección y los límites.  
  
## <a name="options"></a>Opciones  
 **Sistema de coordenadas**  
 Indique el tipo de sistema de coordenadas que el mapa de datos usa.  
  
-   **Plano** de Elija esta opción cuando los datos del mapa estén en coordenadas X e y, por ejemplo, para crear planes.  
  
-   **Zona geográfica** Elija esta opción cuando los datos del mapa estén en coordenadas de longitud y latitud, por ejemplo, para ubicaciones de ciudades.  
  
 **Estando**  
 Especifique el método que utilizar para proyectar las coordenadas geográficas en una superficie bidimensional. Elija una proyección que sea compatible con los datos que está visualizando. Las cuatro propiedades espaciales a las que afecta la proyección son el área, forma, distancia y dirección. Para las vistas de la tierra, una buena opción de proyección depende de la vista del centro, los límites del mapa y el factor de zoom.  
  
 Cada una de las proyecciones siguientes conserva una o varias de estas propiedades espaciales:  
  
-   **Equirectangular** Elija esta opción para usar la longitud y la latitud como coordenadas rectangulares.  
  
-   **Mercator** Elija esta proyección popular para áreas más pequeñas, para menos distorsión alrededor del Ecuador o si desea agregar una capa de mapa con una capa de mosaico existente que use la proyección Mercator.  
  
-   **Robinson** Elija esta opción para menos distorsión de las áreas grandes que abarcan desde el Ecuador hasta los polos. Fue desarrollado por Arthur H. Robinson en 1963.  
  
-   **Fahey** Elija esta opción para menos distorsión de las áreas grandes que abarcan desde el Ecuador hasta los polos. Fue desarrollado por Lawrence Fahey en 1975.  
  
-   **Eckert1** Elija esta opción para usar paralelos equidistantes en latitud y líneas rectas para los meridianos en longitud.  
  
-   **Eckert3** Elija esta opción para usar paralelos equidistantes en latitud y líneas curvas para los meridianos en longitud.  
  
-   **HammerAitoff** Elija esta opción para mapas polares o mapas mundiales.  
  
-   **Wagner3** Elija esta opción para las asignaciones mundiales.  
  
-   **Bonne** Elija esta opción para ver el mundo tal como aparece en un Atlas.  
  
 **Opciones de salto de página**  
 Seleccione opciones para indicar la manera en que se ajusta el contenido a una página del informe.  
  
 **Opciones de límite**  
 Especifique los límites inferior y superior de las coordenadas para controlar qué parte del mapa aparece en el informe.  
  
 **X mínimo**  
 El valor de X inferior. Solo está disponible para **Planar** .  
  
 **X máximo**  
 El valor de X superior. Solo está disponible para **Planar** .  
  
 **Y mínimo**  
 El valor de Y inferior. Solo está disponible para **Planar** .  
  
 **Y máximo**  
 El valor de Y superior. Solo está disponible para **Planar** .  
  
 **Longitud mínima**  
 El valor de longitud inferior. Solo está disponible para **Geographic** .  
  
 **Longitud máxima**  
 El valor de longitud superior. Solo está disponible para **Geographic** .  
  
 **Latitud mínima**  
 El valor de latitud inferior. Solo está disponible para **Geographic** .  
  
 **Latitud máxima**  
 El valor de latitud superior. Solo está disponible para **Geographic** .  
  
## <a name="see-also"></a>Consulte también  
 [Mapas &#40;Generador de informes y SSRS&#41;](report-design/maps-report-builder-and-ssrs.md)  
  
  
