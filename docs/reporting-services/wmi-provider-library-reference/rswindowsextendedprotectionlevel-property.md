---
title: Propiedad RSWindowsExtendedProtectionLevel | Microsoft Docs
ms.date: 03/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
ms.assetid: 162ffe86-69c3-49d2-b9ed-49d097c05551
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 7854821a9f43bc234490d915ff75339e250f6c39
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65571079"
---
# <a name="rswindowsextendedprotectionlevel-property"></a>Propiedad RSWindowsExtendedProtectionLevel
  Devuelve un valor de cadena que indica el nivel de protección con que se ha configurado el servidor de informes. Esta propiedad es de solo lectura.  
  
## <a name="syntax"></a>Sintaxis  
  
```vb  
Public Dim RSWindowsExtendedProtectionLevel As String  
```  
  
```csharp  
public string RSWindowsExtendedProtectionLevel;  
```  
  
## <a name="remarks"></a>Notas  
 Devuelve un valor de cadena que indica el nivel de protección con que se ha configurado el servidor de informes. Si el servidor de informes al que se conecta el proveedor de WMI no admite la protección extendida, se devuelve "" (cadena vacía). En la lista siguiente se muestran los valores válidos:  
  
 `"Off" | "Allow" | "Require"`  
  
## <a name="example-code"></a>Código de ejemplo  
 [Clase MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-class.md)  
  
## <a name="see-also"></a>Consulte también  
 [Propiedad RSWindowsExtendedProtectionScenario &#40;MSReportServer_ConfigurationSetting de WMI&#41;](../../reporting-services/wmi-provider-library-reference/rswindowsextendedprotectionscenario-property.md)   
 [Método SetExtendedProtectionSettings &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setextendedprotectionsettings.md)   
 [Protección ampliada para la autenticación con Reporting Services](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md)   
 [El archivo de configuración RSReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)  
  
  
