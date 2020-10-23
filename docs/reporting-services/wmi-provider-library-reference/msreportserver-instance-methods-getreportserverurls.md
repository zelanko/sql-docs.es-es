---
description: Método GetReportServerUrls (WMI MSReportServer_Instance)
title: Método GetReportServerUrls (MSReportServer_Instance de WMI) | Microsoft Docs
ms.date: 06/09/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: wmi-provider-library-reference
ms.topic: conceptual
helpviewer_keywords:
- GetReportServerUrls method
ms.assetid: 4865e32c-0114-465a-be8c-be223a7bc09e
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: e3b3e0f7e521cd2a105a3cf093c0a179bd7306d7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "92257528"
---
# <a name="msreportserver_instance-methods---getreportserverurls"></a>Métodos MSReportServer_Instance - GetReportServerUrls
  Devuelve una lista de direcciones URL que los usuarios pueden usar para tener acceso al servidor de informes y al [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```vb  
Public Sub GetReportServerUrls (ByRef ApplicationName() As String, ByRef URLs()_  
    As String, ByRef Length As Int32, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void GetReportServerUrls(out string[] applicationName,   
    out string[] URLs, out int length, out int HRESULT);  
```  
  
## <a name="parameters"></a>Parámetros  
 *ApplicationName[]*  
 Una matriz que contiene las aplicaciones instaladas. Los valores son **ReportServerWebService** o **ReportServerWebApp**.  
  
 *URLs[]*  
 Una matriz que contiene las direcciones URL correctamente registradas.  
  
 *Duración*  
 Un valor entero que contiene la longitud de las matrices devueltas.  
  
 *HRESULT*  
 Un valor que indica éxito o un código de error.  
  
## <a name="return-values"></a>Valores devueltos  
  
## <a name="remarks"></a>Observaciones  
 Se llama a los métodos expuestos por objetos de administración de WMI mediante la función InvokeMethod. Para obtener más información, vea "Ejecutar métodos en objetos de administración" en la la documentación de WMI de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework.  
  
## <a name="requirements"></a>Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspc](../../includes/ssrswminmspc-md.md)]  
  
## <a name="see-also"></a>Consulte también  
 [Miembros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
