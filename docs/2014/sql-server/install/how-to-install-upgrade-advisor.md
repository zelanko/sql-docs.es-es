---
title: Cómo instalar el asesor de actualizaciones | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- installing Upgrade Advisor
- Setup [Upgrade Advisor]
- SQL Server Upgrade Advisor, installing
- Upgrade Advisor [SQL Server], installing
ms.assetid: 481b0704-ce79-4543-b141-67306128aa2b
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0de86b9690f0647803938218ce566508662da20e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66094917"
---
# <a name="how-to-install-upgrade-advisor"></a>Procedimientos: Instalar el Asesor de actualizaciones
  El Asesor de actualizaciones admite el análisis remoto de todos los componentes admitidos excepto [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Si no está analizando instancias de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], puede instalar el Asesor de actualizaciones en cualquier equipo que pueda conectarse a sus instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El equipo también debe cumplir los requisitos previos del Asesor de actualizaciones. Si está examinando instancias de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], debe instalar el Asesor de actualizaciones en el servidor de informes.  
  
 Para obtener más información, vea [instalar el asesor de actualizaciones](../../../2014/sql-server/install/installing-upgrade-advisor.md).  
  
### <a name="to-install-upgrade-advisor"></a>Para instalar el Asesor de actualizaciones  
  
1.  Inicie la instalación mediante uno de los siguientes métodos:  
  
    -   Si va a instalar desde el [!INCLUDE[msCoName](../../includes/msconame-md.md)] sitio web de, haga clic en el vínculo **Descargar** y, a continuación, haga clic en el botón **Ejecutar** para iniciar la instalación.  
  
    -   Si va a instalar desde el medio del producto, abra la carpeta **Redist** , abra la carpeta **Asesor de actualizaciones** y, a continuación, haga doble clic en **SQLUA. msi**.  
  
    > [!NOTE]  
    >  El Asesor de actualizaciones necesita [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 4. Si no está instalado o si tiene una versión preliminar, aparecerá un mensaje de error. Desinstale cualquier versión anterior de [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] y, a continuación, instale la versión más reciente de .NET Framework 4.  
    >   
    >  ScriptDom [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] es un requisito previo para instalar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] el asesor de actualizaciones y el programa de instalación del Asesor de actualizaciones no lo instala. El programa de instalación requiere que descargue e instale [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[tsql](../../includes/tsql-md.md)] ScriptDom desde el [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Feature Pack.  
  
2.  En la página **Bienvenido a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] la instalación del Asesor de actualizaciones** , haga clic en **siguiente**.  
  
3.  En la página **contrato de licencia** , lea el contrato de licencia. Si está de acuerdo, seleccione Acepto **el contrato de licencia** y, a continuación, haga clic en **siguiente**.  
  
4.  En la página **información de registro** , escriba su nombre y su compañía.  
  
5.  En la página **selección de características** , revise el valor de la ruta de **instalación** . Si es necesario, use el botón **examinar** para cambiar la ubicación. Haga clic en **Siguiente**.  
  
6.  En la página **listo para instalar el programa** , haga clic en **instalar** para instalar el asesor de actualizaciones.  
  
7.  Haga clic en **Finalizar** para salir del asistente.  
  
## <a name="see-also"></a>Consulte también  
 [Requisitos previos del Asesor de actualizaciones](../../../2014/sql-server/install/upgrade-advisor-prerequisites.md)  
  
  
