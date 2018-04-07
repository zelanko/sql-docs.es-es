---
title: Configuraciones de hardware (Analytics Platform System)
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.suite: sql
ms.custom: ''
ms.technology: mpp-data-warehouse
description: El hardware Analytics Platform System (APS) está diseñado con unidades escalables para que comprar la cantidad correcta de procesamiento y almacenamiento según sus requisitos empresariales.
ms.date: 01/05/2017
ms.topic: article
ms.assetid: f95945b7-97ae-4ab9-bae5-c792a516acea
caps.latest.revision: 9
ms.openlocfilehash: d6f4b25584826d637db0a5f51ebe8ede458136c2
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="hardware-configurations"></a>Configuraciones de hardware
El hardware Analytics Platform System (APS) está diseñado con unidades escalables para que comprar la cantidad correcta de procesamiento y almacenamiento según sus requisitos empresariales. El dispositivo escala para SQL Server Parallel datos Wareouse (PDW) de unos pocos Terabytes a más de 6 Petabytes de datos de almacenamiento.  
  
## <a name="contents"></a>Contenido  
  
-   [Configuraciones de un bastidor](#section1)  
  
-   [Bastidor varias configuraciones](#section2)  

  
## <a name="section1"></a>Configuraciones de un bastidor  
El primer bastidor en el dispositivo contiene los componentes necesarios para ejecutar PDW. La configuración mínima del dispositivo es un bastidor y red además de una unidad de escalado de Base. Estos diagramas muestran formas que se puede configurar el primer bastidor del dispositivo. Puede tener entre 2 y 9 nodos de proceso en el primer bastidor, según el fabricante del hardware.  
  
### <a name="first-rack-configurations---dell"></a>En primer lugar bastidor configuraciones - DELL  
La configuración mínima para un dispositivo de DELL tiene 3 nodos de proceso. Puede agregar hasta 2 unidades de escala de datos para el primer bastidor para un total de 9 nodos de proceso.  
  
![Configuraciones de primer bastidor Dell](media/first-rack-configurations-dell.png "configuraciones de primer bastidor de Dell")  
  
### <a name="first-rack-configurations---hpe"></a>En primer lugar bastidor configuraciones - HPE  
La configuración mínima para un dispositivo HPE tiene 2 nodos de proceso. Puede agregar hasta 3 unidades de escala de datos para el primer bastidor para un total de 8 nodos de proceso.  
  
![HPE bastidor primero las configuraciones de HPE](media/first-rack-configurations-hpe.png "HPE primero las configuraciones en bastidor")  
  
## <a name="section2"></a>Bastidor varias configuraciones  
Para agregar capacidad al PDW puede agregar a unidades de escala de datos, junto con los componentes adicionales de bastidor y red según sea necesario para proporcionar la potencia adecuada, redes y bastidor infraestructura. Cada bastidor y red adicionales requiere un host pasivo.  
  
Cada proveedor de hardware especifica el número de unidades de escala de datos que puede agregar tiene la capacidad de su dispositivo. Se recomienda agregar suficientes unidades de escala de datos para ver, al menos, un aumento del 20 por ciento en el rendimiento. Por ejemplo, agregar una escala de datos de unidad a un equipo que ya tiene 20 unidades de escala de datos podría producir un aumento del rendimiento insignificante. La ganancia neta no sería que vale la pena el coste y el esfuerzo.  
  
### <a name="scale-out-example---hpe"></a>Escalar horizontalmente ejemplo - HPE  
Este diagrama muestra una aplicación de 3 bastidor HP que contiene 20 nodos de ejecución.  
  
![Dispositivo de HPE con 20 nodos de proceso](media/scale-out-hpe.png "dispositivo HPE con 20 nodos de proceso")  
  
### <a name="scale-out-example--dell-quanta"></a>Escalado horizontal de ejemplo: DELL, Quanta  
Este diagrama muestra un dispositivo de DELL o Quanta 3 bastidor que contiene 21 nodos de proceso.  
  
![Dispositivo de Dell con 21 nodos de proceso](media/scale-out-dell.png "dispositivo de Dell con 21 nodos de proceso")  
 
