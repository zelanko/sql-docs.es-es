---
title: Actualizar las Herramientas de administración de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- management tools, upgrading
ms.assetid: 1dab50b9-d16c-49a1-9ecc-af72adb6c378
author: stevestein
ms.author: sstein
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: craigg
ms.openlocfilehash: b15e0448bb230ff209b17cbe5c0bc719686193f5
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2018
ms.locfileid: "51600725"
---
# <a name="upgrade-sql-server-management-tools"></a>Actualizar las herramientas de administración de SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] admite la actualización desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y versiones posteriores. En este artículo se documenta la compatibilidad y el comportamiento de la actualización de las Herramientas de administración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y los componentes de administración como el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Correo electrónico de base de datos, Planes de mantenimiento, XPStar y XPWeb.  
  
> [!IMPORTANT]  
>  En las instalaciones locales debe ejecutar el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como administrador. Si ejecuta el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde un recurso compartido remoto, debe utilizar una cuenta de dominio que tenga permisos de lectura y ejecución para el recurso compartido remoto.  
  
## <a name="known-upgrade-issues"></a>Problemas de actualización conocidos  
Considere los problemas siguientes antes de actualizar a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]:  
  
### <a name="for-all-upgrade-scenarios"></a>En todos los escenarios de actualización:  
  
- Todos los servidores TSX se deberían actualizar antes de actualizar el servidor MSX. Para obtener más información sobre MSX o TSX en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Administración automatizada en una empresa](../../ssms/agent/automated-administration-across-an-enterprise.md).  
  
-   Todos los componentes de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deben actualizarse al mismo tiempo. Los números de versión de [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]y [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] deben ser los mismos en una instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
-   Puede agregar componentes a una instalación existente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el momento en que actualiza a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para más información, vea [Upgrade SQL Server 2016 Using the Installation Wizard &#40;Setup&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md) (Actualización de SQL Server 2016 mediante el Asistente para instalación [programa de instalación]).  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , como [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], el Asistente para la optimización de [!INCLUDE[ssDE](../../includes/ssde-md.md)] , sqlcmd y osql no se actualizan a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. En su lugar, las herramientas de cliente se ejecutan en paralelo desde las versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] admite la configuración de importación desde las versiones anteriores de las herramientas de cliente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Durante la actualización, la autenticación del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se actualizará de la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a la de Windows. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se admite en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
-   Los datos de los trabajos y alertas se conservarán durante la actualización a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
-   Si se utiliza SQLMail en la instancia que se va a actualizar, se admitirán los XP asociados y se habilitarán después de la actualización. De lo contrario, se desactivarán.  
  
-   Correo electrónico de base de datos, que también se conoce como SQLiMail, se actualizará con el componente [!INCLUDE[ssDE](../../includes/ssde-md.md)] de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. De forma predeterminada, la aplicación Correo electrónico de base de datos se desactivará después de la actualización. Las actualizaciones del esquema deben reconciliarse con un script de actualización después de la actualización.  
  
## <a name="see-also"></a>Ver también  
 [Actualizaciones de ediciones y versiones admitidas](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)   
 [Compatibilidad con versiones anteriores](https://msdn.microsoft.com/library/15d9117e-e2fa-4985-99ea-66a117c1e9fd)   
 [Upgrade SQL Server Using the Installation Wizard &#40;Setup&#41;](../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md) (Actualización de SQL Server mediante el Asistente para instalación [programa de instalación])  
  
  
