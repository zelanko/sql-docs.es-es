---
title: "Quitar una extensión de representación | Documentos de Microsoft"
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
- deleting rendering extensions
- removing rendering extensions
- rendering extensions [Reporting Services], removing
ms.assetid: 2abfebfb-065f-45cc-a904-c914394cf900
caps.latest.revision: 38
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: ea37cf7ac15504a00aeb0f1379e9d48a71231e1c
ms.contentlocale: es-es
ms.lasthandoff: 08/12/2017

---
# <a name="removing-a-rendering-extension"></a>Quitar una extensión de representación
  Para quitar un [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] extensión de representación, basta con quitar el **extensión** elemento de la extensión del archivo rsreportserver.config, situado en **%ProgramFiles%\Microsoft SQL Server\MSRS10_50.\< Nombre de instancia > \Reporting** carpeta. Si ha realizado entradas para un diseñador de informes, así como un servidor de informes, quite el **extensión** elemento desde el [RSReportDesigner Configuration File](../../../reporting-services/report-server/rsreportdesigner-configuration-file.md) así. Después de quitar la información de configuración, la extensión de representación de datos ya no estará disponible en el componente.  
  
## <a name="see-also"></a>Vea también  
 [Archivos de configuración de Reporting Services](../../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [Implementar una extensión de representación](../../../reporting-services/extensions/rendering-extension/implementing-a-rendering-extension.md)   
 [Introducción a las extensiones de representación](../../../reporting-services/extensions/rendering-extension/rendering-extensions-overview.md)   
 [Implementar la interfaz IRenderingExtension](../../../reporting-services/extensions/rendering-extension/implementing-the-irenderingextension-interface.md)   
 [Consideraciones de seguridad para las extensiones](../../../reporting-services/extensions/security-considerations-for-extensions.md)   
 [Implementación de una extensión de representación](../../../reporting-services/extensions/rendering-extension/deploying-a-rendering-extension.md)  
  
  

