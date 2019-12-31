---
title: Configuraciones de hardware
description: El hardware del dispositivo de Analytics Platform System (APS) está diseñado con unidades escalables para que pueda comprar la cantidad adecuada de procesamiento y almacenamiento según sus requisitos empresariales. El dispositivo escala el almacenamiento para almacenamiento de datos paralelos de unos pocos terabytes a más de 6 petabytes de datos.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: ee16045931da345f06c141597ccd25d19a36dea7
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401134"
---
# <a name="hardware-configurations---analytics-platform-system"></a>Configuraciones de hardware: Analytics Platform System
El hardware de Analytics Platform System (APS) está diseñado con unidades escalables para que pueda comprar la cantidad adecuada de procesamiento y almacenamiento según sus requisitos empresariales. El dispositivo escala el almacenamiento para SQL Server Wareouse de datos paralelos (PDW) de unos pocos terabytes a más de 6 petabytes de datos.  
  
## <a name="contents"></a>Contenido  
  
-   [Configuraciones de un bastidor](#section1)  
  
-   [Configuraciones de varios bastidores](#section2)  

  
## <a name="section1"></a>Configuraciones de un bastidor  
El primer bastidor del dispositivo contiene los componentes necesarios para ejecutar PDW. La configuración mínima del dispositivo es un bastidor y una red, además de una unidad de escalado base. En estos diagramas se muestran las maneras en las que se puede configurar el primer bastidor del dispositivo. Puede tener entre 2 y 9 nodos de proceso en el primer bastidor, dependiendo del proveedor de hardware.  
  
### <a name="first-rack-configurations---dell"></a>Configuraciones de primer bastidor: DELL  
La configuración mínima de un dispositivo DELL tiene 3 nodos de proceso. Puede Agregar hasta 2 unidades de escalado de datos al primer bastidor para un total de 9 nodos de proceso.  
  
![Configuraciones de primer bastidor de Dell](media/first-rack-configurations-dell.png "Configuraciones de primer bastidor de Dell")  
  
### <a name="first-rack-configurations---hpe"></a>Configuraciones de primer bastidor: HPE  
La configuración mínima de un dispositivo HPE tiene 2 nodos de proceso. Puede Agregar hasta 3 unidades de escalado de datos en el primer bastidor para un total de 8 nodos de proceso.  
  
![Configuraciones de HPE First rack para HPE](media/first-rack-configurations-hpe.png "Configuraciones de primer bastidor de HPE")  
  
## <a name="section2"></a>Configuraciones de varios bastidores  
Para agregar capacidad a PDW, puede agregar unidades de escala de datos, junto con componentes de red & de bastidor adicionales, según sea necesario, para proporcionar la energía, las redes y la infraestructura de bastidor adecuadas. Cada red & bastidor adicional requiere un host pasivo.  
  
Cada proveedor de hardware especifica el número de unidades de escalado de datos que puede Agregar a partir de la capacidad del dispositivo. Se recomienda agregar suficientes unidades de escala de datos para ver al menos un 20 por ciento de rendimiento. Por ejemplo, la adición de una unidad de escalado de datos a un dispositivo que ya tiene 20 unidades de escalado de datos puede dar lugar a una ganancia de rendimiento insignificante. La ganancia neta no merece la pena el costo y el esfuerzo.  
  
### <a name="scale-out-example---hpe"></a>Ejemplo de escalado horizontal: HPE  
En este diagrama se muestra un dispositivo de tres bastidores de HP que contiene 20 nodos de proceso.  
  
![Dispositivo HPE con 20 nodos de proceso](media/scale-out-hpe.png "Dispositivo HPE con 20 nodos de proceso")  
  
### <a name="scale-out-example---dell-quanta"></a>Escalabilidad horizontal ejemplo: DELL, cuantos  
En este diagrama se muestra un dispositivo DELL o Quanta de 3 bastidores que contiene 21 nodos de proceso.  
  
![Dispositivo Dell con 21 nodos de proceso](media/scale-out-dell.png "Dispositivo Dell con 21 nodos de proceso")  
 
