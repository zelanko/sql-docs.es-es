---
title: Propiedad RSWindowsExtendedProtectionScenario (MSReportServer_ConfigurationSetting de WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 5ac7ab80-9adf-4f65-abfa-fedf53b082b5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 67a43ee9150f68a55a9999eae5bc6e8d8fc970b2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63022447"
---
# <a name="rswindowsextendedprotectionscenario-property-wmi-msreportserverconfigurationsetting"></a>Propiedad RSWindowsExtendedProtectionScenario (MSReportServer_ConfigurationSetting de WMI)
  Devuelve un valor de cadena que indica el escenario de protección extendida que permite la configuración del servidor de informes.  
  
## <a name="syntax"></a>Sintaxis  
  
```vb  
Public Dim RSWindowsExtendedProtectionScenario As String  
```  
  
```csharp  
public string RSWindowsExtendedProtectionScenario;  
```  
  
## <a name="remarks"></a>Comentarios  
 Devuelve un valor de cadena que indica el escenario de protección extendida que permite la configuración del servidor de informes. Si el servidor de informes al que se conecta el proveedor de WMI no admite la protección extendida, se devuelve "" (cadena vacía).  
  
 En la lista siguiente se muestran los valores válidos:  
  
 `"Any | Proxy | Direct"`  
  
## <a name="example-code"></a>Código de ejemplo  
 [Clase MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-class.md)  
  
## <a name="see-also"></a>Vea también  
 [Propiedad RSWindowsExtendedProtectionLevel &#40;WMI MSReportServer_ConfigurationSetting&#41;](rswindowsextendedprotectionlevel-property.md)   
 [Método SetExtendedProtectionSettings &#40;MSReportServer_ConfigurationSetting de WMI&#41;](configurationsetting-method-setextendedprotectionsettings.md)   
 [Protección ampliada para la autenticación con Reporting Services](../security/extended-protection-for-authentication-with-reporting-services.md)   
 [Archivo de configuración RSReportServer](../report-server/rsreportserver-config-configuration-file.md)  
  
  
