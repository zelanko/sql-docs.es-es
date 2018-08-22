---
title: Configuración del almacenamiento para las tablas con optimización para memoria | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: in-memory-oltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6e005de0-3a77-4b91-b497-14cc0f9f6605
caps.latest.revision: 5
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 48cbee157bf1088ddabbf33a7a6501decd8bdefa
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/16/2018
ms.locfileid: "40393751"
---
# <a name="configuring-storage-for-memory-optimized-tables"></a>Configurar el almacenamiento para las tablas con optimización para memoria
  Debe configurar la capacidad de memoria y las operaciones de entrada/salida por segundo (IOPS).  
  
## <a name="storage-capacity"></a>Capacidad de almacenamiento  
 Use la información de [Estimar los requisitos de memoria para las tablas optimizadas para memoria](memory-optimized-tables.md) para calcular el tamaño en memoria de las tablas durables optimizadas para memoria de la base de datos. Puesto que los índices no se conservan en las tablas optimizadas para memoria, no incluya el tamaño de los índices. Una vez que determine el tamaño, necesita proporcionar una cantidad de espacio en disco que sea cuatro veces el tamaño de tablas durables en memoria.  
  
## <a name="storage-performance"></a>Rendimiento del almacenamiento  
 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] puede aumentar considerablemente el rendimiento de las cargas de trabajo. Por tanto, es importante asegurarse de que la entrada/salida no es un cuello de botella.  
  
-   Al migrar tablas basadas en disco a tablas optimizadas para memoria, asegúrese de que el registro de transacciones esté en un medio de almacenamiento que pueda admitir mayor actividad del registro de transacciones. Por ejemplo, si el medio de almacenamiento admite operaciones del registro de transacciones a 100 MB/s, y las tablas optimizadas para memoria producen un rendimiento cinco veces mayor, el medio de almacenamiento del registro de transacciones debe poder admitir una mejora del rendimiento cinco veces mayor para evitar que la actividad del registro de transacciones se convierta en un cuello de botella.  
  
-   Las tablas con optimización para memoria se conservan en archivos distribuidos en uno o varios contenedores. Cada contenedor se debe asignar normalmente a su propio eje, y se usa tanto para aumentar la capacidad de almacenamiento como para mejorar el rendimiento. Debe asegurarse que la IOPS secuencial del medio de almacenamiento puede admitir que se triplique el rendimiento del registro de transacciones.  
  
     Por ejemplo, si las tablas optimizadas para memoria generan 500MB/s de actividad en el registro de transacciones, el almacenamiento para tablas optimizadas para memoria debe admitir 1,5 GB/seg. La necesidad de admitir un 3 veces aumento de rendimiento registro de transacciones procede de la observación de que los pares de archivos delta y de datos se escriben primero con los datos iniciales y, a continuación, necesitan leer/volver a escribir como parte de una operación de combinación.  
  
     Otro factor que hay que tener en cuenta para el rendimiento del almacenamiento es el tiempo de recuperación de las tablas optimizadas para memoria. Los datos de las tablas durables se deben leer en memoria antes de que una base de datos esté a disposición de las aplicaciones. Normalmente, la carga de datos en las tablas optimizadas para memoria se puede realizar a la velocidad de la IOPS. Por tanto, si el almacenamiento total de las tablas durables optimizadas para memoria es de 60 GB y desea poder cargar estos datos en 1 minuto, la IOPS para el almacenamiento se debe establecer en 1 GB/s.  
  
-   Si tiene número par de ejes, debe crear dos veces el número de contenedores y asignar cada par al mismo eje. Esto es necesario para distribuir la IOPS y el almacenamiento. Para obtener más información, consulte [el Filegroup de memoria optimizada](the-memory-optimized-filegroup.md).  
  
## <a name="see-also"></a>Vea también  
 [Crear y administrar el almacenamiento de objetos con optimización para memoria](creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
