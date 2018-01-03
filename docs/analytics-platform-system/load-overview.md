---
title: Cargar
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: 
ms.technology: mpp-data-warehouse
description: "Puede cargar o insertar datos en almacenamiento de datos paralelos de SQL Server (PDW) mediante el uso de Integration Services, utilidad bcp, dwloader o la instrucción SQL INSERT."
ms.date: 10/20/2016
ms.topic: article
ms.assetid: c7292108-4a48-409e-b0f4-e4ba84dce26f
caps.latest.revision: "22"
ms.openlocfilehash: be5ea7c2b939b58c7dfd826965f1568431cb1bff
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="load-sql-server-pdw"></a>Carga (SQL Server PDW)
Puede cargar o insertar datos en almacenamiento de datos paralelos de SQL Server (PDW) mediante el uso de servicios de integración, [bcp (utilidad)](../tools/bcp-utility.md), **dwloader** cargador de línea de comandos o la instrucción SQL INSERT.  

## <a name="loading-environment"></a>Entorno de carga  
Para cargar datos, tendrá que uno o más servidores de carga. Puede usar su propio ETL existente u otros servidores, o puede comprar nuevos servidores. Para obtener más información, consulte [adquirir y configurar un servidor de carga](acquire-and-configure-loading-server.md). Estas instrucciones incluyen un [hoja de planeamiento de capacidad de carga de servidor](loading-server-capacity-planning-worksheet.md) le ayudará a planear la solución adecuada para la carga.  
  
## <a name="load-with-dwloader"></a>Cargar con dwloader  
Mediante el [dwloader cargador de línea de comandos](dwloader.md) es la forma más rápida para cargar datos en PDW.  
  
![Proceso de carga](media/loading-process.png "proceso de carga")  
  
dwloader carga los datos directamente a los nodos de proceso sin pasar los datos a través del nodo de Control. Para cargar datos, dwloader en primer lugar se comunica con el nodo de Control para obtener información de contacto para los nodos de proceso. dwloader configura un canal de comunicación con cada nodo de cálculo y, a continuación, envía fragmentos de 256KB de datos a los nodos de proceso en un comportamiento por turnos inmediatamente.  
  
En cada nodo de proceso, servicio de movimiento de datos (DMS) recibe y procesa los fragmentos de datos. Procesamiento de los datos incluye la conversión de cada fila en formato nativo de SQL Server y calcular el hash de distribución para determinar el nodo de proceso al que pertenece cada fila.  
  
Después de procesar las filas, DMS utiliza un movimiento de forma aleatoria para transferir cada fila en el nodo de proceso correcto y la instancia de SQL Server. A medida que SQL Server recibe las filas, crea los lotes según la **– b** parámetro tamaño de lote se establece en dwloader y, a continuación, carga el lote de forma masiva.  

## <a name="load-with-prepared-statements"></a>Cargar con instrucciones preparadas

Puede utilizar instrucciones preparadas para cargar datos en tablas replicadas y distribuidas. Cuando los datos de entrada no coincide con el tipo de datos de destino, se realiza una conversión implícita. Las conversiones implícitas compatibles con PDW instrucciones preparadas son un subconjunto de las conversiones compatibles con SQL Server. Es decir, se admiten solo un subconjunto de las conversiones, pero las conversiones compatibles coincide con las conversiones implícitas de SQL Server. Independientemente de si la tabla de destino que se va a cargar se define como una tabla replicada o distribuida, las conversiones implícitas se aplican (si es necesario) a todas las columnas que existen en la tabla de destino. 

<!-- MISSING LINK
For more information, see [Prepared statements](prepared-statements.md).
-->
  
## <a name="related-tasks"></a>Related Tasks  
  
|Tarea|Description|  
|--------|---------------|  
|Crear la base de datos de almacenamiento provisional.|[Crear la base de datos de almacenamiento provisional](staging-database.md)|  
|Carga con Integration Services.|[Carga con Integration Services](load-with-ssis.md)|  
|Comprender las conversiones de tipo para dwloader.|[Reglas de conversión de tipos de datos para dwloader](dwloader-data-type-conversion-rules.md)|  
|Carga los datos con dwloader.|[Cargador de la línea de comandos de dwloader](dwloader.md)|  
|Comprender las conversiones de tipo para la INSERCIÓN.|[Carga de datos con INSERT](load-with-insert.md)|  
 
<!-- MISSING LINKS
## See Also  
[Grant permissions to load data](grant-permissions-to-load-data.md)  
[Common metadata query examles](metadata-query-examples.md)  
  
-->
