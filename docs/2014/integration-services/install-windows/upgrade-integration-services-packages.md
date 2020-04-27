---
title: Actualizar paquetes de Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services, migrating
- migrating packages [Integration Services]
ms.assetid: 68dbdf81-032c-4a73-99f6-41420e053980
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: a1ff35cfc7d5e8611c06981b2e3a9fe9dd6e82fd
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62769001"
---
# <a name="upgrade-integration-services-packages"></a>Actualizar paquetes de Integration Services
  Cuando se actualiza una instancia de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a la versión actual de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], los paquetes [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] existentes no se actualizan automáticamente al formato de paquete que usa la versión [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] actual. Tendrá que seleccionar un método de actualización y actualizar manualmente los paquetes.  
  
 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] Al actualizar un paquete [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , migra los scripts de las tareas script y componentes script a [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA). En [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], los scripts de tareas script o componentes de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] script usados para aplicaciones (VSA). Para más información sobre los cambios que es posible que haya que realizar en los scripts antes de la migración y sobre los errores de conversión de scripts, vea [Migrar scripts a VSTA](../../sql-server/install/migrate-scripts-to-vsta.md).  
  
 Para obtener información sobre la actualización de paquetes cuando se convierte un proyecto al modelo de implementación de proyecto, vea [Deploy Projects to Integration Services Server](../deploy-projects-to-integration-services-server.md).  
  
## <a name="sql-server-2000-data-transformation-services-packages"></a>Los paquetes de Servicios de transformación de datos de SQL Server 2000  
 La compatibilidad con la migración o ejecución de paquetes de servicios de transformación de datos (DTS) ya no se incluye en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]la versión actual de. La funcionalidad de DTS siguiente ya no se incluye.  
  
-   Tiempo de ejecución DTS  
  
-   DTS API  
  
-   El Asistente para migrar paquetes, que permite migrar paquetes DTS a la versión siguiente de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   Compatibilidad con el mantenimiento de paquetes DTS en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
-   Tarea Ejecutar paquete DTS 2000  
  
-   Examen del Asesor de actualizaciones de paquetes DTS.  
  
 Las siguientes opciones están disponibles para mirar paquetes de DTS.  
  
-   Migre los paquetes a [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] o a [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)]y después actualice los paquetes a [!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)].  
  
     Para obtener información sobre cómo migrar paquetes DTS a [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] y a [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)], vea [Paquetes de Servicios de transformación de datos (DTS](https://go.microsoft.com/fwlink/?LinkId=251870) (2005) y [Paquetes de Servicios de transformación de datos (DTS](https://go.microsoft.com/fwlink/?LinkId=251871) (2008).  
  
-   Vuelva a crear los paquetes DTS mediante [!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)].  
  
     Para más información sobre las nuevas características de [!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)], vea [Novedades &#40;Integration Services&#41;](../what-s-new-in-integration-services-in-sql-server-2016.md). Para obtener información general de la estructura de paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], vea [paquetes de Integration Services &#40;SSIS&#41;](../integration-services-ssis-packages.md).  
  
## <a name="selecting-an-upgrade-method"></a>Seleccionar un método de actualización  
 Puede utilizar distintos métodos para actualizar los paquetes de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] . En algunos de estos métodos, la actualización solo es temporal. En otros, es definitiva. La tabla siguiente describe cada uno de estos métodos y si la actualización es temporal o definitiva.  
  
> [!NOTE]  
>  Cuando se ejecuta un paquete de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] mediante la utilidad **dtexec** que se instala con la versión actual de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], the tempoary package upgrade increases the execution time. La proporción de incremento de tiempo de ejecución del paquete depende del tamaño del mismo. Para evitar un incremento del tiempo de ejecución, se recomienda actualizar el paquete antes de ejecutarlo.  
  
