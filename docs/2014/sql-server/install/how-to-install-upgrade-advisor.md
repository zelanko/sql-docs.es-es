---
title: 'Cómo: instalar el Asesor de actualizaciones | Documentos de Microsoft'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- installing Upgrade Advisor
- Setup [Upgrade Advisor]
- SQL Server Upgrade Advisor, installing
- Upgrade Advisor [SQL Server], installing
ms.assetid: 481b0704-ce79-4543-b141-67306128aa2b
caps.latest.revision: 24
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: b98a4b134025d22ad9d13ce9fa38a7e4f2605e0b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36202431"
---
# <a name="how-to-install-upgrade-advisor"></a>Instalar el Asesor de actualizaciones
  El Asesor de actualizaciones admite el análisis remoto de todos los componentes admitidos excepto [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Si no está analizando instancias de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], puede instalar el Asesor de actualizaciones en cualquier equipo que pueda conectarse a sus instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El equipo también debe cumplir los requisitos previos del Asesor de actualizaciones. Si está examinando instancias de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], debe instalar el Asesor de actualizaciones en el servidor de informes.  
  
 Para obtener más información, consulte [instalar el Asesor de actualizaciones](../../../2014/sql-server/install/installing-upgrade-advisor.md).  
  
### <a name="to-install-upgrade-advisor"></a>Para instalar el Asesor de actualizaciones  
  
1.  Inicie la instalación mediante uno de los siguientes métodos:  
  
    -   Si está instalando desde el [!INCLUDE[msCoName](../../includes/msconame-md.md)] sitio Web, haga clic en el **descargar** vincular y, a continuación, haga clic en el **ejecutar** botón para iniciar la instalación.  
  
    -   Si va a instalar desde el CD del producto, abra el **redist** carpeta, abra el **Asesor de actualizaciones** carpeta y, a continuación, haga doble clic en **SQLUA.msi**.  
  
    > [!NOTE]  
    >  El Asesor de actualizaciones necesita [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 4. Si no está instalado o si tiene una versión preliminar, aparecerá un mensaje de error. Desinstale cualquier versión anterior de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] y, a continuación, instale la versión más reciente de .NET Framework 4.  
    >   
    >  El [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] ScriptDom es un requisito previo para instalar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Asesor de actualizaciones y no se instala con la instalación del Asesor de actualizaciones. El programa de instalación requiere que descargue e instale el [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] ScriptDom desde el [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Feature Pack.  
  
2.  En el **Bienvenido a la [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] instalación del Asesor de actualizaciones** página, haga clic en **siguiente**.  
  
3.  En el **contrato de licencia** página, lea el contrato de licencia. Si los acepta, seleccione **acepto el contrato de licencia** y, a continuación, haga clic en **siguiente**.  
  
4.  En el **información de registro** página, escriba el nombre y la empresa.  
  
5.  En el **selección de características** página, revise la **ruta de acceso de instalación** valor. Si es necesario, utilice el **examinar** botón para cambiar la ubicación. Haga clic en **Siguiente**.  
  
6.  En el **preparado para instalar el programa** página, haga clic en **instalar** para instalar el Asesor de actualizaciones.  
  
7.  Haga clic en **Finalizar** para salir del asistente.  
  
## <a name="see-also"></a>Vea también  
 [Requisitos previos del Asesor de actualizaciones](../../../2014/sql-server/install/upgrade-advisor-prerequisites.md)  
  
  