---
title: Instalar actualizaciones de servicio de SQL Server 2014 | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7d6c962b-c8d0-49f7-a2ac-00ad8dca930a
caps.latest.revision: 13
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: c7601914ed32def54b153282a90b51629b1380b6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36202554"
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
 En una instancia instalada de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], le recomendamos que aplique todas las actualizaciones disponibles: las versiones de distribución General (GDR - las actualizaciones de seguridad y crítico), Service Pack (SP), así como la CU más reciente disponible acumulativa Update ().  
  
 Según el tipo de versión de mantenimiento, actualizaciones de SQL Server están disponibles a través de Microsoft Update (MU), Microsoft Download Center o el servidor de revisión de los servicios de soporte técnico al cliente. Microsoft Update (para poder ver estas actualizaciones que necesita para participar en Microsoft Update a través de Windows Update en el panel de Control) proporciona automáticamente actualizaciones críticas y de seguridad para SQL Server. Service Packs están disponibles en Microsoft Update como descarga opcional/importante, así como el centro de descarga. Las actualizaciones acumulativas están disponibles en el servidor de descarga de revisión de Microsoft proporcionado en los artículos de la Base de conocimiento de CU.  
  
## <a name="see-also"></a>Vea también  
 [Instalar SQL Server 2014 desde el Asistente para la instalación &#40;el programa de instalación&#41;](install-sql-server-from-the-installation-wizard-setup.md)   
 [Agregar características a una instancia de SQL Server 2014 &#40;el programa de instalación&#41;](add-features-to-an-instance-of-sql-server-setup.md)   
 [Quitar una instalación de SQL Server 2014](repair-a-failed-sql-server-installation.md)  
  
  