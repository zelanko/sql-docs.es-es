---
title: Propiedad IsSharePointIntegrated (MSReportServer_Instance de WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- IsSharePointIntegrated property
ms.assetid: e21d00ad-5d9a-4290-8d74-7eeeda39e1ed
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 716ff525b322a5722a097ad69dee3e7c3ee97bb6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48227105"
---
# <a name="issharepointintegrated-property-wmi-msreportserverinstance"></a>Propiedad IsSharePointIntegrated (WMI MSReportServer_Instance)
  Especifica si el servidor de informes está en modo integrado de SharePoint. A partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], esta propiedad siempre devuelve `False`, porque en modo de SharePoint las instancias de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] son servicios compartidos de SharePoint y los proveedores WMI no las controlan.  
  
## <a name="syntax"></a>Sintaxis  
  
```vb  
Public Dim IsSharePointIntegrated As Boolean  
```  
  
```csharp  
public Boolean IsSharePointIntegrated;  
```  
  
## <a name="property-values"></a>Valores de propiedad  
 Un valor `Boolean` que indica si el servidor de informes está en modo integrado de SharePoint.  
  
## <a name="requirements"></a>Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspc](../../includes/ssrswminmspc-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Miembros de MSReportServer_Instance](msreportserver-instance-members.md)   
 [Clase MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-class.md)  
  
  
