---
title: Capacidad de procesamiento y almacenamiento - Analytics Platform System | Microsoft Docs
description: Sus requisitos empresariales determinan el número de unidades de escalado de datos y el tamaño de los discos del nodo de proceso que necesite en su aplicación Analytics Platform System (APS).
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 7188ace65e31d92cc5acfdc684457b219836d2d1
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52527800"
---
# <a name="processing-and-storage-capacity-in-analytics-platform-system"></a>Capacidad de procesamiento y almacenamiento en Analytics Platform System
Sus requisitos empresariales determinan el número de unidades de escalado de datos y el tamaño de los discos del nodo de proceso que necesite en su aplicación Analytics Platform System (APS). Use estos cálculos de almacenamiento y procesamiento para guiar la capacidad de adquisición y planeación de decisiones.  
  
  
## <a name="section1"></a>Planeación de capacidad de procesamiento  
Rendimiento de las consultas de almacenamiento de datos paralelos de SQL Server (PDW) depende en gran medida del número de núcleos de CPU funciona en los datos en paralelo. Dentro de límites, aumenta el paralelismo, mejora el rendimiento de consulta de procesamiento paralelo masivo (MPP). Incluso si el tamaño de los datos es relativamente pequeño, la potencia del motor de consultas MPP se mejora al tener mayor paralelismo.  
  
Por ejemplo, un dispositivo con 12 nodos de proceso tiene 192 núcleos de CPU que procesan los datos en paralelo. Eso es 192 forma paralelismo. Un dispositivo con 56 nodos de proceso tiene 896 núcleos todos trabajan en paralelo. Esta magnitud de paralelismo no es factible sin MPP informática.  
  
A medida que aumenta el número de nodos de proceso, escalar horizontalmente el dispositivo requiere la adición de más de un nodo de proceso en un momento para obtener una ventaja evidente. Los proveedores de hardware admiten configuraciones específicas solo escalado de unidades de datos para asegurarse de que la ventaja de escalar la aplicación supera el coste de redistribución de los datos entre más nodos de proceso.  
  
### <a name="data-scale-unit-configuration-examples---hpe"></a>Ejemplos de configuración de unidad de escalado de datos - HPE  
Estos son algunos ejemplos de las configuraciones admitidas de HPE para Uunits de escalado de datos. Estos pueden variar con respecto a las configuraciones admitidas más recientes, pero se proporcionan como un ejemplo de cómo aumentar la capacidad en aproximadamente un 20 por ciento.  
  
Aumento de precios es el aumento de porcentaje de capacidad aumentando el Uunits de escala de datos de una fila a la siguiente. Por ejemplo, aumentar las unidades de escala de datos de 6 a 8 ofrece un aumento del 33% en la memoria y núcleos de CPU.  También aumenta el espacio en disco que no se muestra en esta tabla.  
  
|Unidades de escalado de datos|Nodos de proceso|Núcleos de CPU|Memoria (GB)|Aumento de precios|  
|--------------------|-----------------|-------------|-----------------|----------|  
|1|2|32|512|-|  
|2|4|64|1024|100%|  
|3|6|96|1536|50%|  
|4|8|128|2048|33%|  
|5|10|160|2560|25%|  
|6|12|192|3072|20%|  
|8|16|256|4096|33%|  
|10|20|320|5120|25%|  
|12|24|384|6144|20%|  
|16|32|512|8192|33%|  
|20|40|640|10240|25%|  
|24|48|768|12288|20%|  
|28|56|896|14336|17%|  
  
Explicación:  
  
-   **Las unidades de escalado de datos** por dispositivo. Para obtener información acerca de las unidades de escala de datos, vea [componentes de Hardware de Analytics Platform System](hardware-components.md).  
  
-   **Nodos de proceso** por dispositivo.  
  
-   **Núcleos de CPU** por dispositivo. Hay 16 núcleos por nodo de proceso, un núcleo por cada par de disco reflejado. Para la estructura de disco de nodo de proceso, consulte [componentes de Hardware de Analytics Platform System](hardware-components.md).  
  
-   **Memoria** por dispositivo. Cada núcleo tiene 256 GB de memoria.  
  
