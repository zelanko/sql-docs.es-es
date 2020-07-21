---
title: Propiedad RSWindowsExtendedProtectionLevel (MSReportServer_ConfigurationSetting de WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 162ffe86-69c3-49d2-b9ed-49d097c05551
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f30e5d2399c643e4bc3be5ade3789280dba610f6
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66097012"
---
# <a name="rswindowsextendedprotectionlevel-property-wmi-msreportserver_configurationsetting"></a>Propiedad RSWindowsExtendedProtectionLevel (WMI MSReportServer_ConfigurationSetting)
  Devuelve un valor de cadena que indica el nivel de protección con que se ha configurado el servidor de informes. Esta propiedad es de solo lectura.  
  
## <a name="syntax"></a>Sintaxis  
  
```vb  
Public Dim RSWindowsExtendedProtectionLevel As String  
```  
  
```csharp  
public string RSWindowsExtendedProtectionLevel;  
```  
  
## <a name="remarks"></a>Observaciones  
 Devuelve un valor de cadena que indica el nivel de protección con que se ha configurado el servidor de informes. Si el servidor de informes al que se conecta el proveedor de WMI no admite la protección extendida, se devuelve "" (cadena vacía). En la lista siguiente se muestran los valores válidos:  
  
 `"Off" | "Allow" | "Require"`  
  
## <a name="example-code"></a>Código de ejemplo  
 [Clase MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-class.md)  
  
## <a name="see-also"></a>Consulte también  
 [Propiedad RSWindowsExtendedProtectionScenario &#40;MSReportServer_ConfigurationSetting de WMI&#41;](rswindowsextendedprotectionscenario-property.md)   
 [Método SetExtendedProtectionSettings &#40;MSReportServer_ConfigurationSetting de WMI&#41;](configurationsetting-method-setextendedprotectionsettings.md)   
 [Protección ampliada para la autenticación con Reporting Services](../security/extended-protection-for-authentication-with-reporting-services.md)   
 [Archivo de configuración RSReportServer](../report-server/rsreportserver-config-configuration-file.md)  
  
  
