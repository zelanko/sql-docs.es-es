---
title: Mapas personalizados en informes para dispositivos móviles de Reporting Services | Microsoft Docs
ms.date: 03/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: 59a4ebad-587a-4770-afcd-c69216b8afd9
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: a3786fcf92c767905c6295dffc8a24e7a86d2cbe
ms.sourcegitcommit: 9ece10c2970a4f0812647149d3de2c6b75713e14
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/16/2018
ms.locfileid: "51813948"
---
# <a name="custom-maps-in-reporting-services-mobile-reports"></a>Mapas personalizados en informes para dispositivos móviles de Reporting Services
Los mapas geográficos del Publicador de informes móviles de Microsoft SQL Server se definen en un formato conocido como *archivos de forma ESRI*.  
  
Este formato lo diseñó una empresa privada, pero actualmente se trata de un formato semiabierto extendido que se utiliza en una gran mayoría de las aplicaciones SIG. Según este formato, el Publicador de informes móviles requiere que se proporcionen dos archivos al definir un mapa:  
  
- Un archivo .SHP para geometrías de formas  
- Un archivo .DBF para metadatos  
  
Los nombres de archivo de base deben coincidir (por ejemplo, *canada.shp* y *canada.dbf*). Los metadatos deben incluir el campo *NOMBRE* con el valor del nombre de la forma correspondiente (clave), que se usará al rellenar el mapa con datos.  
  
> **Nota**: Los dos archivos de mapa, SHP y DBF, no pueden tener un tamaño superior a 512 KB. Si los archivos de asignación son demasiado grandes, use una herramienta como [https://mapshaper.org/](https://mapshaper.org/) para reducir el tamaño.  
  
Vea cómo [Agregar un mapa personalizado a un informe de Reporting Services móvil](../../reporting-services/mobile-reports/add-a-custom-map-to-a-reporting-services-mobile-report.md).  
  
## <a name="technical-information"></a>Información técnica  
  
- La especificación oficial: [https://www.esri.com/library/whitepapers/pdfs/shapefile.pdf](https://www.esri.com/library/whitepapers/pdfs/shapefile.pdf)  
- El artículo del archivo de forma de Wikipedia: [https://en.wikipedia.org/wiki/Shapefile](https://en.wikipedia.org/wiki/Shapefile)  
  
## <a name="creating--editing-map-geometry"></a>Creación y edición de geometría de mapas  
  
La creación y edición de archivos de formas constituyen un proceso complejo que va más allá del ámbito de aplicación de este documento. A continuación se indican algunos recursos y aplicaciones para ayudarle a empezar:  
  
- ArcGIS: [https://www.arcgis.com/](https://www.arcgis.com/)  
- Complemento MAPublisher para Adobe Illustrator: [https://www.avenza.com/mapublisher](https://www.avenza.com/mapublisher)  
- QuantumGIS (gratis): [https://www.qgis.org/](https://www.qgis.org/)  
- Editor de archivos de forma Manco: [https://www.mancosoftware.com/ShapeFileEditor](https://www.mancosoftware.com/ShapeFileEditor)  
  
## <a name="existing-shapefiles"></a>Archivos de formas existentes  
  
Muchos archivos de formas existentes se pueden descargar desde Internet, en sitios como estos:  
  
- DIVA-GIS: [https://www.diva-gis.org/Data](https://www.diva-gis.org/Data)  
- OpenStreetMap: [https://openstreetmapdata.com/data](https://openstreetmapdata.com/data)  
  
### <a name="see-also"></a>Vea también  
- [Mapas de informes de Reporting Services móviles](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)  
- [Create and publish mobile reports with SQL Server Mobile Report Publisher (Creación y publicación de informes móviles con el Publicador de informes de SQL Server Mobile)](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)   
  
  
  
