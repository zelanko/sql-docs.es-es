---
title: Referencia (SSRS) de la biblioteca de proveedor WMI de Reporting Services | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- Reporting Services WMI Provider Library
apilocation:
- reportingservices.mof
helpviewer_keywords:
- WMI provider [Reporting Services], library
ms.assetid: 17ba711d-7eff-4423-9168-63dc425a3428
caps.latest.revision: 42
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ce7657f048154ab0cf68c8e160bf1e5e6d15c210
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

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
  
## <a name="see-also"></a>Vea también  
 [Acceso al proveedor WMI de Reporting Services](../../reporting-services/tools/access-the-reporting-services-wmi-provider.md)   
 [Referencia técnica de &#40; SSRS &#41;](../../reporting-services/technical-reference-ssrs.md)  
  
  
