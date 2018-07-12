---
title: Método SetExtendedProtectionSettings (MSReportServer_ConfigurationSetting de WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 2d8e7232-42f4-41b6-98eb-c856f6c85d8c
caps.latest.revision: 7
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: fbc49b6978c9d60344795b3c05729e14e9fa3838
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37181482"
---
# <a name="setextendedprotectionsettings-method-wmi-msreportserverconfigurationsetting"></a>Método SetExtendedProtectionSettings (WMI MSReportServer_ConfigurationSetting)
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
  
 `”Off | Allow | Require”`  
  
 *ExtendedProtectionScenario*  
 Establece el RSWindowsExtendedProtectionScenario en el archivo RSReportserver.config. El valor es obligatorio y no distingue entre mayúsculas y minúsculas.  
  
 En la lista siguiente se muestran los valores válidos:  
  
 `”Any” | “Proxy” | “Direct”`  
  
## <a name="remarks"></a>Notas  
 Las propiedades RSWindowsExtendedProtectionLevel y RSWindowsExtendedProtectionScenario se aplican cuando AuthenticationTypes del archivo RSReportServer.config incluye RSWindowNTLM, RSWindowsNegotiate o RSWindowsKerberos. El establecimiento de estas propiedades afecta a cómo los usuarios y el software cliente se autentican con un servidor de informes. Se recomienda que lea la documentación sobre protección extendida antes de establecer ExtendedProtectionLevel en `Allow` o `Require`.  
  
 Para establecer ExtendedProtectionLevel, el usuario debe ser miembro del grupo de administradores integrado (BUILTIN\Administrators) en el servidor de informes.  
  
## <a name="requirements"></a>Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Propiedad RSWindowsExtendedProtectionScenario &#40;MSReportServer_ConfigurationSetting de WMI&#41;](rswindowsextendedprotectionscenario-property.md)   
 [Propiedad RSWindowsExtendedProtectionLevel &#40;MSReportServer_ConfigurationSetting de WMI&#41;](rswindowsextendedprotectionlevel-property.md)   
 [Protección ampliada para la autenticación con Reporting Services](../security/extended-protection-for-authentication-with-reporting-services.md)   
 [Archivo de configuración RSReportServer](../report-server/rsreportserver-config-configuration-file.md)  
  
  