### <a name="data-scale-unit-configuration-examples---dell-quanta"></a>Ejemplos configuración de unidad de escala datos - Dell, cuantos  
Estos son algunos ejemplos de las configuraciones admitidas de Dell y cuantos para Uunits de escalado de datos. Estos pueden variar con respecto a las configuraciones admitidas más recientes, pero se proporcionan como un ejemplo de cómo aumentar la capacidad en aproximadamente un 20 por ciento.  
  
Aumento de precios es el aumento de porcentaje de capacidad aumentando el Uunits de escala de datos de una fila a la siguiente. Por ejemplo, aumentar las unidades de escala de datos de 6 a 8 ofrece un aumento del 33% en la memoria y núcleos de CPU. También aumenta el espacio en disco que no se muestra en esta tabla.  
  
|Unidades de escalado de datos|Nodos de proceso|Núcleos de CPU|Memoria (GB)|Aumento de precios|  
|--------------------|-----------------|-------------|-----------------|----------|  
|1|3|48|768|-|  
|2|6|96|1536|100%|  
|3|9|144|2,304|50%|  
|4|12|192|3,072|33%|  
|5|15|240|3,840|25%|  
|6|18|288|4,608|20%|  
|7|21|336|5,376|17%|  
|8|24|384|6,144|14%|  
|9|27|432|6,912|13%|  
|12|36|576|9,216|33%|  
|15|45|720|11,520|25%|  
|18|54|864|13,824|20%|  
  
## <a name="section2"></a>Planear la capacidad de almacenamiento  
Esta tabla se estima que puede cargar y almacenar hasta 6 petabytes de datos sin comprimir en un dispositivo de Analytics Platform System totalmente integrado. 
  
|Fabricante|Tamaño de la unidad|Nodo por proceso de almacenamiento de datos físicos|Nodos de proceso máxima por bastidor|Almacenamiento de datos máximo físicos por bastidor|Calcula el almacenamiento de datos máximo por bastidor|Bastidores máximos|Calcula el almacenamiento de datos máximo por cada dispositivo.|  
|----------|--------------|------------------------------------------|----------------------------------|------------------------------------------|------------------------------------------------|-----------------|-----------------------------------------------------|  
|HPE|1 TB|16 TB|8|128 TB|320 TB|7|2,240 TB|  
|HPE|2 TB|32 TB|8|256 TB|640 TB|7|4,480 TB|  
|HPE|3 TB|48 TB|8|384 TB|960 TB|7|6,720 TB|  
|DELL|1 TB|16 TB|9|144 TB|360 TB|6|2.160 TB|  
|DELL|2 TB|32 TB|9|288 TB|720 TB|6|4.320 TB|  
|DELL|3 TB|48 TB|9|432 TB|1080 TB|6|6,480 TB|  
  
Explicación:  
  
-   **Tamaño de la unidad** es 1, 2 o 3 TB para cada proveedor de Hardware.  
  
-   **Almacenamiento de datos físicos por nodo de proceso** = (tamaño de unidad) * (16 discos por nodo de proceso). No se incluyen los discos reflejados, ya que son para la redundancia.  
  
-   **Nodos de proceso máxima por bastidor** es específico del proveedor de hardware.  
  
-   **Almacenamiento de datos máximo físicos por bastidor** = (almacenamiento de datos físicos por nodo de proceso) * (nodos de proceso máxima por bastidor).  
  
-   **Calcula el almacenamiento de datos máximo por bastidor** = (almacenamiento de datos máximo físicos por bastidor) * (5 para una relación de compresión de 5:1) \* (50% para los registros y tempDB). Se trata de una estimación conservadora para los datos de usuario sin comprimir que se pueden cargar y almacenar en el dispositivo. Esto es una estimación y no se aplica mediante software. El almacenamiento de datos de usuario real depende de los datos y la configuración.  
  
-   **Máximos bastidores** es específico para cada proveedor de Hardware.  
  
-   **Calcula el almacenamiento de datos máximo por dispositivo** = (almacenamiento de datos máximo estimado por bastidor) * (racks máximo). Se trata de un cálculo moderado del tamaño total general de los datos de usuario que puede cargar y almacenar en un dispositivo totalmente integrado.  
  
