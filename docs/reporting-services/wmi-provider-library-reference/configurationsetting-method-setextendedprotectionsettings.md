---
title: Método SetExtendedProtectionSettings (MSReportServer_ConfigurationSetting de WMI) | Microsoft Docs
ms.date: 03/20/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
ms.assetid: 2d8e7232-42f4-41b6-98eb-c856f6c85d8c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: cbfd4392572713e1c81fef07467842e18549e089
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "65581014"
---
# <a name="configurationsetting-method---setextendedprotectionsettings"></a>Método de ConfigurationSetting: SetExtendedProtectionSettings
  El método SetExtendedProtectionSettings se utiliza para establecer las propiedades RSWindowsExtendedProtectionScenario y RSWindowsExtendedProtectionLevel en el archivo de configuración RSReportServer.config de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
## <a name="syntax"></a>Sintaxis  
  
```vb  
Public Sub SetExtendedProtectionSettings( _  
        ByVal ExtendedProtectionLevel As String, _  
        ByVal ExtendedProtectionScenario As String, _  
        ByRef Warnings() As String, _  
        ByRef Length As Int32, _  
        ByRef HRESULT As Int32)  
```  
  
```csharp  
public void SetExtendedProtectionSettings(  
            string ExtendedProtectionLevel,  
            string ExtendedProtectionScenario,  
            out string[] Warnings,  
            out Int32 Length,  
            out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parámetros  
 *ExtendedProtectionLevel*  
 Establece el RSWindowsExtendedProtectionLevel en el archivo RSRreportserver.config. El valor es obligatorio y no distingue entre mayúsculas y minúsculas.  
  
 En la lista siguiente se muestran los valores válidos:  
  
 `"Off | Allow | Require"`  
  
 *ExtendedProtectionScenario*  
 Establece el RSWindowsExtendedProtectionScenario en el archivo RSReportserver.config. El valor es obligatorio y no distingue entre mayúsculas y minúsculas.  
  
 En la lista siguiente se muestran los valores válidos:  
  
 `"Any" | "Proxy" | "Direct"`  
  
## <a name="remarks"></a>Observaciones  
 Las propiedades RSWindowsExtendedProtectionLevel y RSWindowsExtendedProtectionScenario se aplican cuando AuthenticationTypes del archivo RSReportServer.config incluye RSWindowNTLM, RSWindowsNegotiate o RSWindowsKerberos. El establecimiento de estas propiedades afecta a cómo los usuarios y el software cliente se autentican con un servidor de informes. Se recomienda leer la documentación sobre protección extendida antes de establecer ExtendedProtectionLevel en **Allow** o **Require**.  
  
 Para establecer ExtendedProtectionLevel, el usuario debe ser miembro del grupo de administradores integrado (BUILTIN\Administrators) en el servidor de informes.  
  
## <a name="requirements"></a>Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte también  
 [Propiedad RSWindowsExtendedProtectionScenario &#40;MSReportServer_ConfigurationSetting de WMI&#41;](../../reporting-services/wmi-provider-library-reference/rswindowsextendedprotectionscenario-property.md)   
 [Propiedad RSWindowsExtendedProtectionLevel &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/rswindowsextendedprotectionlevel-property.md)   
 [Protección ampliada para la autenticación con Reporting Services](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md)   
 [Archivo de configuración RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)  
  
  
