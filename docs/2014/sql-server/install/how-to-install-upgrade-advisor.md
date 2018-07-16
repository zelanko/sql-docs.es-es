---
title: 'Cómo: instalar Upgrade Advisor | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- installing Upgrade Advisor
- Setup [Upgrade Advisor]
- SQL Server Upgrade Advisor, installing
- Upgrade Advisor [SQL Server], installing
ms.assetid: 481b0704-ce79-4543-b141-67306128aa2b
caps.latest.revision: 24
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 241bae15e3d4edf548e12cfcb06ca09cab8c8a89
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37216445"
---
# <a name="how-to-install-upgrade-advisor"></a>Instalar el Asesor de actualizaciones
  El Asesor de actualizaciones admite el análisis remoto de todos los componentes admitidos excepto [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Si no está analizando instancias de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], puede instalar el Asesor de actualizaciones en cualquier equipo que pueda conectarse a sus instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El equipo también debe cumplir los requisitos previos del Asesor de actualizaciones. Si está examinando instancias de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], debe instalar el Asesor de actualizaciones en el servidor de informes.  
  
 Para obtener más información, consulte [Installing Upgrade Advisor](../../../2014/sql-server/install/installing-upgrade-advisor.md).  
  
### <a name="to-install-upgrade-advisor"></a>Para instalar el Asesor de actualizaciones  
  
1.  Inicie la instalación mediante uno de los siguientes métodos:  
  
    -   Si está instalando desde el [!INCLUDE[msCoName](../../includes/msconame-md.md)] sitio Web, haga clic en el **descargar** vincular y, a continuación, haga clic en el **ejecutar** botón para iniciar la instalación.  
  
    -   Si está instalando desde el CD del producto, abra el **redist** carpeta, abra el **Upgrade Advisor** carpeta y, a continuación, haga doble clic en **SQLUA.msi**.  
  
    > [!NOTE]  
    >  El Asesor de actualizaciones necesita [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 4. Si no está instalado o si tiene una versión preliminar, aparecerá un mensaje de error. Desinstale cualquier versión anterior de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] y, a continuación, instale la versión más reciente de .NET Framework 4.  
    >   
    >  El [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] ScriptDom es un requisito previo para instalar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Asesor de actualizaciones y no se instala con la instalación de Upgrade Advisor. El programa de instalación requiere que descargue e instale el [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] ScriptDom desde el [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Feature Pack.  
  
2.  En el **Bienvenido a la [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] instalación de Upgrade Advisor** página, haga clic en **siguiente**.  
  
3.  En el **contrato de licencia** página, lea el contrato de licencia. Si está de acuerdo, seleccione **acepto el contrato de licencia** y, a continuación, haga clic en **siguiente**.  
  
4.  En el **información de registro** , escriba su nombre y la empresa.  
  
5.  En el **selección de características** , revise el **ruta de instalación** valor. Si es necesario, utilice el **examinar** botón para cambiar la ubicación. Haga clic en **Siguiente**.  
  
6.  En el **preparado para instalar el programa** página, haga clic en **instalar** para instalar el Asesor de actualizaciones.  
  
7.  Haga clic en **Finalizar** para salir del asistente.  
  
## <a name="see-also"></a>Vea también  
 [Requisitos previos del Asesor de actualizaciones](../../../2014/sql-server/install/upgrade-advisor-prerequisites.md)  
  
  
