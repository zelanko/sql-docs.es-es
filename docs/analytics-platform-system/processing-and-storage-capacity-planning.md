---
title: Capacidad de procesamiento y almacenamiento - Analytics Platform System | Documentos de Microsoft
description: Los requisitos empresariales determinan el número de unidades de escala de datos y el tamaño de los discos de nodo de proceso que necesite en su dispositivo Analytics Platform System (APS).
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: f552372ac108d219ad410b88ec9911ecaea63ab3
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/19/2018
ms.locfileid: "31539605"
---
# <a name="processing-and-storage-capacity-in-analytics-platform-system"></a>Capacidad de procesamiento y el almacenamiento en el sistema de la plataforma de análisis
Los requisitos empresariales determinan el número de unidades de escala de datos y el tamaño de los discos de nodo de proceso que necesite en su dispositivo Analytics Platform System (APS). Utilice estos cálculos de procesamiento y almacenamiento para guiar la capacidad de compra y decisiones de planeación.  
  
  
## <a name="section1"></a>Planeación de la capacidad de procesamiento  
Rendimiento de las consultas de almacenamiento de datos paralelos de SQL Server (PDW) depende en gran medida del número de núcleos de CPU funciona en los datos en paralelo. Dentro de los límites, aumentar el paralelismo mejora el rendimiento de las consultas de procesamiento paralelo masivo (MPP). Incluso si el tamaño de los datos es relativamente pequeño, la potencia del motor de consulta MPP de se ha mejorado al tener mayor paralelismo.  
  
Por ejemplo, un dispositivo con 12 nodos de ejecución tiene 192 núcleos de CPU que procesan los datos en paralelo. Así es 192 forma paralelismo. Un dispositivo con 56 nodos de proceso tiene 896 núcleos todas funcionan en paralelo. Esta magnitud de paralelismo no es factible sin MPP informática.  
  
A medida que aumenta el número de nodos de proceso, el escalado de la aplicación, es necesario agregar más de un nodo de proceso a la vez para obtener una mejora apreciable. Los proveedores de hardware admiten determinadas configuraciones de unidades de escala de datos para asegurarse de que la ventaja de ajuste de escala en el dispositivo supera con creces el costo de redistribución de los datos a través de varios nodos de cálculo.  
  
### <a name="data-scale-unit-configuration-examples---hpe"></a>Ejemplos de configuración de unidad de escala de datos - HPE  
Estos son ejemplos de las configuraciones admitidas de HPE para Uunits de escala de datos. Se pueden variar de las configuraciones admitidas más recientes, pero se proporciona como un ejemplo de cómo aumentar la capacidad en aproximadamente un 20 por ciento.  
  
Aumento en el nivel es el aumento de porcentaje de capacidad aumentando el Uunits de escala de datos de una fila a la siguiente. Por ejemplo, aumentar las unidades de escala de datos de 6 a 8 ofrece un aumento de un 33% de núcleos de CPU y memoria.  También aumenta el espacio en disco que no está incluido en esta tabla.  
  
|Unidades de escala de datos|Nodos de proceso|Núcleos de CPU|Memoria (GB)|Elevar|  
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
  
-   **Unidades de escala de datos** por dispositivo. Para obtener información acerca de las unidades de escala de datos, vea [componentes de Hardware del sistema de plataforma de análisis](hardware-components.md).  
  
-   **Nodos de proceso** por dispositivo.  
  
-   **Núcleos de CPU** por dispositivo. Hay 16 núcleos por nodo de proceso, un núcleo por cada par de disco reflejado. Para la estructura de disco de nodo de proceso, consulte [componentes de Hardware del sistema de plataforma de análisis](hardware-components.md).  
  
-   **Memoria** por dispositivo. Cada núcleo tiene 256 GB de memoria.  
  
### <a name="data-scale-unit-configuration-examples--dell-quanta"></a>Ejemplos de configuración de un unidad datos escala: Dell, Quanta  
Estos son ejemplos de las configuraciones admitidas de Dell y cuantos para Uunits de escala de datos. Se pueden variar de las configuraciones admitidas más recientes, pero se proporciona como un ejemplo de cómo aumentar la capacidad en aproximadamente un 20 por ciento.  
  
Aumento en el nivel es el aumento de porcentaje de capacidad aumentando el Uunits de escala de datos de una fila a la siguiente. Por ejemplo, aumentar las unidades de escala de datos de 6 a 8 ofrece un aumento de un 33% de núcleos de CPU y memoria. También aumenta el espacio en disco que no está incluido en esta tabla.  
  
|Unidades de escala de datos|Nodos de proceso|Núcleos de CPU|Memoria (GB)|Elevar|  
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
Esta tabla se estima que puede cargar y almacenar hasta 6 petabytes de datos sin comprimir en un dispositivo de sistema de la plataforma de análisis totalmente integrado. 
  
|Fabricante|Tamaño de la unidad|Nodo de cada proceso de almacenamiento de datos físicos|Nodos de proceso máximos por bastidor|Almacenamiento de datos máximo físicos por bastidor|Almacenamiento de datos de número máximo de usuarios por bastidor de estimado|Racks máximos|Calcula el almacenamiento de datos de número máximo de usuarios por cada dispositivo.|  
|----------|--------------|------------------------------------------|----------------------------------|------------------------------------------|------------------------------------------------|-----------------|-----------------------------------------------------|  
|HPE|1 TB|16 TB|8|128 TB|320 TB|7|2,240 TB|  
|HPE|2 TB|32 TB|8|256 TB|640 TB|7|4,480 TB|  
|HPE|3 TB|48 TB|8|384 TB|960 TB|7|6,720 TB|  
|DELL|1 TB|16 TB|9|144 TB|360 TB|6|ENTORNO A 2.160 TB|  
|DELL|2 TB|32 TB|9|288 TB|720 TB|6|4.320 TB|  
|DELL|3 TB|48 TB|9|432 TB|1080 TB|6|6,480 TB|  
  
Explicación:  
  
-   **Tamaño de la unidad** es 1, 2 ó 3 TB para cada proveedor de Hardware.  
  
-   **Almacenamiento de datos físicos por nodo de proceso** = (tamaño de unidad) * (16 discos por nodo de proceso). No se incluyen los discos reflejados ya que son para redundancia.  
  
-   **Nodos de proceso máxima por bastidor** es específico del proveedor de hardware.  
  
-   **Almacenamiento de datos máximo físicos por bastidor** = (almacenamiento de datos físicos por nodo de proceso) * (nodos de proceso máxima por cada bastidor).  
  
-   **Calcula el almacenamiento de datos de número máximo de usuarios por bastidor** = (almacenamiento de datos máximo físicos por bastidor) * (5 para una razón de compresión de 5:1) \* (50% para los registros y tempDB). Se trata de un cálculo moderado para los datos de usuario sin comprimir que se pueden cargar y almacenar en el dispositivo. Esto es una estimación y no se aplica por software. El almacenamiento de datos de usuario real depende de los datos y su configuración.  
  
-   **Racks máximos** es específica para cada proveedor de Hardware.  
  
-   **Calcula el almacenamiento de datos máximo por dispositivo** = (almacenamiento de datos máximo estimado por bastidor) * (racks máximo). Se trata de un cálculo moderado del tamaño total general de los datos de usuario que puede cargar y almacenar en un dispositivo totalmente integrado.  
  
