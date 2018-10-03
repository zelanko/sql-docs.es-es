---
title: Utilice el Asesor de actualizaciones para preparar las actualizaciones | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Upgrade Advisor [SQL Server]
- upgrading SQL Server, Upgrade Advisor
- upgrading SQL Server, preparing to upgrade
- SQL Server Upgrade Advisor
- analyzing installations for upgrading [SQL Server]
ms.assetid: d85b0833-ddeb-42e3-9397-97ea60d521b7
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c8ade9c0d0d877ca1c12c1361e0e0ba45c2e7ecb
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48209295"
---
# <a name="use-upgrade-advisor-to-prepare-for-upgrades"></a>Usar el Asesor de actualizaciones para preparar las actualizaciones
  El Asesor de actualizaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ayuda a preparar las actualizaciones de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Esta herramienta analiza los componentes instalados de las versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y genera un informe que identifica los problemas que han de solucionarse antes o después de la actualización.  
  
## <a name="how-upgrade-advisor-works"></a>Cómo funciona el Asesor de actualizaciones  
 Al ejecutar el Asesor de actualizaciones, se mostrará la página de inicio del Asesor de actualizaciones. Desde la página Inicio, podrá ejecutar las siguientes herramientas:  
  
-   Asistente para análisis del Asesor de actualizaciones  
  
-   Visor de informes del Asesor de actualizaciones  
  
-   Ayuda del Asesor de actualizaciones  
  
 La primera vez que utilice el Asesor de actualizaciones, ejecute el Asistente para análisis del Asesor de actualizaciones para analizar los componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Una vez que el asistente haya finalizado el análisis, podrá ver los informes resultantes en el Visor de informes del Asesor de actualizaciones. Los informes incluyen vínculos a información de la Ayuda del Asesor de actualizaciones que le ayudará a solucionar los problemas conocidos o a paliar su efecto.  
  
## <a name="upgrade-advisor-analysis"></a>Análisis del Asesor de actualizaciones  
 El Asesor de actualizaciones analiza los siguientes componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
 El análisis examina los objetos accesibles, como scripts, procedimientos almacenados, desencadenadores y archivos de seguimiento. El Asesor de actualizaciones no puede analizar aplicaciones de escritorio ni procedimientos almacenados cifrados.  
  
 El resultado se presenta como un informe XML. Podrá ver el informe XML mediante el Visor de informes del Asesor de actualizaciones.  
  
> [!NOTE]  
>  Los informes pueden contener un elemento "otros problemas de actualización". Este elemento vincula a una lista de problemas que no detecta el Asesor de actualizaciones, pero que pueden existir en el servidor o en las aplicaciones. Debe leer la lista de problemas no detectables y determinar si debe realizar cambios en el servidor o en las aplicaciones para solventarlos.  
  
## <a name="how-to-install-and-run-upgrade-advisor"></a>Cómo instalar y ejecutar el Asesor de actualizaciones  
 La ubicación en la que se instala el Asesor de actualizaciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] depende de lo que se vaya a analizar. El Asesor de actualizaciones admite el análisis remoto de todos los componentes admitidos excepto [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Si no está analizando instancias de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], puede instalar el Asesor de actualizaciones en cualquier equipo que pueda conectarse a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y que cumpla los requisitos previos del Asesor de actualizaciones. Para obtener información detallada, vea [Actualizaciones de ediciones y versiones admitidas](../../database-engine/install-windows/supported-version-and-edition-upgrades.md). Si está examinando instancias de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], debe instalar el Asesor de actualizaciones en el servidor de informes.  
  
 El Asesor de actualizaciones está disponible en un Feature Pack.  
  
 Requisitos previos para instalar y ejecutar el Asesor de actualizaciones son las siguientes:  
  
-   [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)] SP2, Windows 7 SP1 y [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)] SP1.  
  
-   Windows Installer a partir de la versión 4.5. Puede instalar Windows Installer desde la [sitio Web de Windows Installer](http://go.microsoft.com/fwlink/?LinkId=49112).  
  
-   Microsoft .NET Framework 4. .NET framework 4 está disponible en el [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CD del producto y desde el [página de descarga de .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=209895).  
  
    -   Para instalar .NET Framework 4 desde el disco de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], busque la raíz de la unidad de disco. A continuación, haga doble clic en la carpeta \redist, haga doble clic en la carpeta DotNetFrameworks y ejecute dotNetFx40_Full_x86_x64.exe (para sistemas operativos de 32 bits o para sistemas operativos de 64 bits).  
  
 Para instalar el Asesor de actualizaciones desde Internet, haga clic en el botón de descarga de la página de descarga. Puede ejecutar la instalación inmediatamente o guardar el archivo SQLUA.msi para ejecutarlo más tarde. Si va a realizar la instalación desde el disco del producto, ejecute el archivo SQLUA.msi directamente desde dicho disco.  
  
 Después de instalar el Asesor de actualizaciones, puede abrirlo desde el **iniciar** menú:  
  
-   Haga clic en **iniciar**, apunte a **todos los programas**, apunte a [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)]y, a continuación, haga clic en  **[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Upgrade Advisor**.  
  
 Para obtener más información, vea la documentación del Asesor de actualizaciones incluida en la descarga del Asesor de actualizaciones y las notas de la versión de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Trabajar con varias versiones e instancias de SQL Server](../../../2014/sql-server/install/work-with-multiple-versions-and-instances-of-sql-server.md)   
 [Actualizaciones de ediciones y versiones admitidas](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)   
 [Compatibilidad con versiones anteriores](../../../2014/getting-started/backward-compatibility.md)  
  
  
