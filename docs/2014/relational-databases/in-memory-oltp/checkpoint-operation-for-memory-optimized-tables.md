---
title: Funcionamiento de los puntos de comprobación para tablas con optimización para memoria | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 47975bd5-373f-43cd-946a-da8e8088b610
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: ddcdec0f624c1d6f70c57e593eaf9da66cbe0419
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63065533"
---
# <a name="checkpoint-operation-for-memory-optimized-tables"></a>Funcionamiento de los puntos de comprobación para tablas con optimización para memoria
  Es necesario que se produzca un punto de comprobación periódicamente para los datos optimizados para memoria en los archivos delta y de datos para avanzar la parte activa del registro de transacciones. El punto de comprobación permite que las tablas optimizadas para memoria se restauren o se recuperen hasta el último punto de comprobación correcto y después se aplique la parte activa del registro de transacciones para actualizar las tablas optimizadas para memoria al momento dado actual. La operación de punto de comprobación para las tablas basadas en disco y para las tablas optimizadas para memoria es distinta. A continuación se describen los diferentes escenarios y el comportamiento de punto de comprobación para las tablas en disco y para las optimizadas para memoria:  
  
## <a name="manual-checkpoint"></a>Punto de comprobación manual  
 Cuando se emite un punto de comprobación manual, cierra el punto de comprobación tanto para las tablas optimizadas para memoria como para las basadas en disco. El archivo de datos activo se cierra aunque puede estar parcialmente lleno.  
  
## <a name="automatic-checkpoint"></a>Punto de comprobación automático  
 El punto de comprobación automático se implementa de forma distinta para las tablas basadas en disco y las tablas optimizadas para memoria debido a las diferentes formas en que se conservan los datos.  
  
 Para las tablas basadas en disco, se usa un punto de comprobación automático basado en la opción de configuración del intervalo de recuperación (para obtener más información, vea [Cambiar el tiempo de recuperación de destino de una base de datos &#40;SQL Server&#41;](../logs/change-the-target-recovery-time-of-a-database-sql-server.md)).  
  
 Para las tablas optimizadas para memoria, se toma un punto de comprobación automático cuando el archivo de registro de transacciones es mayor de 512 MB desde el último punto de comprobación. 512 MB incluye registros de transacciones para tablas tanto basadas en disco y optimizadas para memoria.  
  
## <a name="see-also"></a>Vea también  
 [Crear y administrar el almacenamiento de objetos con optimización para memoria](creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
