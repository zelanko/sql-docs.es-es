---
title: SQL Errors (objeto de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQL Errors object
- SQLServer:SQL Errors
ms.assetid: 6e5273ca-29cb-4618-88a2-70b9b8d6cf76
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f36cd694756544a44df657d97fd84e1967167b55
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63183008"
---
# <a name="sql-server-sql-errors-object"></a>SQL Errors (objeto de SQL Server)
  El objeto **SQLServer: SQL Errors** de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Microsoft proporciona contadores para supervisar los **errores de SQL**.  
  
 En esta tabla se describen los contadores de los [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **errores de SQL** .  
  
|Contadores de errores de SQL de SQL Server|Descripción|  
|------------------------------------|-----------------|  
|**Errores por segundo**|Número de errores/seg.|  
  
 Cada contador del objeto contiene las instancias siguientes:  
  
|Elemento|Definición|  
|----------|----------------|  
|**_Total**|Información sobre todos los errores.|  
|**Errores de base de BD sin conexión**|Hace un seguimiento de los errores graves que hacen que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deje sin conexión la base de datos actual.|  
|**Errores de información**|Información relacionada con los mensajes de error que proporcionan información a los usuarios pero no causan errores.|  
|**Eliminar errores de conexión**|Hace un seguimiento de los errores graves que hacen que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] elimine la conexión actual.|  
|**Errores de usuario**|Información sobre los errores de usuario.|  
  
## <a name="see-also"></a>Consulte también  
 [Supervisar el uso de recursos&#40;Monitor de sistema&#41;](monitor-resource-usage-system-monitor.md)  
  
  
