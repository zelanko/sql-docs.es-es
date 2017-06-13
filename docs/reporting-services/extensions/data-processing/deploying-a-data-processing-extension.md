---
title: "Implementar una extensión de procesamiento de datos | Documentos de Microsoft"
ms.custom: 
ms.date: 03/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- data processing extensions [Reporting Services], deploying
- Extension element
- deploying [Reporting Services], extensions
ms.assetid: e5c0b5a9-1386-47cb-aade-96653ecfaa54
caps.latest.revision: 34
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: d312cdf2c5588c8dc12ff000fe4163d7f562ea7f
ms.contentlocale: es-es
ms.lasthandoff: 06/13/2017

---
# <a name="deploying-a-data-processing-extension"></a>Implementar una extensión de procesamiento de datos
  Una vez que haya escrito y compilado la [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] extensión de procesamiento de datos en un [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] biblioteca, debe hacerlo reconocible por el servidor de informes y el Diseñador de informes. Esto es tan fácil como copiar la extensión en los directorios adecuados y agregar entradas a los archivos de configuración de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] correspondientes.  
  
## <a name="configuration-file-extension-element"></a>Elemento de extension de archivos de configuración  
 Las extensiones de procesamiento de datos que se implementan en el servidor de informes o el Diseñador de informes tienen que escribirse como **extensión** elementos en los archivos de configuración. Estos archivos son RSReportServer.config para el servidor de informes y RSReportDesigner.config para el Diseñador de informes.  
  
 En la tabla siguiente se describe los atributos para el **extensión** (elemento) para las extensiones de procesamiento de datos.  
  
|Attribute|Description|  
|---------------|-----------------|  
|**Nombre**|Un nombre único para la extensión, por ejemplo "SQL" para la extensión de procesamiento de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] u "OLEDB" para la extensión de procesamiento de datos de OLE DB. La longitud máxima para el atributo **Name** es de 255 caracteres. El nombre debe ser único entre todas las entradas en el elemento **Extension** del archivo de configuración.|  
|**Tipo**|Lista separada por comas que incluye el espacio de nombres completo junto con el nombre del ensamblado.|  
|**Visible**|Un valor de **false** indica que la extensión de procesamiento de datos no debería estar visible en las interfaces de usuario. Si el atributo no está incluido, el valor predeterminado es **true**.|  
  
 Para obtener más información acerca de los archivos RSReportServer.config o RSReportDesigner.config, vea [Reporting Services Configuration Files](../../../reporting-services/report-server/reporting-services-configuration-files.md).  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Description|  
|-----------|-----------------|  
|[Cómo: implementar una extensión de procesamiento de datos en un servidor de informes](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension-to-a-report-server.md)|Describe cómo implementar la extensión de procesamiento de datos para un servidor de informes.|  
|[Cómo: implementar una extensión de procesamiento de datos en el Diseñador de informes](../../../reporting-services/extensions/data-processing/deploying-a-data-processing-extension-to-report-designer.md)|Describe cómo implementar la extensión de procesamiento de datos para el Diseñador de informes.|  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de Reporting Services](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Implementar una extensión de procesamiento de datos](../../../reporting-services/extensions/data-processing/implementing-a-data-processing-extension.md)   
 [Biblioteca de extensión de Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  
