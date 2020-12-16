---
title: Funcionamiento de los puntos de comprobación para tablas con optimización para memoria | Microsoft Docs
description: Obtenga información sobre los puntos de control en las tablas optimizadas para memoria en SQL Server. La operación de punto de control de la tabla optimizada para memoria es distinta de la de las tablas basadas en disco.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 47975bd5-373f-43cd-946a-da8e8088b610
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8ea64147c8a7bf9f6142b36cb048d7ad39f43b66
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/14/2020
ms.locfileid: "97465396"
---
# <a name="checkpoint-operation-for-memory-optimized-tables"></a>Funcionamiento de los puntos de comprobación para tablas con optimización para memoria
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Es necesario que se produzca un punto de comprobación periódicamente para los datos optimizados para memoria en los archivos delta y de datos para avanzar la parte activa del registro de transacciones. El punto de comprobación permite que las tablas optimizadas para memoria se restauren o se recuperen hasta el último punto de comprobación correcto y después se aplique la parte activa del registro de transacciones para actualizar las tablas optimizadas para memoria al momento dado actual. La operación de punto de comprobación para las tablas basadas en disco y para las tablas optimizadas para memoria es distinta. A continuación se describen los diferentes escenarios y el comportamiento de punto de comprobación para las tablas en disco y para las optimizadas para memoria:  
  
## <a name="manual-checkpoint"></a>Punto de comprobación manual  
 Cuando se emite un punto de comprobación manual, cierra el punto de comprobación tanto para las tablas optimizadas para memoria como para las basadas en disco. El archivo de datos activo se cierra aunque puede estar parcialmente lleno.  
  
## <a name="automatic-checkpoint"></a>Punto de comprobación automático  
 El punto de comprobación automático se implementa de forma distinta para las tablas basadas en disco y las tablas optimizadas para memoria debido a las diferentes formas en que se conservan los datos.  
  
 Para las tablas basadas en disco, se usa un punto de comprobación automático basado en la opción de configuración del intervalo de recuperación (para obtener más información, vea [Cambiar el tiempo de recuperación de destino de una base de datos &#40;SQL Server&#41;](../../relational-databases/logs/change-the-target-recovery-time-of-a-database-sql-server.md)).  
  
 Para las tablas optimizadas para memoria, se usa un punto de comprobación automático cuando el archivo de registro de transacciones supera 1,5 GB desde el último punto de comprobación. Este tamaño de 1,5 GB incluye los registros de transacciones tanto para las tablas optimizadas en memoria como para las basadas en disco.  
  
## <a name="see-also"></a>Consulte también  
 [Crear y administrar el almacenamiento de objetos optimizados para memoria](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
