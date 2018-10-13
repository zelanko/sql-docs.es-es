---
title: Actualizar Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Integration Services, upgrading
- SSIS, upgrading
- SQL Server Integration Services, upgrading
- upgrading Integration Services
ms.assetid: 04f9863c-ba0b-47c5-af91-f2d41b078a23
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: b6abc8e9e025bc24b4f456b58e0e9625e66b4b71
ms.sourcegitcommit: 5d6e1c827752c3aa2d02c4c7653aefb2736fffc3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/10/2018
ms.locfileid: "49072029"
---
# <a name="upgrade-integration-services"></a>Actualizar Integration Services
  Si [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] o [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] está instalado actualmente en el equipo, puede realizar la actualización a [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)].  
  
 Al actualizar a [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] en un equipo que tenga instalada una de estas versiones anteriores de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] se instala en paralelo con la versión anterior.  
  
 Con esta instalación en paralelo se instalan varias versiones de la utilidad dtexec. Para asegurarse de que ejecuta la versión correcta de la utilidad, escriba la ruta de acceso completa en el símbolo del sistema (\<unidad>:\Archivos de programa\Microsoft SQL Server\\<versión\>\DTS\Binn) para ejecutar la utilidad. Para obtener más información acerca de dtexec, vea [dtexec Utility](../packages/dtexec-utility.md).  
  
> [!NOTE]  
>  En versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], cuando se instalaba [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] todos los usuarios del grupo Usuarios tenía acceso al servicio de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] de forma predeterminada. Cuando instala [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], los usuarios no tienen acceso al servicio de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . El servicio es seguro de forma predeterminada. Después de instalar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , el administrador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe ejecutar la herramienta de configuración de DCOM (Dcomcnfg.exe) para conceder acceso al servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] a usuarios específicos. Para más información, consulte [Grant Permissions to Integration Services Service](../grant-permissions-to-integration-services-service.md).  
  
## <a name="before-upgrading-integration-services"></a>Antes de actualizar Integration Services  
 Recomendamos que ejecute el Asesor de actualizaciones antes de actualizar a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. El Asesor de actualizaciones notifica los problemas que podría encontrar si migra los paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] existentes al nuevo formato de paquete que [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utiliza. Para obtener más información, vea [Use Upgrade Advisor to Prepare for Upgrades](../../sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md).  
  
> [!NOTE]  
>  Compatibilidad para migrar o ejecutar paquetes de servicios de transformación de datos (DTS) no se incluye en la versión actual de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. La funcionalidad de DTS siguiente ya no se incluye.  
>   
>  -   Tiempo de ejecución DTS  
> -   DTS API  
> -   El Asistente para migrar paquetes, que permite migrar paquetes DTS a la versión siguiente de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
> -   Compatibilidad con el mantenimiento de paquetes DTS en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
> -   Tarea Ejecutar paquete DTS 2000  
> -   Examen del Asesor de actualizaciones de paquetes DTS.  
>   
>  Para obtener información sobre otras características, vea [no incluye funcionalidad de Integration Services en SQL Server 2014](../discontinued-integration-services-functionality-in-sql-server-2014.md).  
  
## <a name="upgrading-integration-services"></a>actualizar Integration Services  
 Puede actualizar con uno de los métodos siguientes:  
  
-   Ejecute [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] el programa de instalación y seleccione la opción de **actualizar desde SQL Server 2005, SQL Server 2008 o SQL Server 2008 R2**, o **[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]**.  
  
-   Ejecute **setup.exe** en el símbolo del sistema y especifique el `/ACTION=upgrade` opción. Para obtener más información, vea la sección "Scripts de instalación de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]," en [instalar SQL Server 2014 desde el símbolo del sistema](../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md).  
  
 No puede utilizar la actualización para realizar las acciones siguientes:  
  
-   Reconfigurar una instalación existente de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
-   Pasar de una versión de 32 bits a una versión de 64 bits de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o de una versión de 64 bits a una versión de 32 bits.  
  
-   Pasar de una versión traducida de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a otra.  
  
 Al actualizar, puede actualizar tanto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] como el [!INCLUDE[ssDE](../../includes/ssde-md.md)], actualizar solo el [!INCLUDE[ssDE](../../includes/ssde-md.md)]o simplemente actualizar [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Si solo actualiza [!INCLUDE[ssDE](../../includes/ssde-md.md)], [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] o [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] siguen siendo funcionales, pero no dispone de la funcionalidad de [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)]. Si solo actualiza [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] es totalmente funcional, pero solo puede almacenar paquetes en el sistema de archivos, a menos que se disponga de una instancia de [!INCLUDE[ssDECurrent](../../includes/ssdecurrent-md.md)] en otro equipo.  
  
