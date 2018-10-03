---
title: Implementar una extensión de representación | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.topic: reference
helpviewer_keywords:
- rendering extensions [Reporting Services]
- custom rendering extensions [Reporting Services]
- transformations [Reporting Services]
- extensions [Reporting Services], rendering
- rendering extensions [Reporting Services], implementing
ms.assetid: 4a5c64f5-2391-4597-ba3f-81d265b23703
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 665b13c8a163c67a800ee0a1771da46af58ab67c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48113711"
---
# <a name="implementing-a-rendering-extension"></a>Implementar una extensión de representación
  Una extensión de representación es un componente o módulo de un servidor de informes que transforma los datos de informes y la información de diseño en un formato específico del dispositivo. Reporting Services de SQL Server incluye seis extensiones de representación: HTML, Excel, Word, CSV o Text, XML, Image y PDF. Puede crear extensiones de representación adicionales para generar informes en otros formatos.  
  
> [!NOTE]  
>  Para determinar qué extensiones de representación están disponibles, puede ver la lista de extensiones instaladas en el archivo RSReportServer.config.  
  
## <a name="in-this-section"></a>En esta sección  
 [Información general de las extensiones de representación](rendering-extensions-overview.md)  
 Explica cómo escribir una extensión de representación personalizada para [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)].  
  
 [Ejecución de la interfaz IRenderingExtension](implementing-the-irenderingextension-interface.md)  
 Describe los atributos de una extensión de representación.  
  
 [Implementación de una extensión de representación](deploying-a-rendering-extension.md)  
 Describe cómo implementar una extensión de representación en un servidor de informes.  
  
 [Eliminación de una extensión de representación](removing-a-rendering-extension.md)  
 Describe cómo quitar una extensión de representación de un servidor de informes.  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de Reporting Services](../reporting-services-extensions.md)   
 [Biblioteca de extensiones de Reporting Services](../reporting-services-extension-library.md)  
  
  
