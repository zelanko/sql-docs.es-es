---
title: Requisitos previos del Asesor de actualización | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- installing Upgrade Advisor
- requirements [Upgrade Advisor]
- software [Upgrade Advisor]
- system requirements [Upgrade Advisor]
- Setup [Upgrade Advisor]
- SQL Server Upgrade Advisor, prerequisites
- prerequisites [Upgrade Advisor]
- Upgrade Advisor [SQL Server], prerequisites
ms.assetid: d21a39e5-5f81-4096-a7dd-f244e4779992
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 130059c64357d36ddf6c5eea7e27b15b0e42778c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48148515"
---
# <a name="upgrade-advisor-prerequisites"></a>Requisitos previos del Asesor de actualizaciones
  En este tema se describen los requisitos de software para el Asesor de actualizaciones.  
  
## <a name="prerequisites"></a>Requisitos previos  
 Los requisitos previos para instalar y ejecutar el Asesor de actualizaciones son los siguientes:  
  
-   [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] SP1, [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] a partir de SP2, Windows 7 o [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] R2.  
  
-   Windows Installer 4.5. Puede instalar Windows Installer desde la [sitio Web de Windows Installer](http://go.microsoft.com/fwlink/?LinkId=49112).  
  
-   [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], a partir de .NET Framework 4. El [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] está disponible en el [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CD del producto y desde el [sitio Web de descarga de SDK, los redistribuibles y service pack](http://go.microsoft.com/fwlink/?LinkId=48882).  
  
    -   Para instalar .NET Framework 4 desde el disco de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], busque la raíz de la unidad de disco. A continuación, haga doble clic en la carpeta \redist, haga doble clic en la carpeta DotNetFrameworks y ejecute dotNetFx40_Full_x86_x64.exe (para sistemas operativos de 32 bits y 64 bits).  
  
-   El [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] ScriptDom es un requisito previo para instalar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Asesor de actualizaciones y no se instala con la instalación de Upgrade Advisor. El programa de instalación requiere que descargue e instale el [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] ScriptDom desde el [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Feature Pack.  
  
## <a name="see-also"></a>Vea también  
 [Instalar el Asesor de actualizaciones](../../../2014/sql-server/install/how-to-install-upgrade-advisor.md)  
  
  
