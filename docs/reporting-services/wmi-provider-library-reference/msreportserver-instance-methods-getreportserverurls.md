---
title: Método GetReportServerUrls (MSReportServer_Instance de WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/09/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: ''
ms.component: wmi-provider-library-reference
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- GetReportServerUrls method
ms.assetid: 4865e32c-0114-465a-be8c-be223a7bc09e
caps.latest.revision: 12
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: fb88837f3c9393c561e65c13656bb0e87a516325
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2018
---
# <a name="msreportserverinstance-methods---getreportserverurls"></a>Métodos MSReportServer_Instance - GetReportServerUrls
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
  
 *Longitud*  
 Un valor entero que contiene la longitud de las matrices devueltas.  
  
 *HRESULT*  
 Un valor que indica éxito o un código de error.  
  
## <a name="return-values"></a>Valores devueltos  
  
## <a name="remarks"></a>Notas  
 Se llama a los métodos expuestos por objetos de administración de WMI mediante la función InvokeMethod. Para obtener más información, vea "Ejecutar métodos en objetos de administración" en la la documentación de WMI de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework.  
  
## <a name="requirements"></a>Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspc](../../includes/ssrswminmspc-md.md)]  
  
## <a name="see-also"></a>Ver también  
 [Miembros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
