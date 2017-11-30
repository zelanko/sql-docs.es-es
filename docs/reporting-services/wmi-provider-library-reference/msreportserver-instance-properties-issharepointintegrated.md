---
title: Propiedad IsSharePointIntegrated (MSReportServer_Instance de WMI) | Microsoft Docs
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
helpviewer_keywords: IsSharePointIntegrated property
ms.assetid: e21d00ad-5d9a-4290-8d74-7eeeda39e1ed
caps.latest.revision: "13"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 28725a99986d738729cda736b7ffcf32a58db2de
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="msreportserverinstance-properties---issharepointintegrated"></a>Propiedades de MSReportServer_Instance: IsSharePointIntegrated
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
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspc](../../includes/ssrswminmspc-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Miembros de MSReportServer_Instance](../../reporting-services/wmi-provider-library-reference/msreportserver-instance-members.md)   
 [Clase MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
  