|Método de actualización|Tipo de actualización|  
|--------------------|---------------------|  
|Use la utilidad **dtexec** que se instala con la versión actual de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para ejecutar un paquete de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] .<br /><br /> Para obtener más información, consulte [utilidad dtexec](../packages/dtexec-utility.md).|La actualización del paquete es temporal. En el caso de un paquete de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] , la migración de scripts es temporal.<br /><br /> No se pueden guardar los cambios.|  
|Abra un archivo de paquete de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].|La actualización del paquete es definitiva si guarda el paquete; de lo contrario, es temporal.<br /><br /> En el caso de un paquete [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] , la migración del script es definitiva si guarda el paquete; de lo contrario, es temporal.|  
|Agregar un paquete de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a un proyecto existente en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].|La actualización del paquete es definitiva. En el caso de un paquete de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] , la migración de scripts es definitiva.|  
|Abra un archivo de proyecto [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] o [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] en [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)]y luego use el Asistente para actualizar paquetes de [!INCLUDE[ssIS](../../includes/ssis-md.md)] para actualizar varios paquetes en el proyecto.<br /><br /> Para obtener más información, vea [Actualizar paquetes de Integration Services mediante el Asistente para actualizar paquetes SSIS](upgrade-integration-services-packages-using-the-ssis-package-upgrade-wizard.md) y [Ayuda F1 del Asistente para actualización del paquete SSIS](../ssis-package-upgrade-wizard-f1-help.md).|La actualización del paquete es definitiva. En el caso de un paquete de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] , la migración de scripts es definitiva.|  
|Use la utilidad <xref:Microsoft.SqlServer.Dts.Runtime.Application.Upgrade%2A> para actualizar uno o más paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|La actualización del paquete es definitiva. En el caso de un paquete de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] , la migración de scripts es definitiva.|  
  
## <a name="custom-applications-and-custom-components"></a>Aplicaciones y componentes personalizados  
 [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] no funcionarán con la versión actual de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 Puede usar la versión actual de las herramientas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para ejecutar y administrar paquetes que incluyen componentes personalizados de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)][!INCLUDE[ssIS](../../includes/ssis-md.md)]. Hemos agregado cuatro reglas de redirección de enlace a los archivos siguientes para redirigir los ensamblados en tiempo de ejecución de la versión 10.0.0.0 ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]) a la versión 11.0.0.0 ([!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]).  
  
-   DTExec.exe.config  
  
-   dtshost.exe.config  
  
-   DTSWizard.exe.config  
  
-   DTUtil.exe.config  
  
-   DTExecUI.exe.config  
  
 Para usar [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] para diseñar paquetes que incluyen [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] componentes [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] personalizados de y, debe modificar el archivo devenv. exe. config que se encuentra en * \<la unidad>*: \Archivos de programa\Microsoft Visual Studio 10.0 \ Common7\IDE.  
  
 Para usar estos paquetes con aplicaciones cliente compiladas con el motor de ejecución para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], incluya reglas de redirección en la sección de configuración del archivo *.exe.config para el ejecutable. Las reglas redirigirán los ensamblados en tiempo de ejecución a la versión 11.0.0.0 ([!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]). Para obtener más información sobre el redireccionamiento de versiones de ensamblado, vea [ \<elemento> de assemblyBinding para>en tiempo de \<ejecución ](https://msdn.microsoft.com/library/twy1dw1e.aspx).  
  
### <a name="locating-the-assemblies"></a>Buscar los ensamblados  
 En [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], los ensamblados de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] se actualizaron a .NET 4.0. Hay una memoria caché global de ensamblados independiente para .net 4, que se encuentra en * \<la unidad>*: \Windows\Microsoft.NET\assembly. Puede buscar todos los ensamblados de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] bajo esta ruta de acceso, normalmente en la carpeta GAC_MSIL.  
  
 Como en versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], los archivos [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . dll de extensibilidad principales también se encuentran en * \<la unidad>*: \Archivos de programa\Microsoft SQL Server\100\SDK\Assemblies.  
  
## <a name="understanding-sql-server-package-upgrade-results"></a>Descripción de los resultados de la actualización del paquete SQL Server  
 Durante el proceso de actualización del paquete, la mayoría de los componentes y características de los paquetes de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] se convierten sin problema en sus homólogos de la versión actual de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Sin embargo, hay varios componentes y características que no se actualizarán u obtendrán resultados en la actualización que habría que tener en cuenta. La tabla siguiente identifica estos componentes y características.  
  
