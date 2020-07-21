---
title: Configurar las propiedades del servidor en Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- SSAS, configuration properties
- Analysis Services, configuration properties
- SQL Server Analysis Services, configuration properties
- configuration options [Analysis Services]
- server properties [Analysis Services]
- properties [Analysis Services], configuration
- properties [Analysis Services]
ms.assetid: 274b89cd-14ed-4666-bc13-eedf1de51e18
author: minewiskan
ms.author: owend
ms.openlocfilehash: 1b450d603ec1d7b8c930a0361d8070519b6a2a91
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84940626"
---
# <a name="configure-server-properties-in-analysis-services"></a>Configurar las propiedades de servidor en Analysis Services
  Un administrador de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] puede modificar las propiedades de configuración predeterminadas del servidor para una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Cada instancia tiene sus propias propiedades de configuración que se pueden establecer independientemente de las demás instancias en el mismo servidor.  
  
 Para establecer propiedades de servidor, utilice SQL Server Management Studio o modifique el archivo msmdsrv.ini de una instancia específica.  
  
 Este tema contiene las siguientes secciones:  
  
 [Configurar las propiedades del servidor (instancia)](#bkmk_config)  
  
 [Referencia de propiedades de servidor](#bkmk_ref)  
  
##  <a name="configure-server-instance-properties"></a><a name="bkmk_config"></a>Configurar las propiedades del servidor (instancia)  
 Las páginas de propiedades de SQL Server Management Studio contienen un subconjunto de las propiedades disponibles, que muestran solo las propiedades que es más probable que haya que modificar. El conjunto completo de propiedades se puede encontrar en el archivo msmdsrv.ini.  
  
> [!NOTE]  
>  Este tema no documenta las propiedades de configuración de implementación de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Para obtener más información sobre la configuración de implementación, vea [especificar valores de configuración para la implementación de soluciones](../multidimensional-models/deployment-script-files-solution-deployment-config-settings.md).  
  
#### <a name="view-or-set-configuration-properties-in-management-studio"></a>Ver o establecer propiedades de configuración de Management Studio  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conéctese a una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
     En el Explorador de objetos, haga clic con el botón derecho en la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y luego haga clic en **Propiedades**. Aparecerá la página General mostrando las propiedades que se utilizan con más frecuencia.  
  
2.  Para ver propiedades adicionales, active la casilla **Mostrar propiedades avanzadas (todas)** en la parte inferior de la página.  
  
     La modificación de las propiedades de servidor solo se admite en los servidores en modo tabular y modo multidimensional. Si ha instalado [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)], utilice siempre los valores predeterminados, a menos que un ingeniero de soporte técnico de Microsoft indique lo contrario.  
  
     Para obtener información sobre cómo resolver problemas de funcionamiento o de rendimiento mediante las propiedades de servidor, vea la [Guía de operaciones de SQL Server 2008 R2 Analysis Services](https://go.microsoft.com/fwlink/?LinkID=225539).  
  
     También puede leer sobre las propiedades del servidor (que en gran parte no se han cambiado en las últimas versiones) en estas notas del producto de Microsoft, [SQL Server 2005 Analysis Services (SSAS) Server Properties (Propiedades del servidor SQL Server 2005 Analysis Services (SSAS))](https://go.microsoft.com/fwlink/?LinkID=199102).  
  
    > [!NOTE]  
    >  Algunas propiedades se pueden establecer solo en el archivo msmdrsrv.ini. Si la propiedad que desea establecer no está visible incluso después de mostrar las propiedades avanzadas, es posible que tenga que modificar el archivo msmdsrv.ini directamente.  
  
#### <a name="view-or-edit-configuration-properties-in-the-msmdsrvini-file"></a>Ver o editar las propiedades de configuración del archivo msmdsrv.ini  
  
1.  Antes de comenzar, compruebe la propiedad **DataDir** en la página de propiedades General de Management Studio para comprobar la ubicación de los archivos de programa de Analysis Services, incluido el archivo msmdsrv.ini. Al comprobar la ubicación de los archivos de programa se asegurará de que está modificando el archivo correcto.  
  
    > [!NOTE]  
    >  En una instalación predeterminada, el archivo se encuentra en la carpeta \Archivos de programa\Microsoft SQL Server\MSAS12.MSSQLSERVER\OLAP \Config  
  
2.  Cree una copia de seguridad del archivo en caso de que necesite revertir al archivo original.  
  
3.  Utilice un editor de texto para ver o modificar el archivo msmdsrv.ini.  
  
4.  Después de guardar el archivo, debe reiniciar el servicio.  
  
##  <a name="server-property-reference"></a><a name="bkmk_ref"></a> Referencia de las propiedades de servidor  
 Las propiedades de configuración de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] son importantes para ajustar bien el sistema. Por ejemplo, para hacer que el comportamiento del registro de consultas sea coherente con los requisitos, puede establecer las propiedades relevantes.  
  
 En los siguientes temas se explican las diversas propiedades de configuración de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] :  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Propiedades generales](general-properties.md)|Las propiedades generales son las básicas y las avanzadas, e incluyen propiedades que definen el directorio de datos, el directorio de copia de seguridad y otros comportamientos del servidor.|  
