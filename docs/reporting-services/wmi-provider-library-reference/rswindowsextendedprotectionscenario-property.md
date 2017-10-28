---
title: Propiedad RSWindowsExtendedProtectionScenario | Documentos de Microsoft
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5ac7ab80-9adf-4f65-abfa-fedf53b082b5
caps.latest.revision: 6
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 6449b0b9d9e27c860d3246b4992cac6405af731f
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="rswindowsextendedprotectionscenario-property"></a>Propiedad RSWindowsExtendedProtectionScenario
  Devuelve un valor de cadena que indica el escenario de protección extendida que permite la configuración del servidor de informes.  
  
## <a name="syntax"></a>Sintaxis  
  
```vb  
Public Dim RSWindowsExtendedProtectionScenario As String  
```  
  
```csharp  
public string RSWindowsExtendedProtectionScenario;  
```  
  
## <a name="remarks"></a>Comentarios  
 Devuelve un valor de cadena que indica el escenario de protección extendida que permite la configuración del servidor de informes. Si el servidor de informes al que se conecta el proveedor de WMI no admite la protección extendida se devuelve "" (cadena vacía).  
  
 En la lista siguiente se muestran los valores válidos:  
  
 `”Any | Proxy | Direct”`  
  
## <a name="example-code"></a>Código de ejemplo  
 [Clase MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## <a name="see-also"></a>Vea también  
 [Propiedad RSWindowsExtendedProtectionLevel &#40; WMI MSReportServer_ConfigurationSetting &#41;](../../reporting-services/wmi-provider-library-reference/rswindowsextendedprotectionlevel-property.md)   
 [Método SetExtendedProtectionSettings &#40; WMI MSReportServer_ConfigurationSetting &#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setextendedprotectionsettings.md)   
 [Protección ampliada para la autenticación con Reporting Services](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md)   
 [Archivo de configuración RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)  
  
  

