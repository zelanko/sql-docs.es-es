---
title: Propiedades del servidor de Analysis Services | Documentos de Microsoft
ms.custom: ''
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SSAS, configuration properties
- Analysis Services, configuration properties
- SQL Server Analysis Services, configuration properties
- configuration options [Analysis Services]
- server properties [Analysis Services]
- properties [Analysis Services], configuration
- properties [Analysis Services]
ms.assetid: 274b89cd-14ed-4666-bc13-eedf1de51e18
caps.latest.revision: 21
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 383edec320f81f30c58b0dcbdcbe4a0bd979d106
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="server-properties-in-analysis-services"></a>Configurar las propiedades de servidor en Analysis Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Un administrador de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] puede modificar las propiedades de configuración predeterminadas del servidor de una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Cada instancia tiene sus propias propiedades de configuración, que se establecen independientemente de las demás instancias en el mismo servidor.  
  
 Para configurar el servidor, use SQL Server Management Studio o modifique el archivo msmdsrv.ini de una instancia específica.  
 
Las páginas de propiedades de SQL Server Management Studio muestran un subconjunto de las propiedades con más probabilidad de ser modificadas. La lista completa de propiedades se encuentra en el archivo msmdsrv.ini.   
  
> [!NOTE]  
>  En una instalación predeterminada, msmdsrv.ini se encuentra en la carpeta \Archivos de programa\Microsoft SQL Server\MSAS13.MSSQLSERVER\OLAP \Config.
> 
> Otras propiedades que afectan a la configuración del servidor incluyen las propiedades de configuración de implementación de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]. Para más información sobre estas propiedades, vea [Especificar la configuración para la implementación de soluciones](../../analysis-services/multidimensional-models/deployment-script-files-solution-deployment-config-settings.md).
 
##  <a name="bkmk_config"></a> Configurar propiedades en Management Studio 
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conéctese a una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
2. En el Explorador de objetos, haga clic con el botón derecho en la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y luego haga clic en **Propiedades**. Aparecerá la página General mostrando las propiedades que se utilizan con más frecuencia.  