|[Propiedades de minería de datos](data-mining-properties.md)|Las propiedades de minería de datos controlan qué algoritmos de minería de datos están habilitados y cuáles no. De manera predeterminada, todos los algoritmos están habilitados.|  
|DSO|DSO ya no es compatible. Se omiten las propiedades de DSO.|  
|[Propiedades de características](feature-properties.md)|Las propiedades de características corresponden a las características del producto, la mayor parte de ellas avanzadas, incluidas las propiedades que controlan los vínculos entre las instancias de servidor.|  
|[Propiedades de almacén de propiedades](filestore-properties.md)|Las propiedades de almacén de archivos solamente sirven para uso avanzado. Incluyen valores de configuración avanzada de la administración de memoria.|  
|[Propiedades del administrador de bloqueos](lock-manager-properties.md)|Las propiedades del administrador de bloqueos definen los comportamientos del servidor relativos a bloqueos y tiempos de espera. La mayoría de estas propiedades solo sirven para uso avanzado.|  
|[Propiedades del registro](log-properties.md)|Las propiedades del registro controlan si los eventos inician la sesión en el servidor, dónde y cómo. Esto incluye el registro de errores, el registro de excepciones, la caja negra SQL, el registro de consultas y los seguimientos.|  
|[Propiedades de memoria](memory-properties.md)|Las propiedades de memoria controlan la forma en la que el servidor utiliza la memoria. Son fundamentalmente para uso avanzado.|  
|[Propiedades de red](network-properties.md)|Las propiedades de red controlan el comportamiento del servidor relativo a redes, incluidas las propiedades que controlan la compresión y los elementos XML binarios. La mayoría de estas propiedades solo sirven para uso avanzado.|  
|[Propiedades de OLAP](olap-properties.md)|Las propiedades OLAP controlan el procesamiento de cubos y dimensiones, el procesamiento diferido, el almacenamiento de datos en caché y el comportamiento de las consultas. Incluyen propiedades básicas y avanzadas.|  
|[Propiedades de seguridad](security-properties.md)|La sección de seguridad contiene propiedades básicas y avanzadas que definen permisos de acceso. Esto incluye valores de configuración relacionados con administradores y usuarios.|  
|[Propiedades del grupo de subprocesos](thread-pool-properties.md)|Las propiedades de grupo de subprocesos controlan cuántos subprocesos crea el servidor. Se trata fundamentalmente de propiedades avanzadas.|  
  
## <a name="see-also"></a>Consulte también  
 [Administración de instancias de Analysis Services](../instances/analysis-services-instance-management.md)   
 [Especificar la configuración para la implementación de soluciones](../multidimensional-models/deployment-script-files-solution-deployment-config-settings.md)  
  
  
