---
title: Interoperabilidad y coexistencia (Integration Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- interoperability and coexistence [Integration Services]
- Integration Services, interoperability and coexistence
ms.assetid: edfbcd56-012f-462e-a542-95491394fda9
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9f5b9bcd179e5485ad4959df02fd0b05b638998f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48200895"
---
# <a name="interoperability-and-coexistence-integration-services"></a>Interoperabilidad y coexistencia (Integration Services)
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services (SSIS) puede coexistir en paralelo con [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Integration Services y [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Integration Services.  
  
## <a name="features-and-differences"></a>Características y diferencias  
 En la tabla siguiente se enumeran algunas de las diferencias entre la versión actual y las versiones anteriores de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
|Característica|[!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]|[!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)]|[!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)]|  
|-------------|-------------------------------|---------------------------------|---------------------------------|  
|Entorno de desarrollo|[SQL Server 2014 Data Tools – Business Intelligence para Visual Studio 2012 CTP 2](http://www.microsoft.com/download/details.aspx?id=40736)<br /><br /> [SQL Server 2014 Data Tools - Business Intelligence para Visual Studio 2013](http://www.microsoft.com/download/details.aspx?id=42313)|[SQL Server Data Tools para Visual Studio 2010](http://msdn.microsoft.com/library/hh500335\(v=vs.103\).aspx)<br /><br /> [SQL Server Data Tools – Business Intelligence para Visual Studio 2012](http://www.microsoft.com/download/details.aspx?id=36843)|Business Intelligence Development Studio ([!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsOrcas](../../includes/vsorcas-md.md)])|  
|Entorno de administración|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]|[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]|  
|Tabla del sistema principal en msdb para almacenar paquetes|sysssispackages|sysssispackages|sysssispackages|  
|Utilidad de símbolo del sistema principal para los paquetes en ejecución|**dtexec** (dtexec.exe), versión 2014|**dtexec** (dtexec.exe), versión 2012|**dtexec** (dtexec.exe), versión 2008|  
|Carpeta raíz predeterminada del sistema de archivos|C:\Archivos de programa\Microsoft SQL Server\120\DTS|C:\Archivos de programa\Microsoft SQL Server\110\DTS|C:\Archivos de programa\Microsoft SQL Server\100\DTS|  
|Clave raíz predeterminada del Registro|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\SSIS|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\SSIS|HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\100\SSIS|  
  
## <a name="side-by-side-compatibility-issues"></a>Problemas de compatibilidad de simultaneidad  
 Cuando [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services está instalado en paralelo con [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Integration Services y [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Integration Services, se pueden realizar las siguientes tareas:  
  
-   **Diseñar paquetes en las herramientas de datos de SQL Server**. Utilice las siguientes herramientas para desarrollar y mantener paquetes basados en las versiones correspondientes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    -   Utilice la versión [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] de Business Intelligence Development Studio para desarrollar y mantener paquetes basados en [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)]  
  
    -   Use la [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] verzi [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para desarrollar y mantener paquetes basados en [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)].  
  
    -   Use la [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] verzi [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para desarrollar y mantener paquetes basados en [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)].  
  
-   **Cargar y ejecutar paquetes**. Puede cargar y ejecutar paquetes que se desarrollaron en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], en el [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] verzi [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Al agregar el paquete a un proyecto existente, el paquete se actualiza de forma permanente al formato que usa [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services. Al abrir el archivo del paquete en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], el paquete se actualiza temporalmente al formato que usa [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Integration Services. Si guarda este cambio en el paquete, se actualizará definitivamente. Una vez guardados en el formato que [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utiliza Integration Services, los paquetes ya no se pueden abrir en el correspondiente [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] versión de Business Intelligence Development Studio ni ejecutarse con la correspondiente [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Servicios de integración o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] herramientas de Integration Services.  
  
-   **Administrar paquetes en SQL Server Management Studio**. No se puede conectar a una instancia de la [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] versión de la [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] servicio desde el [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] versión de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. No se puede conectar a una instancia de la [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] versión de la [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] desde el [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] versión de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. Puede usar la versión de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para administrar paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] almacenados en una instancia de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Debe modificar el archivo de configuración del servicio para agregar la instancia de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a la lista de ubicaciones administradas por el servicio. Para obtener más información, vea [Configurar el servicio Integration Services &#40;servicio SSIS&#41;](../service/integration-services-service-ssis-service.md).  
  
-   **Almacenar paquetes en SQL Server**. Puede almacenar paquetes en las bases de datos siguientes.  
  
    |Formato del paquete|Base de datos|  
    |--------------------|--------------|  
    |[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Servicios de integración|base de datos msdb de una instancia de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]|  
    |[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] Servicios de integración|base de datos msdb de una instancia de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]|  
    |[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Servicios de integración|base de datos msdb de una instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]|  
  
     En una instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], puede importar paquetes desde una instancia de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o desde una instancia de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], pero no se puede exportar paquetes a una instancia de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o a una instancia de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].  
  
     En una instancia de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], no puede importar paquetes desde una instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ni exportar paquetes a dicha instancia.  
  
-   **Ejecutar paquetes**. Puede ejecutar [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] Integration Services y [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] paquetes de Integration Services mediante el uso de la [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] versión de la **dtexec** utilidad o de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente. Cada vez que un [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] herramienta Integration Services carga un paquete que se desarrolló en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], la herramienta convierte temporalmente, en la memoria, el paquete al paquete de formato que [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] usa. Si el [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] paquete presenta problemas que impiden una conversión correcta, el [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] herramienta Integration Services no puede ejecutar el paquete hasta que se resuelvan esos problemas. Para obtener más información, consulte [Upgrade Integration Services Packages](upgrade-integration-services-packages.md).  
  
  
