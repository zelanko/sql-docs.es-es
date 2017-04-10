---
title: "M&#233;todo SetExtendedProtectionSettings (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs"
ms.custom: ""
ms.date: "12/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2d8e7232-42f4-41b6-98eb-c856f6c85d8c
caps.latest.revision: 7
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# M&#233;todo SetExtendedProtectionSettings (WMI MSReportServer_ConfigurationSetting)
  El método SetExtendedProtectionSettings se utiliza para establecer las propiedades RSWindowsExtendedProtectionScenario y RSWindowsExtendedProtectionLevel en el archivo de configuración RSReportServer.config de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
## Sintaxis  
  
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
  
## Parámetros  
 *ExtendedProtectionLevel*  
 Establece el RSWindowsExtendedProtectionLevel en el archivo RSRreportserver.config. El valor es obligatorio y no distingue entre mayúsculas y minúsculas.  
  
 En la lista siguiente se muestran los valores válidos:  
  
 `”Off | Allow | Require”`  
  
 *ExtendedProtectionScenario*  
 Establece el RSWindowsExtendedProtectionScenario en el archivo RSReportserver.config. El valor es obligatorio y no distingue entre mayúsculas y minúsculas.  
  
 En la lista siguiente se muestran los valores válidos:  
  
 `”Any” | “Proxy” | “Direct”`  
  
## Comentarios  
 Las propiedades RSWindowsExtendedProtectionLevel y RSWindowsExtendedProtectionScenario se aplican cuando AuthenticationTypes del archivo RSReportServer.config incluye RSWindowNTLM, RSWindowsNegotiate o RSWindowsKerberos. El establecimiento de estas propiedades afecta a cómo los usuarios y el software cliente se autentican con un servidor de informes. Se recomienda leer la documentación sobre protección extendida antes de establecer ExtendedProtectionLevel en **Allow** o **Require**.  
  
 Para establecer ExtendedProtectionLevel, el usuario debe ser miembro del grupo de administradores integrado (BUILTIN\Administrators) en el servidor de informes.  
  
## Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## Vea también  
 [Propiedad RSWindowsExtendedProtectionScenario &#40;MSReportServer_ConfigurationSetting de WMI&#41;](../../reporting-services/wmi-provider-library-reference/rswindowsextendedprotectionscenario property.md)   
 [Propiedad RSWindowsExtendedProtectionLevel &#40;MSReportServer_ConfigurationSetting de WMI&#41;](../../reporting-services/wmi-provider-library-reference/rswindowsextendedprotectionlevel-property.md)   
 [Protección ampliada para la autenticación con Reporting Services](../../reporting-services/security/extended-protection-for-authentication-with-reporting-services.md)   
 [El archivo de configuración RSReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)  
  
  