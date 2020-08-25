---
title: Capacidad de procesamiento y almacenamiento
description: Los requisitos empresariales determinan el número de unidades de escala de datos y el tamaño de los discos de nodos de proceso que se necesitan en el dispositivo de análisis de plataforma (APS).
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 143c37b6b55b96f8a0225c98db2212f07b2cd3a5
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "74400544"
---
# <a name="processing-and-storage-capacity-in-analytics-platform-system"></a>Capacidad de procesamiento y almacenamiento en Analytics Platform System
Los requisitos empresariales determinan el número de unidades de escala de datos y el tamaño de los discos de nodos de proceso que se necesitan en el dispositivo de análisis de plataforma (APS). Use estos cálculos de procesamiento y almacenamiento para guiar las decisiones de compra y planeamiento de la capacidad.  
  
  
## <a name="planning-for-processing-capacity"></a><a name="section1"></a>Planeación de la capacidad de procesamiento  
El rendimiento de las consultas para SQL Server almacenamiento de datos paralelos (PDW) depende en gran medida del número de núcleos de CPU que trabajan en los datos en paralelo. Dentro de los límites, el aumento del paralelismo mejora el rendimiento de las consultas de procesamiento paralelo masivo (MPP). Incluso si el tamaño de los datos es relativamente pequeño, la potencia del motor de consulta MPP se ha mejorado con un mayor paralelismo.  
  
Por ejemplo, un dispositivo con 12 nodos de proceso tiene 192 núcleos de CPU que procesan los datos en paralelo. Ese es el paralelismo 192. Un dispositivo con 56 nodos de proceso tiene 896 núcleos que funcionan en paralelo. Esta magnitud de paralelismo no es factible sin la computación de MPP.  
  
A medida que aumenta el número de nodos de proceso, el escalado horizontal del dispositivo requiere que se agregue más de un nodo de proceso a la vez para obtener una ventaja perceptible. Los proveedores de hardware solo admiten configuraciones específicas de unidades de escala de datos para garantizar que la ventaja de escalar el dispositivo supera el costo de redistribuir los datos entre más nodos de proceso.  
  
### <a name="data-scale-unit-configuration-examples---hpe"></a>Ejemplos de configuración de unidades de escala de datos: HPE  
Estos son ejemplos de las configuraciones de HPE admitidas para la escala de datos Uunits. Pueden variar de las configuraciones admitidas más recientes, pero se proporcionan como ejemplo de cómo aumentar la capacidad en un 20 por ciento aproximadamente.  
  
La elevación es el porcentaje de aumento de capacidad incrementando el Uunits de escala de datos de una fila a la siguiente. Por ejemplo, al aumentar las unidades de escala de datos de 6 a 8, se obtiene una mejora del 33% en la memoria y los núcleos de CPU.  También aumenta el espacio en disco que no se muestra en esta tabla.  
  
|Unidades de escalado de datos|Nodos de proceso|Núcleos de CPU|Memoria (GB)|Garantía|  
|--------------------|-----------------|-------------|-----------------|----------|  
|1|2|32|512|-|  
|2|4|64|1024|100%|  
|3|6|96|1536|50 %|  
|4|8|128|2048|33 %|  
|5|10|160|2560|25 %|  
|6|12|192|3072|20%|  
|8|16|256|4096|33 %|  
|10|20|320|5120|25 %|  
|12|24|384|6144|20%|  
|16|32|512|8192|33 %|  
|20|40|640|10240|25 %|  
|24|48|768|12288|20%|  
|28|56|896|14336|17 %|  
  
Explicación:  
  
-   **Unidades de escalado de datos** por dispositivo. Para obtener información sobre las unidades de escalado de datos, consulte [los componentes de hardware del sistema de plataforma de análisis](hardware-components.md).  
  
-   **Nodos de proceso** por dispositivo.  
  
-   **Núcleos de CPU** por dispositivo. Hay 16 núcleos por nodo de proceso, un núcleo por cada par de disco reflejado. Para la estructura de disco del nodo de proceso, consulte [componentes de hardware del sistema de plataforma de análisis](hardware-components.md).  
  
-   **Memoria** por dispositivo. Cada núcleo tiene 256 GB de memoria.  
  
