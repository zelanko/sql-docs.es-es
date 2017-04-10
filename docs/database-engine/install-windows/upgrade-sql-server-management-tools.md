---
title: "Actualizar las herramientas de administraci&#243;n de SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "herramientas de administración, actualizar"
ms.assetid: 1dab50b9-d16c-49a1-9ecc-af72adb6c378
caps.latest.revision: 19
author: "stevestein"
ms.author: "sstein"
manager: "jhubbard"
caps.handback.revision: 19
---
# Actualizar las herramientas de administraci&#243;n de SQL Server
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] admite la actualización desde [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y versiones posteriores. En este tema se documenta la compatibilidad y el comportamiento de la actualización de las Herramientas de administración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y los componentes de administración como el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , Correo electrónico de base de datos, Planes de mantenimiento, XPStar y XPWeb.  
  
> [!IMPORTANT]  
>  En las instalaciones locales debe ejecutar el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como administrador. Si ejecuta el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde un recurso compartido remoto, debe utilizar una cuenta de dominio que tenga permisos de lectura y ejecución para el recurso compartido remoto.  
  
## Problemas de actualización conocidos  
 Considere los problemas siguientes antes de actualizar a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]:  
  
### En todos los escenarios de actualización:  
  
-   Todos los servidores TSX se deberían actualizar antes de actualizar el servidor MSX. Para obtener más información sobre MSX o TSX en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Administración automatizada en una empresa](../../ssms/agent/automated-administration-across-an-enterprise.md).  
  
-   Todos los componentes de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deben actualizarse al mismo tiempo. Los números de versión de [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]y [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] deben ser los mismos en una instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
-   Puede agregar componentes a una instalación existente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el momento en que actualiza a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obtener más información, vea [Actualización a SQL Server 2016 mediante el Asistente para instalación &#40;programa de instalación&#41;](../../database-engine/install-windows/upgrade-to-sql-server-2016-using-the-installation-wizard-setup.md).  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , como [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], el Asistente para la optimización de [!INCLUDE[ssDE](../../includes/ssde-md.md)] , sqlcmd y osql no se actualizan a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. En su lugar, las herramientas de cliente se ejecutan en paralelo desde las versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] admite la configuración de importación desde las versiones anteriores de las herramientas de cliente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Durante la actualización, la autenticación del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se actualizará de la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a la de Windows. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no se admite en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
-   Los datos de los trabajos y alertas se conservarán durante la actualización a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
-   Si se utiliza SQLMail en la instancia que se va a actualizar, se admitirán los XP asociados y se habilitarán después de la actualización. De lo contrario, se desactivarán.  
  
-   Correo electrónico de base de datos, que también se conoce como SQLiMail, se actualizará con el componente [!INCLUDE[ssDE](../../includes/ssde-md.md)] de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. De forma predeterminada, la aplicación Correo electrónico de base de datos se desactivará después de la actualización. Las actualizaciones del esquema deben reconciliarse con un script de actualización después de la actualización.  
  
## Vea también  
 [Actualizaciones de ediciones y versiones admitidas](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)   
 [Compatibilidad con versiones anteriores](../Topic/Backward%20Compatibility_deleted.md)   
 [Actualización a SQL Server 2016 mediante el Asistente para instalación &#40;programa de instalación&#41;](../../database-engine/install-windows/upgrade-to-sql-server-2016-using-the-installation-wizard-setup.md)  
  
  