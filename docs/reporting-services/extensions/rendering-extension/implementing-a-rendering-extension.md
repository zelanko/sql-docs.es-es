---
title: "Implementar una extensión de representación | Documentos de Microsoft"
ms.custom: 
ms.date: 03/16/2017
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
- rendering extensions [Reporting Services]
- custom rendering extensions [Reporting Services]
- transformations [Reporting Services]
- extensions [Reporting Services], rendering
- rendering extensions [Reporting Services], implementing
ms.assetid: 4a5c64f5-2391-4597-ba3f-81d265b23703
caps.latest.revision: 34
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: c6be8db763c82a47d0635169f33a0f0543910abe
ms.contentlocale: es-es
ms.lasthandoff: 08/12/2017

---
# <a name="implementing-a-rendering-extension"></a>Implementar una extensión de representación
  Una extensión de representación es un componente o módulo de un servidor de informes que transforma los datos de informes y la información de diseño en un formato específico del dispositivo. Reporting Services de SQL Server incluye seis extensiones de representación: HTML, Excel, Word, CSV o Text, XML, Image y PDF. Puede crear extensiones de representación adicionales para generar informes en otros formatos.  
  
> [!NOTE]  
>  Para determinar qué extensiones de representación están disponibles, puede ver la lista de extensiones instaladas en el archivo RSReportServer.config.  
  
## <a name="in-this-section"></a>En esta sección  
 [Información general de las extensiones de representación](../../../reporting-services/extensions/rendering-extension/rendering-extensions-overview.md)  
 Explica cómo escribir una extensión de representación personalizada para [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
 [Ejecución de la interfaz IRenderingExtension](../../../reporting-services/extensions/rendering-extension/implementing-the-irenderingextension-interface.md)  
 Describe los atributos de una extensión de representación.  
  
 [Implementación de una extensión de representación](../../../reporting-services/extensions/rendering-extension/deploying-a-rendering-extension.md)  
 Describe cómo implementar una extensión de representación en un servidor de informes.  
  
 [Eliminación de una extensión de representación](../../../reporting-services/extensions/rendering-extension/removing-a-rendering-extension.md)  
 Describe cómo quitar una extensión de representación de un servidor de informes.  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de Reporting Services](../../../reporting-services/extensions/reporting-services-extensions.md)   
 [Biblioteca de extensión de Reporting Services](../../../reporting-services/extensions/reporting-services-extension-library.md)  
  
  

