---
title: Cargar datos en almacenamiento de datos paralelos | Microsoft Docs
description: Puede cargar o insertar datos en almacenamiento de datos paralelos de SQL Server (PDW) mediante el uso de la instrucción SQL INSERT, dwloader, utilidad bcp o Integration Services.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: f4551f77b1348ece34dc87dc8abeb91e27290d00
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63183483"
---
# <a name="loading-data-into-parallel-data-warehouse"></a>Cargar datos en almacenamiento de datos paralelos
Puede cargar o insertar datos en almacenamiento de datos paralelos de SQL Server (PDW) mediante el uso de Integration Services, [bcp (utilidad)](../tools/bcp-utility.md), **dwloader** del cargador de la línea de comandos o la instrucción SQL INSERT.  

## <a name="loading-environment"></a>Cargando el entorno  
Para cargar datos, necesita uno o más servidores de carga. Puede usar su propio ETL existente u otros servidores, o puede comprar nuevos servidores. Para obtener más información, consulte [adquirir y configurar un servidor al cargar](acquire-and-configure-loading-server.md). Estas instrucciones incluyen un [hoja de planeamiento de capacidad de cargar Server](loading-server-capacity-planning-worksheet.md) le ayudará a planear la solución adecuada para la carga.  
  
## <a name="load-with-dwloader"></a>Cargar con dwloader  
Mediante el [del cargador de la línea de comandos de dwloader](dwloader.md) es la forma más rápida para cargar datos en PDW.  
  
![Proceso de carga](media/loading-process.png "proceso de carga")  
  
dwloader carga datos directamente a los nodos de proceso sin pasar los datos a través del nodo de Control. Para cargar datos, dwloader en primer lugar se comunica con el nodo de Control para obtener información de contacto para los nodos de proceso. dwloader configura un canal de comunicación con cada nodo de proceso y, a continuación, envía fragmentos de 256KB de datos a los nodos de proceso de forma round robin.  
  
En cada nodo de proceso, el servicio de movimiento de datos (DMS) recibe y procesa los fragmentos de datos. Procesamiento de los datos incluye la conversión de cada fila en formato nativo de SQL Server y calcular el hash de distribución para determinar el nodo de proceso al que pertenece cada fila.  
  
Después de procesar las filas, DMS usa un movimiento de orden aleatorio para cada fila de transferencia para el nodo de proceso correcto y la instancia de SQL Server. Como SQL Server recibe las filas, crea los lotes según la **-b** parámetro de tamaño de lote establecido en dwloader y, a continuación, el lote carga masiva.  

## <a name="load-with-prepared-statements"></a>Cargar con instrucciones preparadas

Puede usar las instrucciones preparadas para cargar datos en tablas replicadas y distribuidas. Cuando los datos de entrada no coincide con el tipo de datos de destino, se realiza una conversión implícita. Las conversiones implícitas compatibles con PDW instrucciones preparadas son un subconjunto de las conversiones compatibles con SQL Server. Es decir, se admiten solo un subconjunto de las conversiones, pero las conversiones compatibles coinciden con las conversiones implícitas de SQL Server. Independientemente de si la tabla de destino que se va a cargar se define como una tabla replicada o distribuida, las conversiones implícitas se aplican (si es necesario) a todas las columnas que existen en la tabla de destino. 

<!-- MISSING LINK
For more information, see [Prepared statements](prepared-statements.md).
-->
  
## <a name="related-tasks"></a>Related Tasks  
  
|Tarea|Descripción|  
|--------|---------------|  
|Crear la base de datos de almacenamiento provisional.|[Crear la base de datos provisional](staging-database.md)|  
|Carga con Integration Services.|[Carga con Integration Services](load-with-ssis.md)|  
|Comprender las conversiones de tipos para dwloader.|[Reglas de conversión de tipos de datos para dwloader](dwloader-data-type-conversion-rules.md)|  
|Carga de datos con dwloader.|[Cargador de la línea de comandos de dwloader](dwloader.md)|  
|Comprender las conversiones de tipos para insertar.|[Carga de datos con INSERT](load-with-insert.md)|  
 
<!-- MISSING LINKS
## See Also  
[Grant permissions to load data](grant-permissions-to-load-data.md)  
[Common metadata query examles](metadata-query-examples.md)  
  
-->
