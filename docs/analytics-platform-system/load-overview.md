---
title: Carga de datos
description: Puede cargar o insertar datos en SQL Server almacenamiento de datos paralelos (PDW) mediante Integration Services, la utilidad BCP, dwloader o la instrucción INSERT de SQL.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: fd161820fd53d45642848697bce9589a98dec4ca
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401045"
---
# <a name="loading-data-into-parallel-data-warehouse"></a>Cargar datos en almacenamiento de datos paralelos
Puede cargar o insertar datos en SQL Server almacenamiento de datos paralelos (PDW) mediante Integration Services, la [utilidad BCP](../tools/bcp-utility.md), el cargador de línea de comandos **dwloader** o la instrucción INSERT de SQL.  

## <a name="loading-environment"></a>Cargando entorno  
Para cargar datos, necesita uno o más servidores de carga. Puede usar su propio ETL existente u otros servidores, o puede adquirir nuevos servidores. Para obtener más información, vea [adquirir y configurar un servidor de carga](acquire-and-configure-loading-server.md). Estas instrucciones incluyen una [hoja de cálculo de planeamiento](loading-server-capacity-planning-worksheet.md) de la capacidad del servidor de carga para ayudarle a planear la solución adecuada para la carga.  
  
## <a name="load-with-dwloader"></a>Carga con dwloader  
Usar el [cargador de línea de comandos dwloader](dwloader.md) es la forma más rápida de cargar datos en PDW.  
  
![Proceso de carga](media/loading-process.png "Cargando proceso")  
  
dwloader carga los datos directamente en los nodos de proceso sin pasar los datos a través del nodo de control. Para cargar datos, dwloader primero se comunica con el nodo de control para obtener información de contacto para los nodos de proceso. dwloader configura un canal de comunicación con cada nodo de proceso y, a continuación, envía fragmentos de datos de 256 KB a los nodos de proceso de manera Round Robin.  
  
En cada nodo de proceso, el servicio de movimiento de datos (DMS) recibe y procesa los fragmentos de datos. El procesamiento de los datos incluye la conversión de cada fila en SQL Server formato nativo y el cálculo del hash de distribución para determinar el nodo de proceso al que pertenece cada fila.  
  
Después de procesar las filas, DMS usa un movimiento de orden aleatorio para transferir cada fila al nodo de proceso y la instancia de SQL Server correctos. Como SQL Server recibe las filas, las procesa por lotes según el parámetro de tamaño de lote **-b** establecido en dwloader y, a continuación, carga de forma masiva el lote.  

## <a name="load-with-prepared-statements"></a>Cargar con instrucciones preparadas

Puede usar instrucciones preparadas para cargar datos en tablas distribuidas y replicadas. Cuando los datos de entrada no coinciden con el tipo de datos de destino, se realiza una conversión implícita. Las conversiones implícitas admitidas por las instrucciones preparadas de PDW son un subconjunto de conversiones admitidas por SQL Server. Es decir, solo se admite un subconjunto de conversiones, pero las conversiones admitidas coinciden SQL Server conversiones implícitas. Independientemente de si la tabla de destino que se va a cargar se define como una tabla distribuida o replicada, se aplican las conversiones implícitas (si es necesario) a todas las columnas que existen en la tabla de destino. 

<!-- MISSING LINK
For more information, see [Prepared statements](prepared-statements.md).
-->
  
## <a name="related-tasks"></a>Related Tasks  
  
|Tarea|Descripción|  
|--------|---------------|  
|Crear la base de datos de ensayo.|[Crear la base de datos de ensayo](staging-database.md)|  
|Cargue con Integration Services.|[Carga con Integration Services](load-with-ssis.md)|  
|Comprenda las conversiones de tipos para dwloader.|[Reglas de conversión de tipos de datos para dwloader](dwloader-data-type-conversion-rules.md)|  
|Carga de datos con dwloader.|[Cargador de línea de comandos de dwloader](dwloader.md)|  
|Comprender las conversiones de tipos de INSERT.|[Carga de datos con INSERT](load-with-insert.md)|  
 
<!-- MISSING LINKS
## See Also  
[Grant permissions to load data](grant-permissions-to-load-data.md)  
[Common metadata query examles](metadata-query-examples.md)  
  
-->
