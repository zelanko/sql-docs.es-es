---
title: Característica propiedades | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- SQMSupportEnabled property
- ComUdfEnabled property
- LinkToOtherInstanceEnabled property
- ManagedCodeEnabled property
- ConnStringEncryptionEnabled property
- LinkFromOtherInstanceEnabled property
- LinkInsideInstanceEnabled property
- UseCachedPageAllocators property
ms.assetid: a34d046a-6562-4d98-b827-37cebc6d77b4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1cc2d52bd942fe15eeabd72f1c37740637e692d2
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66069050"
---
# <a name="feature-properties"></a>Propiedades de características
  Las propiedades de características corresponden a las características del producto, la mayor parte de ellas avanzadas, incluidas las propiedades que controlan los vínculos entre las instancias de servidor.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] admite las propiedades de servidor enumeradas en la tabla siguiente. Para obtener más información sobre las propiedades de servidor adicionales y cómo establecerlas, vea [Configure Server Properties in Analysis Services](server-properties-in-analysis-services.md).  
  
 **Se aplica a:** Modo de servidor multidimensional únicamente  
  
## <a name="properties"></a>Propiedades  
  
|Property|Default|Descripción|  
|--------------|-------------|-----------------|  
|`ManagedCodeEnabled`|1|Una propiedad booleana que indica si los procedimientos de almacenamiento CLR están habilitados.|  
|`LinkInsideInstanceEnabled`|1|Una propiedad booleana que indica si se puede crear un objeto vinculado dentro de la misma instancia del servidor.|  
|`LinkToOtherInstanceEnabled`|0|Una propiedad booleana que indica si los objetos en servidores remotos se pueden vincular.|  
|`LinkFromOtherInstanceEnabled`|0|Una propiedad booleana que indica si los objetos se pueden vincular desde otras instancias del servidor.|  
|`ConnStringEncryptionEnabled`|1|Una propiedad booleana que indica si la cadena de conexión se cifra en el archivo de configuración del servidor.|  
|`UseCachedPageAllocators`|0|Una propiedad booleana que indica si los asignadores de páginas almacenados en caché están habilitados.|  
|`ComUdfEnabled`|0|Una propiedad booleana que indica si las funciones definidas por el usuario como objetos COM están habilitadas.|  
|`SQMSupportEnabled`|1|Una propiedad booleana que indica si se envían automáticamente informes de uso de características y de errores a [!INCLUDE[msCoName](../../includes/msconame-md.md)] .|  
|`ResourceMonitoringEnabled`|1|Una propiedad booleana que indica si los contadores de supervisión de recursos internos están habilitados. Esta propiedad está activada de forma predeterminada. Cuando se habilita, esta propiedad permite a los contadores recopilar datos de uso acerca de la actividad de la E/S, la memoria y la CPU.<br /><br /> Los contadores de supervisión de recursos internos se usan en las Vistas de administración dinámica (DVM) que informan de la utilización de los recursos. Si deshabilita esta propiedad, las consultas DMV siguen ejecutándose, pero el conjunto de resultados no será válido. Entre las consultas DMV que dependen de esta propiedad se incluyen las siguientes:<br />**Conjunto de filas DISCOVER_OBJECT_ACTIVITY**<br />**Conjunto de filas DISCOVER_COMMAND_OBJECTS**<br />**DISCOVER_SESSIONS** (para SESSION_READS, SESSION_WRITES, SESSION_CPU_TIME_MS)<br /><br /> <br /><br /> En un sistema de varios núcleos que usa la arquitectura NUMA, si se deshabilita esta propiedad, puede mejorar el rendimiento de las consultas, en particular para altas cargas de trabajo multi-usuario. Tendrá que ejecutar pruebas comparativas para determinar si el rendimiento de las consultas mejora al cambiar esta propiedad. Para obtener las prácticas recomendadas para realizar pruebas comparativas, como es borrar la memoria caché y evitar errores comunes, vea la [Guía de operaciones de SQL Server 2008 R2 Analysis Services](https://go.microsoft.com/fwlink/?LinkID=225539).|  
  
## <a name="see-also"></a>Vea también  
 [Configurar las propiedades del servidor en Analysis Services](server-properties-in-analysis-services.md)   
 [Determinar el modo de servidor de una instancia de Analysis Services](../instances/determine-the-server-mode-of-an-analysis-services-instance.md)   
 [Usar vistas de administración dinámica &#40;DMV&#41; para supervisar Analysis Services](../instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)  
  
  