3.  Para ver propiedades adicionales, active la casilla **Mostrar propiedades avanzadas (todas)** en la parte inferior de la página.  
  
     La modificación de las propiedades de servidor solo se admite en los servidores en modo tabular y modo multidimensional. Si ha instalado [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)], use siempre los valores predeterminados, a menos que el servicio de soporte técnico de Microsoft le indique lo contrario.  
  
     Para obtener información sobre cómo resolver problemas de funcionamiento o de rendimiento mediante las propiedades de servidor, vea la [Guía de operaciones de SQL Server 2008 R2 Analysis Services](http://go.microsoft.com/fwlink/?LinkID=225539).  
  
     También puede leer sobre las propiedades del servidor (que en gran parte no se han cambiado en las últimas versiones) en estas notas del producto de Microsoft, [SQL Server 2005 Analysis Services (SSAS) Server Properties (Propiedades del servidor SQL Server 2005 Analysis Services (SSAS))](http://go.microsoft.com/fwlink/?LinkID=199102).    
  
##  <a name="bkmk_msmdsrvini"></a> Configurar propiedades en msmdsrv.ini
  Algunas propiedades se pueden establecer solo en el archivo msmdrsrv.ini. Si la propiedad que desea establecer no está visible incluso después de mostrar las propiedades avanzadas, es posible que tenga que modificar el archivo msmdsrv.ini directamente.
  
1.  Compruebe la propiedad **DataDir** en la página de propiedades General de Management Studio para comprobar la ubicación de los archivos de programa de Analysis Services, incluido el archivo msmdsrv.ini.

     En un servidor que tiene varias instancias, la comprobación de la ubicación del archivo de programa garantiza la modificación del archivo correcto.  
  
2.  Vaya a la carpeta **config** de la ubicación de la carpeta de archivos del programa.

3. Cree una copia de seguridad del archivo en caso de que necesite revertir al archivo original.  
  
4.  Utilice un editor de texto para ver o modificar el archivo msmdsrv.ini.  
  
5.  Guarde el archivo y reinicie el servicio.  
  
##  <a name="bkmk_ref"></a> Referencia de las propiedades de servidor  
  
 En los siguientes temas se explican las diversas propiedades de configuración de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] :  
  
|Tema|Description|  
|-----------|-----------------|  
|[Propiedades generales](../../analysis-services/server-properties/general-properties.md)|Las propiedades generales son las básicas y las avanzadas, e incluyen propiedades que definen el directorio de datos, el directorio de copia de seguridad y otros comportamientos del servidor.|  
|[Propiedades de minería de datos](../../analysis-services/server-properties/data-mining-properties.md)|Las propiedades de minería de datos controlan qué algoritmos de minería de datos están habilitados y cuáles no. De manera predeterminada, todos los algoritmos están habilitados.| 
|[Propiedades de DAX](../../analysis-services/server-properties/dax-properties.md)|Define las propiedades relacionadas con las consultas DAX.|
|DSO|DSO ya no es compatible. Se omiten las propiedades de DSO.|  
|[Propiedades de características](../../analysis-services/server-properties/feature-properties.md)|Las propiedades de características corresponden a las características del producto, la mayor parte de ellas avanzadas, incluidas las propiedades que controlan los vínculos entre las instancias de servidor.|  
|[FILESTORE, propiedades](../../analysis-services/server-properties/filestore-properties.md)|Las propiedades de almacén de archivos solamente sirven para uso avanzado. Incluyen valores de configuración avanzada de la administración de memoria.|  
|[Propiedades del Administrador de bloqueos](../../analysis-services/server-properties/lock-manager-properties.md)|Las propiedades del administrador de bloqueos definen los comportamientos del servidor relativos a bloqueos y tiempos de espera. La mayoría de estas propiedades solo sirven para uso avanzado.|  
|[Propiedades de registro](../../analysis-services/server-properties/log-properties.md)|Las propiedades del registro controlan si los eventos inician la sesión en el servidor, dónde y cómo. Esto incluye el registro de errores, el registro de excepciones, la caja negra SQL, el registro de consultas y los seguimientos.|  
|[Propiedades de memoria](../../analysis-services/server-properties/memory-properties.md)|Las propiedades de memoria controlan la forma en la que el servidor utiliza la memoria. Son fundamentalmente para uso avanzado.|  
|[Propiedades de red](../../analysis-services/server-properties/network-properties.md)|Las propiedades de red controlan el comportamiento del servidor relativo a redes, incluidas las propiedades que controlan la compresión y los elementos XML binarios. La mayoría de estas propiedades solo sirven para uso avanzado.|  
|[Propiedades OLAP](../../analysis-services/server-properties/olap-properties.md)|Las propiedades OLAP controlan el procesamiento de cubos y dimensiones, el procesamiento diferido, el almacenamiento de datos en caché y el comportamiento de las consultas. Incluyen propiedades básicas y avanzadas.|  
|[Propiedades de seguridad](../../analysis-services/server-properties/security-properties.md)|La sección de seguridad contiene propiedades básicas y avanzadas que definen permisos de acceso. Esto incluye valores de configuración relacionados con administradores y usuarios.|  
|[Propiedades del grupo de subprocesos](../../analysis-services/server-properties/thread-pool-properties.md)|Las propiedades de grupo de subprocesos controlan cuántos subprocesos crea el servidor. Se trata fundamentalmente de propiedades avanzadas.|  
  
## <a name="see-also"></a>Vea también  
 [Administración de una instancia de Analysis Services](../../analysis-services/instances/analysis-services-instance-management.md)   
 [Especificar la configuración de implementación de soluciones](../../analysis-services/multidimensional-models/deployment-script-files-solution-deployment-config-settings.md)  
  
  
