---
title: Propiedad RSWindowsExtendedProtectionScenario | Microsoft Docs
ms.date: 03/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
ms.assetid: 5ac7ab80-9adf-4f65-abfa-fedf53b082b5
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 24b73ad1d226603215507a899b036c2702e09a18
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 05/14/2019
ms.locfileid: "65571109"
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
  
## <a name="remarks"></a>Notas  
 Devuelve un valor de cadena que indica el escenario de protección extendida que permite la configuración del servidor de informes. Si el servidor de informes al que se conecta el proveedor de WMI no admite la protección extendida, se devuelve "" (cadena vacía).  
  
 En la lista siguiente se muestran los valores válidos:  
  
 `"Any | Proxy | Direct"`  
  
## <a name="example-code"></a>Código de ejemplo  
 [Clase MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## <a name="see-also"></a>Consulte también  
 [Propiedad RSWindowsExtendedProtectionLevel &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/rswindowsextendedprotectionlevel-property.md)   
 [Método SetExtendedProtectionSettings &#40;MSReportServer_ConfigurationSetting de WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setextendedprotectionsettings.md)   
 [Protección ampliada para la autenticación con Reporting Services](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md)   
 [El archivo de configuración RSReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)  
  
  
