---
title: Referencia de la biblioteca de proveedores WMI de Reporting Services (SSRS) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
apiname:
- Reporting Services WMI Provider Library
apilocation:
- reportingservices.mof
helpviewer_keywords:
- WMI provider [Reporting Services], library
ms.assetid: 17ba711d-7eff-4423-9168-63dc425a3428
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: af3b51f934b9b0221747116772af7a747813e70f
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 05/14/2019
ms.locfileid: "65571060"
---
# <a name="reporting-services-wmi-provider-library-reference-ssrs"></a>Referencia de la biblioteca de proveedores WMI de Reporting Services (SSRS)
  El proveedor de Instrumental de administración de Windows (WMI) [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] admite operaciones de WMI que le permiten escribir scripts y código para modificar la configuración del servidor de informes y del Administrador de informes.  
  
 Por ejemplo, si quiere cambiar si se usará la seguridad integrada cuando el servidor de informes se conecte a la base de datos del servidor de informes, cree una instancia de la clase MSReportServer_ConfigurationSetting y use la propiedad DatabaseIntegratedSecurity de la instancia del servidor de informes. Las clases que se muestran en la tabla siguiente representan los componentes  de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Las clases se definen en los espacios de nombres [!INCLUDE[ssRSWMInmspc](../../includes/ssrswminmspc-md.md)] o [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)] . Cada una de las clases admite las operaciones de la lectura y escritura. Las operaciones de creación no se admiten.  
  
## <a name="classes"></a>Clases  
 [Clase MSReportServer_Instance](../../reporting-services/wmi-provider-library-reference/msreportserver-instance-class.md)  
 Proporciona la información básica requerida para que un cliente se conecte a un servidor de informes instalado.  
  
 [Clase MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
 Representa la instalación y los parámetros de tiempo de ejecución de una instancia del servidor de informes. Estos parámetros se guardan en el archivo de configuración del servidor de informes.  
  
 Para obtener más información acerca de las operaciones WMI, vea la documentación de SDK WMI que se incluye con el SDK de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] .  
  
## <a name="see-also"></a>Consulte también  
 [Obtener acceso al proveedor WMI de Reporting Services](../../reporting-services/tools/access-the-reporting-services-wmi-provider.md)   
 [Referencia técnica &#40;SSRS&#41;](../../reporting-services/technical-reference-ssrs.md)  
  
  
