---
title: "Método GetReportServerUrls (WMI MSReportServer_Instance) | Documentos de Microsoft"
ms.custom: 
ms.date: 06/09/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- GetReportServerUrls method
ms.assetid: 4865e32c-0114-465a-be8c-be223a7bc09e
caps.latest.revision: 12
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: a4b7067d9e6360902bf76b1bfe27c7ed6541f481
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---
# <a name="msreportserverinstance-methods---getreportserverurls"></a>Métodos de MSReportServer_Instance - GetReportServerUrls
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
  
## <a name="remarks"></a>Comentarios  
 Se llama a los métodos expuestos por objetos de administración de WMI mediante la función InvokeMethod. Para obtener más información, vea "Ejecutar métodos en objetos de administración" en la la documentación de WMI de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework.  
  
## <a name="requirements"></a>Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspc](../../includes/ssrswminmspc-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Miembros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  

