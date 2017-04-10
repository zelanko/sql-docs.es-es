---
title: "MSSQL_ENG014121 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "error MSSQL_ENG014121"
ms.assetid: c8595854-cce1-4566-ad64-d565555caded
caps.latest.revision: 13
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 13
---
# MSSQL_ENG014121
    
## Detalles del mensaje  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|14121|  
|Origen del evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nombre simbólico||  
|Texto del mensaje|No se pudo quitar el distribuidor '%s'. Tiene asociadas bases de datos de distribución.|  
  
## Explicación  
 No se puede quitar una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configurada como distribuidor del rol de distribuidor porque hay bases de datos de distribución asociadas con esa instancia. Este error se produce si intenta quitar una base de datos de distribución que está asociada a uno o más publicadores.  
  
## Acción del usuario  
 Para encontrar los nombres de algunos publicadores y las bases de datos de distribución asociadas a este distribuidor, ejecute [sp_helpdistpublisher & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md) desde cualquier base de datos en el distribuidor.  
  
 Ejecutar [sp_dropdistributiondb & #40; Transact-SQL & #41;](../../relational-databases/system-stored-procedures/sp-dropdistributiondb-transact-sql.md) para las bases de datos de distribución asociadas con este distribuidor. Cuando haya quitado todas las asociaciones con bases de datos de distribución, puede deshabilitar la distribución.  
  
## Vea también  
 [Errores y eventos referencia & #40; Replicación y nº 41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [Configurar la distribución](../../relational-databases/replication/configure-distribution.md)  
  
  