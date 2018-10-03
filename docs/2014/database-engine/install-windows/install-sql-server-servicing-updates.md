---
title: Instalar actualizaciones de servicio de SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 7d6c962b-c8d0-49f7-a2ac-00ad8dca930a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5c6d4165cc0cdedbef073ba950366265f4699d1f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48087145"
---
# <a name="install-sql-server-2014-servicing-updates"></a>Instalar actualizaciones de servicio de SQL Server 2014
  Este tema proporciona información acerca de cómo instalar actualizaciones para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Esta sección proporciona información acerca de lo siguiente:  
  
-   Instalar actualizaciones para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] durante una nueva instalación  
  
-   Instalar actualizaciones para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] una vez instalado.  
  
 Se recomienda que los clientes evalúen e instalen las últimas actualizaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puntualmente para asegurarse de que los sistemas están al día con las actualizaciones de seguridad más recientes.  
  
## <a name="installing-updates-for-includesscurrentincludessscurrent-mdmd-during-a-new-installation"></a>Instalar actualizaciones para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] durante una nueva instalación  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] integra las últimas actualizaciones del producto con la instalación del producto principal, de modo que el producto principal y las actualizaciones aplicables se instalen al mismo tiempo. La actualización del producto puede buscar actualizaciones aplicables en:  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update  
  
-   Windows Server Update Services (WSUS)  
  
-   Una carpeta local  
  
-   Un recurso compartido de red  
  
 Una vez que el programa de instalación encuentra las versiones más recientes de las actualizaciones aplicables, las descarga y las integra con el proceso de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] actual. La actualización del producto puede incluir una actualización acumulativa, un Service Pack o un Service Pack más la actualización acumulativa. Funcionalidad de actualización de producto es una extensión de la [funcionalidad de instalación integrada](http://go.microsoft.com/fwlink/?LinkId=219945) que estaba disponible en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] PCU1.  
  
## <a name="installing-updates-for-includesscurrentincludessscurrent-mdmd-after-it-has-already-been-installed"></a>Instalar actualizaciones para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] una vez instalado  
 En una instancia instalada de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], recomendamos que aplique todas las actualizaciones disponibles: las versiones de distribución General (GDR - las actualizaciones de seguridad y crítico), Service Packs (SP), así como la más reciente disponible actualización acumulativa (CU).  
  
 Según el tipo de versión de mantenimiento, actualizaciones de SQL Server están disponibles a través de Microsoft Update (MU), Microsoft Download Center o la revisión de los servicios de soporte técnico al cliente servidor. Las actualizaciones críticas y de seguridad para SQL Server se proporcionan automáticamente por Microsoft Update (para poder ver estas actualizaciones que necesita para participar en Microsoft Update a través de Windows Update en el panel de Control). Service Packs están disponibles en Microsoft Update como descarga opcional/importante, así como el centro de descarga. Las actualizaciones acumulativas están disponibles en el servidor de descarga de revisión de Microsoft proporcionado en artículos de Knowledge Base de CU.  
  
## <a name="see-also"></a>Vea también  
 [Instalar SQL Server 2014 desde el Asistente para instalación &#40;el programa de instalación&#41;](install-sql-server-from-the-installation-wizard-setup.md)   
 [Agregar características a una instancia de SQL Server 2014 &#40;el programa de instalación&#41;](add-features-to-an-instance-of-sql-server-setup.md)   
 [Anular una instalación de SQL Server 2014](repair-a-failed-sql-server-installation.md)  
  
  
