---
title: "Biblioteca de extensión de servicios de Reporting | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
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
- namespaces [Reporting Services]
- Reporting Services, extending
- extensions [Reporting Services], library
- library [Reporting Services]
ms.assetid: e8eff470-64d6-41c3-b98b-5ec916c121c3
caps.latest.revision: 33
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: b9a1ce1e388575d6d5b9b46a00dbc85ae8cde84b
ms.contentlocale: es-es
ms.lasthandoff: 06/13/2017

---
# <a name="reporting-services-extension-library"></a>Biblioteca de extensiones de Reporting Services
  La biblioteca de extensiones de Reporting Services es un conjunto de clases, interfaces y tipos de valores que se incluyen en [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Esta biblioteca proporciona acceso a la funcionalidad del sistema y está diseñada para ser la base para que [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] aplicaciones pueden utilizarse para extender [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] componentes.  
  
## <a name="namespaces"></a>Espacios de nombres  
 La biblioteca de extensiones de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] proporciona los espacios de nombres siguientes.  
  
 <xref:Microsoft.ReportingServices.DataProcessing>  
 Contiene las clases e interfaces que le permiten generar componentes que extienden la capacidad de procesamiento de datos de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 <xref:Microsoft.ReportingServices.Interfaces>  
 Contiene las clases e interfaces que permiten construir y enviar notificaciones personalizadas a los usuarios a través de sus propias extensiones de entrega, y construir extensiones de seguridad personalizadas para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 **Microsoft.ReportingServices.ReportRendering**  
 Contiene clases e interfaces que permiten extender las capacidades de representación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Utilizando los miembros de este espacio de nombres junto con los miembros del espacio de nombres <xref:Microsoft.ReportingServices.Interfaces>, puede construir sus propias extensiones de representación personalizadas para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de Reporting Services](../../reporting-services/extensions/reporting-services-extensions.md)  
  
  
