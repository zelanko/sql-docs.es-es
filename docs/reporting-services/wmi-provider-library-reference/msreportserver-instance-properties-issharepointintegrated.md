---
title: Propiedad IsSharePointIntegrated (WMI MSReportServer_Instance) | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- IsSharePointIntegrated property
ms.assetid: e21d00ad-5d9a-4290-8d74-7eeeda39e1ed
caps.latest.revision: 13
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: a4a86ce7dbb8336aaa70cb2f93debe5dd7f9f70f
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="msreportserverinstance-properties---issharepointintegrated"></a>Propiedades de MSReportServer_Instance - IsSharePointIntegrated
  Especifica si el servidor de informes está en modo integrado de SharePoint. A partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], esta propiedad siempre devuelve **False** , porque en el modo de SharePoint las instancias de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] son servicios compartidos de SharePoint y los proveedores WMI no las controlan.  
  
## <a name="syntax"></a>Sintaxis  
  
```vb  
Public Dim IsSharePointIntegrated As Boolean  
```  
  
```csharp  
public Boolean IsSharePointIntegrated;  
```  
  
## <a name="property-values"></a>Valores de propiedad  
 Un valor **Boolean** que indica si el servidor de informes está en modo integrado de SharePoint.  
  
## <a name="requirements"></a>Requisitos  
 **Namespace:**[!INCLUDE[ssRSWMInmspc](../../includes/ssrswminmspc-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Miembros de MSReportServer_Instance](../../reporting-services/wmi-provider-library-reference/msreportserver-instance-members.md)   
 [Clase MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
  