> [!NOTE]  
>  Para identificar qué paquetes experimentan los problemas enumerados en esta tabla, ejecute el Asesor de actualizaciones. Para obtener más información, vea [Use Upgrade Advisor to Prepare for Upgrades](../../sql-server/install/use-upgrade-advisor-to-prepare-for-upgrades.md).  
  
|Componente o característica|Resultados de la actualización|  
|--------------------------|---------------------|  
|Cadenas de conexión|En el caso de paquetes de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] , los nombres de ciertos proveedores han cambiado y requieren valores diferentes en las cadenas de conexión. Para actualizar las cadenas de conexión, utilice uno de los procedimientos siguientes:<br /><br /> -Use el [!INCLUDE[ssIS](../../includes/ssis-md.md)] Asistente para actualizar paquetes para actualizar el paquete y seleccione la opción **actualizar las cadenas de conexión para utilizar los nuevos nombres de proveedor** .<br /><br /> En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]la página general del cuadro de diálogo Opciones, seleccione la opción actualizar las **cadenas de conexión para utilizar los nuevos nombres de proveedor** . Para obtener más información acerca de esta opción, vea [página general](../general-page-of-integration-services-designers-options.md).<br /><br /> -En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el paquete y cambie manualmente el texto de la propiedad ConnectionString.<br /><br /> Nota: No puede usar los procedimientos anteriores para actualizar una cadena de conexión cuando esta se almacena en un archivo de configuración o en un archivo de origen de datos ni cuando una expresión establece la propiedad `ConnectionString`. Para actualizar la cadena de conexión en estos casos, debe actualizar manualmente el archivo o la expresión.<br /><br /> Para obtener más información sobre los orígenes de datos, vea [Orígenes de datos](../connection-manager/data-sources.md).|  
|Transformación de búsqueda|En el caso de paquetes de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], el proceso de actualización actualiza automáticamente la transformación Búsqueda a la versión actual de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Sin embargo, la versión de este componente tiene algunas capacidades adicionales que podría ser conveniente aprovechar.<br /><br /> Para obtener más información, vea [lookup Transformation](../data-flow/transformations/lookup-transformation.md).|  
|Tarea Script y componente Script|El caso de paquetes [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] , el proceso de actualización migra automáticamente los scripts de la tarea Script y del componente Script de VSA a VSTA.<br /><br /> Para más información sobre los cambios que es posible que haya que realizar en los scripts antes de la migración y sobre los errores de conversión de scripts, vea [Migrar scripts a VSTA](../../sql-server/install/migrate-scripts-to-vsta.md).|  
  
### <a name="scripts-that-depend-on-adodbdll"></a>Scripts que dependen de ADODB.dll  
 Es posible que los scripts Tarea de script y Componente de script que hacen referencia de forma explícita a ADODB.dll no se actualicen o ejecuten en equipos sin [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] instalado. Para actualizar los scripts Tarea de script o Componente de script, se recomienda que quite la dependencia de ADODB.dll.  Ado.Net es la alternativa recomendada para el código administrado como scripts VB y C#.  
  
## <a name="external-resources"></a>Recursos externos  
  
-   Artículo técnico, [5 sugerencias para realizar una actualización sin problemas de SSIS a SQL Server 2012](https://go.microsoft.com/fwlink/?LinkId=235321), en msdn.microsoft.com.  
  
-   Entrada de blog [Hacer que las extensiones y aplicaciones personalizadas existentes de SSIS funcionen en Denali](https://go.microsoft.com/fwlink/?LinkId=238157), en blogs.msdn.com.  
  
-   Difusión por web [Actualizar paquetes de SSIS a SQL Server 2012](https://go.microsoft.com/fwlink/?LinkId=258674), en channel9.msdn.com.  
  
  