## <a name="upgrading-both-integration-services-and-the-database-engine-to-includesscurrentincludessscurrent-mdmd"></a>Actualizar tanto Integration Services como el Motor de base de datos a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 En esta sección se describen los efectos de realizar una actualización que tenga los criterios siguientes:  
  
-   Actualiza [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
-   Tanto [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] como la instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] están en el mismo equipo.  
  
### <a name="what-the-upgrade-process-does"></a>Qué hace el proceso de actualización  
 El proceso de actualización lleva a cabo las tareas siguientes:  
  
-   Instala los archivos, el servicio y las herramientas de [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] ([!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] y [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]). Cuando hay varias instancias de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] en el mismo equipo, la primera vez que actualice alguna de las instancias a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] se instalarán los archivos, el servicio y las herramientas de [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)].  
  
-   Actualiza la instancia de la [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] a la [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] versión.  
  
-   Mueve los datos de la [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] o [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] tablas del sistema para el [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] tablas del sistema, como se indica a continuación:  
  
    -   Mueve los paquetes sin cambiar la tabla del sistema msdb.dbo.sysdtspackages90 a msdb.dbo.sysssispackages.  
  
        > [!NOTE]  
        >  Aunque los datos se muevan a una tabla del sistema diferente, el proceso de actualización no migra los paquetes al nuevo formato.  
  
    -   Mueve los metadatos de la carpeta de la tabla del sistema msdb.sysdtsfolders90 a la tabla del sistema msdb.sysssisfolders.  
  
    -   Mueve los datos del registro de la tabla del sistema msdb.sysdtslog90 a la tabla del sistema msdb.sysssislog.  
  
-   Quita las tablas del sistema msdb.sysdts*90 y los procedimientos almacenados que se usan para tener acceso a ellas después de mover los datos a las nuevas tablas msdb.sysssis\* . Sin embargo, la actualización reemplaza la tabla sysdtslog90 por una vista que también se denomina sysdtslog90. Esta nueva vista sysdtslog90 expone la nueva tabla del sistema msdb.sysssislog. De esta forma, se asegura de que los informes basados en la tabla de registro continúan ejecutándose sin interrupción.  
  
-   Para controlar el acceso a los paquetes, crea tres nuevos roles fijos de nivel de base de datos: db_ssisadmin, db_ssisltduser y db_ssisoperator. Los roles de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] de db_dtsadmin, db_dtsltduser y db_dtsoperator no se quitan, sino que se convierten en miembros de los roles nuevos correspondientes.  
  
-   Si el [!INCLUDE[ssIS](../../includes/ssis-md.md)] almacén de paquetes (es decir, la ubicación de sistema de archivos administrada por el [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] service) es la ubicación predeterminada bajo **\SQL Server\90**, **\SQL Server\100**, o **\SQL Server\110** mueve esos paquetes a la nueva ubicación predeterminada bajo **\SQL Server\120**.  
  
-   Actualiza el archivo de configuración del servicio [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para señalar a la instancia actualizada del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
### <a name="what-the-upgrade-process-does-not-do"></a>Qué no hace el proceso de actualización  
 El proceso de actualización no lleva a cabo las tareas siguientes:  
  
-   **No** quitar el [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] o [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] service.  
  
-   No migra los paquetes existentes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] al nuevo formato de paquete que [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usa. Para obtener información sobre cómo migrar paquetes, vea [Actualizar paquetes de Integration Services](upgrade-integration-services-packages.md).  
  
-   No mueve los paquetes desde las ubicaciones del sistema de archivos, excepto la ubicación predeterminada, que se han agregado al archivo de configuración del servicio. Si ha modificado previamente el archivo de configuración del servicio para agregar más carpetas del sistema de archivos, los paquetes que se almacenan en esas carpetas no se moverán a otra ubicación.  
  
-   En los pasos de trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que llaman directamente a la utilidad **dtexec** (dtexec.exe), no actualiza la ruta de acceso al sistema de archivos para la utilidad **dtexec** . Tiene que editar manualmente estos pasos de trabajo para actualizar la ruta de acceso al sistema de archivos con el fin de especificar la ubicación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] correspondiente a la utilidad **dtexec** .  
  
