---
title: Instalar actualizaciones de servicio de SQL Server | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 09/05/2017
ms.prod:
- sql-server-2016
- sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7d6c962b-c8d0-49f7-a2ac-00ad8dca930a
caps.latest.revision: 13
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 46b16dcf147dbd863eec0330e87511b4ced6c4ce
ms.openlocfilehash: 874dc2c5d78484b3aab341b8d515d4e652fe4c30
ms.contentlocale: es-es
ms.lasthandoff: 09/05/2017

---
# <a name="install-sql-server-servicing-updates"></a>Instalar actualizaciones de servicio de SQL Server
Este tema proporciona información acerca de cómo instalar actualizaciones para [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)]. Esta sección proporciona información acerca de lo siguiente:  
  
- Instalar actualizaciones para [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] durante una nueva instalación  
  
- Instalar actualizaciones para [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] una vez instalado.  
  
Instale las últimas actualizaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puntualmente para asegurarse de que los sistemas están al día con las actualizaciones de seguridad más recientes.  
  
## <a name="installing-updates-for-includenoversionincludesssnoversion-mdmd-during-a-new-installation"></a>Instalar actualizaciones para [!INCLUDE[noVersion](../../includes/ssNoVersion-md.md)] durante una nueva instalación  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] integra las últimas actualizaciones del producto con la instalación del producto principal, de modo que el producto principal y las actualizaciones aplicables se instalen al mismo tiempo. La actualización del producto puede buscar actualizaciones aplicables en:  
  
- [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update  
  
- Windows Server Update Services (WSUS)  
  
- Una carpeta local  
  
- Un recurso compartido de red  
  
Una vez que el programa de instalación encuentra las versiones más recientes de las actualizaciones aplicables, las descarga y las integra con el proceso de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] actual. La actualización del producto puede incluir una actualización acumulativa, un Service Pack o un Service Pack más la actualización acumulativa.  
  
## <a name="installing-updates-for-includessnoversionincludesssnoversion-mdmd-after-it-has-already-been-installed"></a>Instalar actualizaciones para [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)] una vez instalado  
En una instancia instalada de [!INCLUDE[ssNoVersion](../../includes/ssNoVersion-md.md)], se recomienda aplicar las actualizaciones de seguridad y actualizaciones críticas más recientes, incluidas las versiones de distribución general (GDR), Services Packs (SP) y actualizaciones acumulativas. Para más información, consulte el [anuncio sobre el modelo de servicios incrementales (ISM) de SQL Server de marzo de 2016](http://blogs.msdn.microsoft.com/sqlreleaseservices/announcing-updates-to-the-sql-server-incremental-servicing-model-ism/). 
  
Las actualizaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] están disponibles a través de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update (MU), Windows Server Update Services (WSUS) y del Centro de descarga de Microsoft. Las actualizaciones críticas y de seguridad para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] están disponibles a través de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update y para poder verlas necesita suscribirse a Microsoft Update a través del applet Windows Update del Panel de control.  
  
Cuando reciba una actualización a través de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update, se actualizan todas las características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a la versión más reciente en modo desatendido. Si necesita más flexibilidad o no tiene acceso a Internet o a WSUS, deberá obtener las actualizaciones en el Centro de descarga de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="see-also"></a>Vea también  
[Instalación de SQL Server desde el asistente para instalación](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md)   
[Agregar características a una instancia de SQL Server &#40;programa de instalación&#41;](../../database-engine/install-windows/add-features-to-an-instance-of-sql-server-2016-setup.md)   
[Reparar una instalación de SQL Server con errores](../../database-engine/install-windows/repair-a-failed-sql-server-installation.md)  


