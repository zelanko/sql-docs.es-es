---
title: Características en desuso de Master Data Services en SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: master-data-services
ms.topic: conceptual
ms.assetid: d8506bda-66dd-45a4-bfc9-3a10fa665acc
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 5c6b7ce5d878969079883abd55e935c8e9c16024
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62925076"
---
# <a name="deprecated-master-data-services-features-in-sql-server-2014"></a>Características desusadas de Master Data Services en SQL Server 2014
  Este tema describe las características desusadas de [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] que siguen estando disponibles en [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]. Está previsto quitar estas características en una futura versión de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Las características en desuso no se deben usar en nuevas aplicaciones.  
  
## <a name="staging-process"></a>Proceso de almacenamiento provisional  
 El proceso de almacenamiento provisional que se empleaba en [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] ya no está disponible en la aplicación web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)]; sin embargo, todavía está disponible en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
 Los errores del proceso de almacenamiento provisional de [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] ya no se muestran en la interfaz de usuario. Códigos de error que se rellenan durante el proceso de almacenamiento provisional siguen estando disponibles en las tablas de ensayo y se pueden encontrar aquí: [ https://msdn.microsoft.com/library/ff487022.aspx ](https://msdn.microsoft.com/library/ff487022.aspx).  
  
 Las tablas de ensayo (tblStgMember, tblStgMemberAttribute y tblStgRelationship) siguen estando disponibles en la base de datos. El procedimiento almacenado usado para iniciar el proceso de almacenamiento provisional (mdm.udpStagingSweep) sigue estando disponible en la base de datos.  
  
 Los métodos de servicio web que llaman al proceso de almacenamiento provisional siguen estando disponibles.  
  
 El intervalo de almacenamiento provisional establecido en [!INCLUDE[ssMDScfgmgr](../includes/ssmdscfgmgr-md.md)] se aplica al proceso de almacenamiento provisional tanto en [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] como en [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)].  
  
 En [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] se ha implementado un proceso de almacenamiento temporal nuevo y de mayor rendimiento. Para más información, vea [Importación de datos &#40;Master Data Services&#41;](overview-importing-data-from-tables-master-data-services.md).  
  
## <a name="metadata"></a>Metadatos  
 Aunque el modelo metadatos se sigue mostrando en la aplicación web [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)], no debe usarse. Se quitará en una versión futura. Los usuarios también pueden ver ya metadatos en el **Explorer** área funcional y ya no puede crear versiones del modelo de metadatos.  
  
## <a name="see-also"></a>Vea también  
 [Características descontinuadas de Master Data Services en SQL Server 2014](discontinued-master-data-services-features.md)  
  
  
