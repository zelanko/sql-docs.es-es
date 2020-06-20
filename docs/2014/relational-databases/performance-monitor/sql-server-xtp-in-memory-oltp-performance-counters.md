---
title: Contadores de rendimiento de XTP (OLTP en memoria) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: fe3cbaf4-65f4-44c5-acc6-7b735cda0c5d
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 4363a526ada3694e92d18cac0d7abe8a26f6a92f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85016939"
---
# <a name="xtp-in-memory-oltp-performance-counters"></a>Contadores de rendimiento de XTP (OLTP en memoria)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ofrece objetos y contadores que el Monitor de rendimiento puede usar para supervisar la actividad de OLTP en memoria.  
  
##  <a name="xtp-in-memory-oltp-performance-objects"></a><a name="SQLServerPOs"></a>Objetos de rendimiento de XTP (OLTP en memoria)  
 En la tabla siguiente se describen los objetos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Objeto de rendimiento|Descripción|  
|------------------------|-----------------|  
|[Cursores XTP](../cursors.md)|El objeto de rendimiento Cursores XTP contiene contadores relacionados con los cursores internos del motor de XTP. Los cursores son los bloques de creación de bajo nivel que el motor de XTP utiliza para procesar consultas de [!INCLUDE[tsql](../../includes/tsql-md.md)] . Por tanto, el usuario no tiene normalmente control directo sobre ellos.|  
|[Recolección de elementos no utilizados de XTP](sql-server-xtp-garbage-collection.md)|El objeto de rendimiento Recolección de elementos no utilizados de XTP contiene contadores relacionados con el recolector de elementos no utilizados del motor de XTP.|  
|[Procesador fantasma de XTP](sql-server-xtp-phantom-processor.md)|El objeto de rendimiento Procesador fantasma de XTP contiene contadores relacionados con el subsistema de procesamiento fantasma del motor de XTP. Este componente es responsable de detectar filas fantasma en transacciones que se ejecutan en el nivel de aislamiento SERIALIZABLE.|  
|[XTP Storage](sql-server-xtp-storage.md)|El objeto de rendimiento XTP Storage contiene contadores relacionados con el almacenamiento de XTP en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Registro de transacciones XTP](sql-server-xtp-transaction-log.md)|El objeto de rendimiento Registro de transacciones XTP contiene contadores relacionados con el registro de transacciones XTP en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Transacciones XTP](sql-server-xtp-transactions.md)|El objeto de rendimiento Transacciones XTP contiene contadores relacionados con las transacciones del motor de XTP en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
  