### <a name="what-you-can-do-after-upgrading"></a>Lo que puede hacer después de actualizar  
 Después de que el proceso de actualización finalice, puede hacer las tareas siguientes:  
  
-   Ejecutar trabajos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que ejecuten paquetes.  
  
-   Use [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para administrar [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] paquetes que están almacenados en una instancia de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Debe modificar el archivo de configuración del servicio para agregar la instancia de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a la lista de ubicaciones administradas por el servicio.  
  
    > [!NOTE]  
    >  Las versiones anteriores de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] no se pueden conectar al servicio de [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)].  
  
-   Identificar la versión de los paquetes en la tabla del sistema msdb.dbo.sysssispackages comprobando el valor en la columna packageformat. La tabla tiene una columna packageformat que identifica la versión de cada paquete. Un valor de 2 en la columna packageformat indica un paquete de [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)]; un valor de 3, un paquete de [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)]. Hasta que migre los paquetes al nuevo formato de paquete, el valor de la columna packageformat no cambia.  
  
-   No puede usar el [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] herramientas para diseñar, ejecutar ni administrar [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] paquetes. Las herramientas de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] incluyen las versiones respectivas de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y la Utilidad de ejecución de paquetes (dtexecui.exe). El proceso de actualización no quita el [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]herramientas. No obstante, no podrá usar estas herramientas para continuar trabajando con paquetes de [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] o [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] en un servidor que se haya actualizado.  
  
-   De forma predeterminada, en una instalación de actualización, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] se configura para registrar en el registro de eventos de aplicación los eventos relacionados con la ejecución de paquetes. Esta configuración podría generar demasiadas entradas en el registro de eventos al utilizar la característica de recopilador de datos de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Los eventos que se registran incluyen EventID 12288, "Se ha iniciado el paquete" y EventID 12289, "El paquete finalizó correctamente". Para detener el registro de estos dos eventos en el registro de eventos de aplicación, abra el Registro para editarlo. A continuación, en el Registro, busque el nodo HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\120\SSIS y cambie el valor DWORD de la configuración LogPackageExecutionToEventLog de 1 a 0.  
  
## <a name="upgrading-only-the-database-engine-to-includesscurrentincludessscurrent-mdmd"></a>Actualizar solo el Motor de base de datos a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 En esta sección se describen los efectos de realizar una actualización que tenga los criterios siguientes:  
  
-   Actualiza únicamente una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Es decir, la instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] ahora es una instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], pero la instancia de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y las herramientas cliente son de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
-   La instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] está en un equipo mientras que [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] y las herramientas cliente están en otro.  
  
### <a name="what-you-can-do-after-upgrading"></a>Lo que puede hacer después de actualizar  
 Las tablas del sistema que almacenan los paquetes en la instancia actualizada de [!INCLUDE[ssDE](../../includes/ssde-md.md)] no son iguales que las que se usan en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]. Por lo tanto, el [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] versiones de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] y [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] no se puede detectar los paquetes en las tablas del sistema en la instancia actualizada de la [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Dado que estos paquetes no se pueden detectar, existen limitaciones en lo que se puede hacer con ellos:  
  
-   No puede usar las herramientas de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] ni de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] ni de [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], en otros equipos para cargar o administrar los paquetes de la instancia actualizada de [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
    > [!NOTE]  
    >  Aunque los paquetes de la instancia actualizada de [!INCLUDE[ssDE](../../includes/ssde-md.md)] no se hayan migrado aún al nuevo formato de paquete, las herramientas de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] no pueden detectarlos. Por lo tanto, las herramientas de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] no pueden usar los paquetes.  
  
-   No puede usar [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] o [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] en otros equipos para ejecutar los paquetes almacenados en msdb en la instancia actualizada de la [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
-   No puede usar los trabajos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en equipos con [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] para ejecutar los paquetes de [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] o [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] que estén almacenados en la instancia actualizada de [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
## <a name="external-resources"></a>Recursos externos  
 Entrada de blog [Hacer que las extensiones y aplicaciones personalizadas existentes de SSIS funcionen en Denali](http://go.microsoft.com/fwlink/?LinkId=238157), en blogs.msdn.com.  
  
  
