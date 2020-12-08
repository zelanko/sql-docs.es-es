---
title: SQL Errors (objeto de SQL Server) | Microsoft Docs
description: Obtenga información sobre el objeto SQLServer:SQL Errors, que proporciona contadores para supervisar errores de SQL en SQL Server.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQL Errors object
- SQLServer:SQL Errors
ms.assetid: 6e5273ca-29cb-4618-88a2-70b9b8d6cf76
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: e0433802954301c9ea5a9e483c0e54ca893f6b2d
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505590"
---
# <a name="sql-server-sql-errors-object"></a>SQL Errors (objeto de SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  El objeto **SQLServer:SQL Errors** de Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona contadores para supervisar los **errores de SQL**.  
  
 En esta tabla se describen los contadores de **errores de SQL** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Contadores de errores de SQL de SQL Server|Descripción|  
|------------------------------------|-----------------|  
|**Errores/seg.**|Número de errores/seg.|  
  
 Cada contador del objeto contiene las instancias siguientes:  
  
|Elemento|Definición|  
|----------|----------------|  
|**_Total**|Información sobre todos los errores.|  
|**DB Offline Errors**|Hace un seguimiento de los errores graves que hacen que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deje sin conexión la base de datos actual.|  
|**Info Errors**|Información relacionada con los mensajes de error que proporcionan información a los usuarios pero no causan errores.|  
|**Kill Connection Errors**|Hace un seguimiento de los errores graves que hacen que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] elimine la conexión actual.|  
|**User Errors**|Información sobre los errores de usuario.|  
  
## <a name="see-also"></a>Consulte también  
 [Supervisar el uso de recursos&#40;Monitor de sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
