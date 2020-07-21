---
title: Método GetReportServerUrls (MSReportServer_Instance de WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- GetReportServerUrls method
ms.assetid: 4865e32c-0114-465a-be8c-be223a7bc09e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f600d7bf2515cb77c587e5c9c3d5f8d1db1e343f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66097188"
---
# <a name="getreportserverurls-method-wmi-msreportserver_instance"></a>Método GetReportServerUrls (WMI MSReportServer_Instance)
  Devuelve una lista de direcciones URL que los usuarios pueden utilizar para tener acceso al servidor de informes y al administrador de informes.  
  
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
 Una matriz que contiene las aplicaciones instaladas. Los valores son `ReportServerWebService` o `ReportManager`.  
  
 *URLs[]*  
 Una matriz que contiene las direcciones URL correctamente registradas.  
  
 *Longitud*  
 Un valor entero que contiene la longitud de las matrices devueltas.  
  
 *HRESULT*  
 Un valor que indica éxito o un código de error.  
  
## <a name="return-values"></a>Valores devueltos  
  
## <a name="remarks"></a>Observaciones  
 Se llama a los métodos expuestos por objetos de administración de WMI mediante la función InvokeMethod. Para obtener más información, vea "Ejecutar métodos en objetos de administración" en la la documentación de WMI de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework.  
  
## <a name="requirements"></a>Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspc](../../includes/ssrswminmspc-md.md)]  
  
## <a name="see-also"></a>Consulte también  
 [Miembros MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
