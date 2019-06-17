---
title: Las configuraciones de hardware - Analytics Platform System | Microsoft Docs
description: El hardware de dispositivo de Analytics Platform System (APS) está diseñado con unidades escalables de forma que comprar la cantidad adecuada de procesamiento y almacenamiento según sus requisitos empresariales. El dispositivo escala almacenamiento para almacenamiento de datos paralelos de unos pocos terabytes a más de 6 petabytes de datos.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 2a252e5f2aebd8d51b9b0eb1f353ded504155c2e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63283268"
---
# <a name="hardware-configurations---analytics-platform-system"></a>Configuraciones de hardware - Analytics Platform System
El hardware de Analytics Platform System (APS) está diseñado con unidades escalables de forma que comprar la cantidad adecuada de procesamiento y almacenamiento según sus requisitos empresariales. El dispositivo se puede escalar almacenamiento para SQL Server paralelo datos Wareouse (PDW) de unos pocos Terabytes a más de 6 Petabytes de datos.  
  
## <a name="contents"></a>Contenido  
  
-   [Configuraciones de un bastidor](#section1)  
  
-   [Bastidor varias configuraciones](#section2)  

  
## <a name="section1"></a>Configuraciones de un bastidor  
El primer bastidor en el dispositivo contiene los componentes necesarios para ejecutar PDW. La configuración mínima del dispositivo es un bastidor y red además de una unidad de escalado de Base. Estos diagramas muestran formas que se puede configurar el primer bastidor del dispositivo. Puede tener entre 2 y 9 nodos de proceso en el primer bastidor, según el fabricante del hardware.  
  
### <a name="first-rack-configurations---dell"></a>En primer lugar bastidor configuraciones - DELL  
La configuración mínima para un dispositivo de DELL tiene 3 nodos de proceso. Puede agregar hasta 2 unidades de escalado de datos para el primer bastidor con un total de 9 nodos de proceso.  
  
![Configuraciones de primer bastidor de Dell](media/first-rack-configurations-dell.png "configuraciones de primer bastidor de Dell")  
  
### <a name="first-rack-configurations---hpe"></a>En primer lugar bastidor configuraciones - HPE  
La configuración mínima para un dispositivo HPE tiene 2 nodos de proceso. Puede agregar hasta 3 unidades de escalado de datos para el primer bastidor con un total de 8 nodos de proceso.  
  
![HPE bastidor primero las configuraciones de HPE](media/first-rack-configurations-hpe.png "HPE primero las configuraciones en bastidor")  
  
## <a name="section2"></a>Bastidor varias configuraciones  
Para agregar capacidad al PDW puede agregar a unidades de escalado de datos, junto con los componentes de bastidor y red adicionales según sea necesario para proporcionar la capacidad adecuada, redes y bastidor de infraestructura. Cada bastidor adicionales y la red requiere un host pasivo.  
  
Cada proveedor de hardware especifica el número de unidades de escala de datos que se pueden agregar según la capacidad de su dispositivo. Se recomienda agregar unidades de escala de datos suficientes para ver al menos un aumento del 20 por ciento en rendimiento. Por ejemplo, agregar una escala de datos podría unidad a un dispositivo que ya tiene 20 unidades de escala de datos en un aumento del rendimiento insignificante. No sería la ganancia neta que vale la pena el costo y esfuerzo.  
  
### <a name="scale-out-example---hpe"></a>Escalar horizontalmente por ejemplo, HPE  
Este diagrama muestra una aplicación de 3 bastidor HP que contiene 20 nodos de proceso.  
  
![Dispositivo HPE con 20 nodos de proceso](media/scale-out-hpe.png "dispositivo HPE con 20 nodos de proceso")  
  
### <a name="scale-out-example---dell-quanta"></a>Escalar horizontalmente por ejemplo, DELL, cuantos  
Este diagrama muestra un dispositivo de DELL o Quanta 3 bastidor, que contiene el 21 nodos de proceso.  
  
![Dispositivo de Dell con 21 nodos de proceso](media/scale-out-dell.png "dispositivo Dell con 21 nodos de proceso")  
 
