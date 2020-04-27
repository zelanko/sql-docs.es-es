---
title: Instalar actualizaciones de servicio de SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 7d6c962b-c8d0-49f7-a2ac-00ad8dca930a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 07f438f86a22b866351a0b83ee7634338f3ad2cd
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62775348"
---
# <a name="install-sql-server-2014-servicing-updates"></a>Instalar actualizaciones de servicio de SQL Server 2014
  Este tema proporciona información acerca de cómo instalar actualizaciones para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Esta sección proporciona información acerca de lo siguiente:  
  
-   Instalar actualizaciones para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] durante una nueva instalación  
  
-   Instalar actualizaciones para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] una vez instalado.  
  
 Se recomienda que los clientes evalúen e instalen las últimas actualizaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puntualmente para asegurarse de que los sistemas están al día con las actualizaciones de seguridad más recientes.  
  
## <a name="installing-updates-for-sscurrent-during-a-new-installation"></a>Instalar actualizaciones para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] durante una nueva instalación  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] integra las últimas actualizaciones del producto con la instalación del producto principal, de modo que el producto principal y las actualizaciones aplicables se instalen al mismo tiempo. La actualización del producto puede buscar actualizaciones aplicables en:  
  
-   [!INCLUDE[msCoName](../../includes/msconame-md.md)] Update  
  
-   Windows Server Update Services (WSUS)  
  
-   Una carpeta local  
  
-   Un recurso compartido de red  
  
 Una vez que el programa de instalación encuentra las versiones más recientes de las actualizaciones aplicables, las descarga y las integra con el proceso de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] actual. La actualización del producto puede incluir una actualización acumulativa, un Service Pack o un Service Pack más la actualización acumulativa. La funcionalidad de Actualización de producto es una extensión de la [funcionalidad de instalación integrada](https://go.microsoft.com/fwlink/?LinkId=219945) que estaba disponible en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] PCU1.  
  
## <a name="installing-updates-for-sscurrent-after-it-has-already-been-installed"></a>Instalar actualizaciones para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] una vez instalado  
 En una instancia instalada de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], se recomienda aplicar todas las actualizaciones disponibles: las versiones de distribución general (GDR-seguridad/actualizaciones críticas), los Service Pack (SP), así como la última actualización acumulativa (Cu) disponible.  
  
 En función del tipo de servicio de mantenimiento, las actualizaciones de SQL Server están disponibles a través de Microsoft Update (MU), el centro de descarga de Microsoft o el servidor de revisiones de servicios de soporte al cliente. Las actualizaciones críticas y de seguridad de SQL Server se proporcionan automáticamente en Microsoft Update (para poder ver estas actualizaciones es necesario participar en MU a través de Windows Update en el panel de control). Los Service Pack están disponibles en MU como descargas opcionales/importantes, así como en el centro de descarga. Hay actualizaciones acumulativas disponibles en el servidor de descarga de revisiones de Microsoft que se proporciona en los artículos de Knowledge base de CU.  
  
## <a name="see-also"></a>Consulte también  
 [Instale SQL Server 2014 desde el Asistente para la instalación &#40;el programa de instalación&#41;](install-sql-server-from-the-installation-wizard-setup.md)   
 Al [instalar actualizaciones desde el símbolo del sistema](installing-updates-from-the-command-prompt.md) , se [agregan características a una instancia de SQL Server 2014 &#40;la instalación&#41;](add-features-to-an-instance-of-sql-server-setup.md)   
 [Anular una instalación de SQL Server 2014](repair-a-failed-sql-server-installation.md)  
  
  
