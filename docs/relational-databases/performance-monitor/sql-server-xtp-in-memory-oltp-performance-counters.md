---
title: Contadores de rendimiento de XTP (OLTP en memoria) de SQL Server | Microsoft Docs
ms.custom: 
ms.date: 04/06/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fe3cbaf4-65f4-44c5-acc6-7b735cda0c5d
caps.latest.revision: 17
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: c4fb8ea7bd2ca4a09f0758c175b9eb2781f2ed5b
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-xtp-in-memory-oltp-performance-counters"></a>Contadores de rendimiento de XTP (OLTP en memoria) de SQL Server
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ofrece objetos y contadores que el Monitor de rendimiento puede usar para supervisar la actividad de OLTP en memoria. Los objetos y los contadores se comparten entre todas las instancias de una versión concreta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el equipo, a partir de [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].  
  
 Antes, los nombres de los objetos y los contadores contenían *XTP*, como en **Cursores XTP**. A partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], los nombres siguen este patrón:  
  
-   **SQL Server** *\<versión>* **Cursores XTP**  
  
 Para *\<versión*, el valor es similar a 2016.  
  
##  <a name="SQLServerPOs"></a> Objetos de rendimiento de SQL Server XTP  
 En la tabla siguiente se describen los objetos de rendimiento de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Objeto de rendimiento|Description|  
|------------------------|-----------------|  
|[Cursores SQL Server XTP](../../relational-databases/performance-monitor/sql-server-xtp-cursors.md)|El objeto de rendimiento Cursores XTP de SQL Server contiene contadores relacionados con los cursores internos del motor OLTP en memoria. Los cursores son los bloques de creación de bajo nivel que usa el motor OLTP en memoria para procesar consultas de [!INCLUDE[tsql](../../includes/tsql-md.md)] . Por tanto, el usuario no tiene normalmente control directo sobre ellos.|  
|[SQL Server XTP Databases](../../relational-databases/performance-monitor/sql-server-xtp-databases.md)|El objeto de rendimiento SQL Server XTP Databases contiene contadores relacionados con las bases de datos del motor OLTP en memoria.|  
|[Recolección de elementos no utilizados de XTP de SQL Server](../../relational-databases/performance-monitor/sql-server-xtp-garbage-collection.md)|El objeto de rendimiento Recolección de elementos no utilizados de XTP de SQL Server contiene contadores relacionados con el recolector de elementos no utilizados del motor OLTP en memoria.|  
|[SQL Server 2016 XTP IO Governor](../../relational-databases/performance-monitor/sql-server-xtp-io-governor.md)|El objeto de rendimiento SQL Server XTP IO Governor contiene contadores relacionados con el regulador de frecuencia de E/S OLPT en memoria.|
|[Procesador fantasma de XTP de SQL Server](../../relational-databases/performance-monitor/sql-server-xtp-phantom-processor.md)|El objeto de rendimiento Procesador fantasma de XTP de SQL Server contiene contadores relacionados con el subsistema de procesamiento fantasma del motor de OLTP en memoria. Este componente es responsable de detectar filas fantasma en transacciones que se ejecutan en el nivel de aislamiento SERIALIZABLE.|  
|[XTP Storage de SQL Server](../../relational-databases/performance-monitor/sql-server-xtp-storage.md)|El objeto de rendimiento Almacenamiento de XTP de SQL Server contiene contadores relacionados con el almacenamiento OLTP en memoria de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Registro de transacciones XTP de SQL Server](../../relational-databases/performance-monitor/sql-server-xtp-transaction-log.md)|El objeto de rendimiento Registro de transacciones XTP de SQL Server contiene contadores relacionados con el registro de transacciones OLTP en memoria de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[Transacciones XTP de SQL Server](../../relational-databases/performance-monitor/sql-server-xtp-transactions.md)|El objeto de rendimiento Transacciones XTP de SQL Server contiene contadores relacionados con las transacciones del motor OLTP en memoria de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
  
  

