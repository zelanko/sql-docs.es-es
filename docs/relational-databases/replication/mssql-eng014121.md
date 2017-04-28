---
title: MSSQL_ENG014121 | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MSSQL_ENG014121 error
ms.assetid: c8595854-cce1-4566-ad64-d565555caded
caps.latest.revision: 13
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2a8972728183fff1e679063cf48e1e20cd7b5089
ms.lasthandoff: 04/11/2017

---
# <a name="mssqleng014121"></a>MSSQL_ENG014121
    
## <a name="message-details"></a>Detalles del mensaje  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|14121|  
|Origen del evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nombre simbólico||  
|Texto del mensaje|No se pudo quitar el distribuidor '%s'. Tiene asociadas bases de datos de distribución.|  
  
## <a name="explanation"></a>Explicación  
 No se puede quitar una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configurada como distribuidor del rol de distribuidor porque hay bases de datos de distribución asociadas con esa instancia. Este error se produce si intenta quitar una base de datos de distribución que está asociada a uno o más publicadores.  
  
## <a name="user-action"></a>Acción del usuario  
 Para buscar los nombres de todos los publicadores y bases de datos de distribución asociados a este distribuidor, ejecute [sp_helpdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md) desde cualquier base de datos del distribuidor.  
  
 Ejecute [sp_dropdistributiondb &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropdistributiondb-transact-sql.md) para todas las bases de datos de distribución asociadas con este distribuidor. Cuando haya quitado todas las asociaciones con bases de datos de distribución, puede deshabilitar la distribución.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de errores y eventos &#40;replicación&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [Configurar la distribución](../../relational-databases/replication/configure-distribution.md)  
  
  
