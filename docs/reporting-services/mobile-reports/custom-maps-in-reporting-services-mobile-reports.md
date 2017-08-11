---
title: "Mapas personalizados en informes móviles de Reporting Services | Documentos de Microsoft"
ms.custom: 
ms.date: 03/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 59a4ebad-587a-4770-afcd-c69216b8afd9
caps.latest.revision: 9
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 410863a8fc12424addbc8edba0196066fd1daf79
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="custom-maps-in-reporting-services-mobile-reports"></a>Mapas personalizados en informes para dispositivos móviles de Reporting Services
Mapas geográficos en SQL Server Mobile Report Publisher se definen en un formato conocido como *archivos de forma ESRI*.  
  
Este formato lo diseñó una empresa privada, pero actualmente se trata de un formato semiabierto extendido que se utiliza en una gran mayoría de las aplicaciones SIG. Según este formato, Mobile Report Publisher requiere dos archivos que se proporcione al definir una asignación:  
  
- Un archivo .SHP para geometrías de formas  
- Un archivo .DBF para metadatos  
  
Los nombres de archivo de base deben coincidir (por ejemplo, *canada.shp* y *canada.dbf*). Los metadatos deben incluir el campo *NOMBRE* con el valor del nombre de la forma correspondiente (clave), que se usará al rellenar el mapa con datos.  
  
> **Nota**: Los dos archivos de mapa, SHP y DBF, no pueden tener un tamaño superior a 512 KB. Si los archivos de mapa son demasiado grandes, use una herramienta como [http://mapshaper.org/](http://mapshaper.org/) para reducir el tamaño.  
  
Vea cómo [Agregar un mapa personalizado a un informe de Reporting Services móvil](../../reporting-services/mobile-reports/add-a-custom-map-to-a-reporting-services-mobile-report.md).  
  
## <a name="technical-information"></a>Información técnica  
  
- La especificación oficial: [http://www.esri.com/library/whitepapers/pdfs/shapefile.pdf](http://www.esri.com/library/whitepapers/pdfs/shapefile.pdf)  
- El artículo de Wikipedia sobre archivos de forma: [https://es.wikipedia.org/wiki/Shapefile](http://en.wikipedia.org/wiki/Shapefile)  
  
## <a name="creating--editing-map-geometry"></a>Creación y edición de geometría de mapas  
  
La creación y edición de archivos de formas constituyen un proceso complejo que va más allá del ámbito de aplicación de este documento. A continuación se indican algunos recursos y aplicaciones para ayudarle a empezar:  
  
- ArcGIS: [http://www.arcgis.com/](http://www.arcgis.com/)  
- Complemento MAPublisher para Adobe Illustrator: [http://www.avenza.com/mapublisher](http://www.avenza.com/mapublisher)  
- QuantumGIS (gratuito): [http://www.qgis.org/](http://www.qgis.org/)  
- Editor de archivos de forma Manco: [http://www.mancosoftware.com/ShapeFileEditor](http://www.mancosoftware.com/ShapeFileEditor)  
  
## <a name="existing-shapefiles"></a>Archivos de formas existentes  
  
Muchos archivos de formas existentes se pueden descargar desde Internet, en sitios como estos:  
  
- Diva-GIS: [http://www.diva-gis.org/Data](http://www.diva-gis.org/Data)  
- OpenStreetMap: [http://openstreetmapdata.com/data](http://openstreetmapdata.com/data)  
  
### <a name="see-also"></a>Vea también  
- [Mapas de informes de Reporting Services móviles](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)  
- [Create and publish mobile reports with SQL Server Mobile Report Publisher (Creación y publicación de informes móviles con el Publicador de informes de SQL Server Mobile)](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)   
  
  
  

