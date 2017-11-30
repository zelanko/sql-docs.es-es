---
title: Propiedad SecureConnectionLevel (MSReportServer_ConfigurationSetting de WMI) | Microsoft Docs
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
apiname: SecureConnectionLevel
apilocation: reportingservices.mof
apitype: MOFDef
helpviewer_keywords: SecureConnectionLevel property
ms.assetid: fd5549e7-b874-41e2-866e-2f58caf6f733
caps.latest.revision: "19"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: be620ce014ce7357a23e20b0cbb61df79775a3b8
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="configurationsetting-property---secureconnectionlevel"></a>Propiedad de ConfigurationSetting: SecureConnectionLevel
  Devuelve el nivel de conexión segura especificado en el archivo RSReportServer.config. Solo lectura.  
  
## <a name="syntax"></a>Sintaxis  
  
```vb  
Public Dim SecureConnectionLevel As Integer  
```  
  
```csharp  
public Integer SecureConnectionLevel;  
```  
  
## <a name="property-values"></a>Valores de propiedad  
 Un valor **Integer** que representa el nivel de conexión segura. Los valores devueltos indican que el SSL está configurado o no. Un valor mayor o igual que 1 indica que SSL está activado. El valor 0 indica que SSL está desactivado.  
  
## <a name="example-code"></a>Código de ejemplo  
 [Clase MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## <a name="requirements"></a>Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Miembros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
