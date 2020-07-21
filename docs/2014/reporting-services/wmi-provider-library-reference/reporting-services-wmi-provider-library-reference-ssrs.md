---
title: Referencia de la biblioteca de proveedores WMI de Reporting Services (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- Reporting Services WMI Provider Library
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- WMI provider [Reporting Services], library
ms.assetid: 17ba711d-7eff-4423-9168-63dc425a3428
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2a98ca22f9d34627e484a698dcf540b31808d07e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66097021"
---
# <a name="reporting-services-wmi-provider-library-reference-ssrs"></a>Referencia de la biblioteca de proveedores WMI de Reporting Services (SSRS)
  El proveedor de Instrumental de administración de Windows (WMI) [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] admite operaciones de WMI que le permiten escribir scripts y código para modificar la configuración del servidor de informes y del Administrador de informes.  
  
 Por ejemplo, si quiere cambiar si se usará la seguridad integrada cuando el servidor de informes se conecte a la base de datos del servidor de informes, cree una instancia de la clase MSReportServer_ConfigurationSetting y use la propiedad DatabaseIntegratedSecurity de la instancia del servidor de informes. Las clases que se muestran en la tabla siguiente representan los componentes  de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Las clases se definen en los espacios de nombres [!INCLUDE[ssRSWMInmspc](../../includes/ssrswminmspc-md.md)] o [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)] . Cada una de las clases admite las operaciones de la lectura y escritura. Las operaciones de creación no se admiten.  
  
## <a name="classes"></a>Clases  
 [MSReportServer_Instance, clase](msreportserver-instance-class.md)  
 Proporciona la información básica requerida para que un cliente se conecte a un servidor de informes instalado.  
  
 [Clase MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-class.md)  
 Representa la instalación y los parámetros de tiempo de ejecución de una instancia del servidor de informes. Estos parámetros se guardan en el archivo de configuración del servidor de informes.  
  
 Para obtener más información acerca de las operaciones WMI, vea la documentación del SDK [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] de WMI que se incluye con el SDK.  
  
## <a name="see-also"></a>Consulte también  
 [Acceder al proveedor de Reporting Services WMI](../tools/access-the-reporting-services-wmi-provider.md)   
 [Referencia técnica &#40;SSRS&#41;](../technical-reference-ssrs.md)  
  
  
