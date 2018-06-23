---
title: Implementar una extensión de procesamiento de datos | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data processing extensions [Reporting Services], deploying
- Extension element
- deploying [Reporting Services], extensions
ms.assetid: e5c0b5a9-1386-47cb-aade-96653ecfaa54
caps.latest.revision: 34
author: douglaslM
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 63628c1be1803833a65875ddf75d4434af38c87f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36200488"
---
# <a name="deploying-a-data-processing-extension"></a>Implementar una extensión de procesamiento de datos
  Después de escribir y compilar la extensión de procesamiento de datos de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] en una biblioteca de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)], es necesario hacer que el servidor de informes y el Diseñador de informes la puedan detectar. Esto es tan fácil como copiar la extensión en los directorios adecuados y agregar entradas a los archivos de configuración de [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] correspondientes.  
  
## <a name="configuration-file-extension-element"></a>Elemento de extension de archivos de configuración  
 Las extensiones de procesamiento de datos que implementa en el servidor de informes o el Diseñador de informes tienen que escribirse como elementos **Extension** en los archivos de configuración. Estos archivos son RSReportServer.config para el servidor de informes y RSReportDesigner.config para el Diseñador de informes.  
  
 En la tabla siguiente se describen los atributos del elemento **Extension** correspondientes a las extensiones de procesamiento de datos.  
  
|Attribute|Descripción|  
|---------------|-----------------|  
|`Name`|Un nombre único para la extensión, por ejemplo "SQL" para la extensión de procesamiento de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] u "OLEDB" para la extensión de procesamiento de datos de OLE DB. La longitud máxima para el atributo `Name` es de 255 caracteres. El nombre debe ser único entre todas las entradas en el elemento **Extension** del archivo de configuración.|  
|`Type`|Lista separada por comas que incluye el espacio de nombres completo junto con el nombre del ensamblado.|  
|`Visible`|El valor `false` indica que la extensión de procesamiento de datos no debería estar visible en las interfaces de usuario. Si el atributo no está incluido, el valor predeterminado es `true`.|  
  
 Para más información sobre los archivos RSReportServer.config o RSReportDesigner.config, vea [Archivos de configuración de Reporting Services](../../report-server/reporting-services-configuration-files.md).  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Cómo implementar una extensión de procesamiento de datos en un servidor de informes](deploying-a-data-processing-extension-to-a-report-server.md)|Describe cómo implementar la extensión de procesamiento de datos para un servidor de informes.|  
|[Cómo implementar una extensión de procesamiento de datos en el Diseñador de informes](deploying-a-data-processing-extension-to-report-designer.md)|Describe cómo implementar la extensión de procesamiento de datos para el Diseñador de informes.|  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de Reporting Services](../reporting-services-extensions.md)   
 [Implementar una extensión de procesamiento de datos](implementing-a-data-processing-extension.md)   
 [Biblioteca de extensiones de Reporting Services](../reporting-services-extension-library.md)  
  
  