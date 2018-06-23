---
title: Propiedad RSWindowsExtendedProtectionScenario (MSReportServer_ConfigurationSetting WMI) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 5ac7ab80-9adf-4f65-abfa-fedf53b082b5
caps.latest.revision: 5
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: f6fa7fa258d4638f6dbe7d6626e067b95882a779
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36106266"
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
  
## <a name="remarks"></a>Notas  
 Devuelve un valor de cadena que indica el escenario de protección extendida que permite la configuración del servidor de informes. Si el servidor de informes al que se conecta el proveedor de WMI no admite la protección extendida se devuelve "" (cadena vacía).  
  
 En la lista siguiente se muestran los valores válidos:  
  
 `”Any | Proxy | Direct”`  
  
## <a name="example-code"></a>Código de ejemplo  
 [Clase MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-class.md)  
  
## <a name="see-also"></a>Vea también  
 [Propiedad RSWindowsExtendedProtectionLevel &#40;MSReportServer_ConfigurationSetting de WMI&#41;](rswindowsextendedprotectionlevel-property.md)   
 [Método SetExtendedProtectionSettings &#40;MSReportServer_ConfigurationSetting de WMI&#41;](configurationsetting-method-setextendedprotectionsettings.md)   
 [Protección ampliada para la autenticación con Reporting Services](../security/extended-protection-for-authentication-with-reporting-services.md)   
 [Archivo de configuración RSReportServer](../report-server/rsreportserver-config-configuration-file.md)  
  
  