### <a name="data-scale-unit-configuration-examples---dell-quanta"></a>Ejemplos de configuración de unidades de escala de datos: Dell, cuantos  
Estos son ejemplos de las configuraciones admitidas de Dell y cuantos para la escala de datos Uunits. Pueden variar de las configuraciones admitidas más recientes, pero se proporcionan como ejemplo de cómo aumentar la capacidad en un 20 por ciento aproximadamente.  
  
La elevación es el porcentaje de aumento de capacidad incrementando el Uunits de escala de datos de una fila a la siguiente. Por ejemplo, al aumentar las unidades de escala de datos de 6 a 8, se obtiene una mejora del 33% en la memoria y los núcleos de CPU. También aumenta el espacio en disco que no se muestra en esta tabla.  
  
|Unidades de escalado de datos|Nodos de proceso|Núcleos de CPU|Memoria (GB)|Garantía|  
|--------------------|-----------------|-------------|-----------------|----------|  
|1|3|48|768|-|  
|2|6|96|1536|100%|  
|3|9|144|2.304|50 %|  
|4|12|192|3072|33 %|  
|5|15|240|3.840|25 %|  
|6|18|288|4.608|20%|  
|7|21|336|5.376|17 %|  
|8|24|384|6144|14 %|  
|9|27|432|6.912|13 %|  
|12|36|576|9.216|33 %|  
|15|45|720|11.520|25 %|  
|18|54|864|13 824|20%|  
  
## <a name="planning-for-storage-capacity"></a><a name="section2"></a>Planeación de la capacidad de almacenamiento  
En esta tabla se calcula que se pueden cargar y almacenar hasta 6 petabytes de datos sin comprimir en una aplicación de sistema de análisis de plataforma totalmente compilada. 
  
|Vendor|Tamaño de la unidad|Almacenamiento físico de datos por nodo de proceso|Máximo de nodos de proceso por bastidor|Almacenamiento de datos máximo físico por bastidor|Almacenamiento de datos de usuario máximo estimado por bastidor|Bastidor máximo|Almacenamiento de datos de usuario máximo estimado por dispositivo|  
|----------|--------------|------------------------------------------|----------------------------------|------------------------------------------|------------------------------------------------|-----------------|-----------------------------------------------------|  
|HPE|1 TB|16 TB|8|128 TB|320 TB|7|2.240 TB|  
|HPE|2 TB|32 TB|8|256 TB|640 TB|7|4.480 TB|  
|HPE|4 TB|64 TB|8|512 TB|1280 TB|7|8.960 TB|  
|DELL|1 TB|16 TB|9|144 TB|360 TB|6|2.160 TB|  
|DELL|2 TB|32 TB|9|288 TB|720 TB|6|4.320 TB|  
|DELL|4 TB|64 TB|9|576 TB|1440 TB|6|8.640 TB|   
  
Explicación:  
  
-   **El tamaño** de la unidad es de 1, 2 o 4 TB para cada proveedor de hardware.  
  
-   **Almacenamiento de datos físicos por nodo de proceso** = (tamaño de la unidad) * (16 discos por nodo de proceso). Los discos reflejados no se incluyen porque son para redundancia.  
  
-   El **número máximo de nodos de proceso por bastidor** es específico del proveedor de hardware.  
  
-   **Almacenamiento de datos máximo físico por bastidor** = (almacenamiento de datos físico por nodo de proceso) * (máximo de nodos de proceso por bastidor).  
  
-   **Almacenamiento de datos de usuario máximo estimado por bastidor** = (almacenamiento de datos máximo físico por bastidor) * (5 para una relación de compresión 5:1) \* (50% para registros y tempDB). Se trata de una estimación conservadora para los datos de usuario sin comprimir que se pueden cargar y almacenar en el dispositivo. Esta es una estimación y no la aplica el software. El almacenamiento de datos de usuario real depende de los datos y la configuración.  
  
-   El **número máximo de bastidores** es específico para cada proveedor de hardware.  
  
-   **Almacenamiento de datos máximo estimado por dispositivo** = (almacenamiento de datos máximo estimado por bastidor) * (racks máximos). Se trata de una estimación conservadora del tamaño total general de los datos de usuario que se pueden cargar y almacenar en una aplicación totalmente compilada.  
  
