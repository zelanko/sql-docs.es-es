---
title: 'Las configuraciones de hardware: Analytics Platform System | Documentos de Microsoft'
description: El hardware del equipo Analytics Platform System (APS) está diseñado con unidades escalables para que comprar la cantidad correcta de procesamiento y almacenamiento según sus requisitos empresariales. El dispositivo escala almacenamiento almacenamiento de datos paralelos de unos pocos terabytes a más de 6 petabytes de datos.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 5677298e1924959c83cd95b86845e37eab7340e9
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/19/2018
---
# <a name="hardware-configurations---analytics-platform-system"></a>Configuraciones de hardware: Analytics Platform System
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
 
