---
title: "M&#233;todo GetReportServerUrls (WMI MSReportServer_Instance) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "método GetReportServerUrls"
ms.assetid: 4865e32c-0114-465a-be8c-be223a7bc09e
caps.latest.revision: 12
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# M&#233;todo GetReportServerUrls (WMI MSReportServer_Instance)
  Devuelve una lista de direcciones URL que los usuarios pueden usar para tener acceso al servidor de informes y al [!INCLUDE[ssRSWebPortal](../../includes/ssrswebportal.md)].  
  
## Sintaxis  
  
```vb  
Public Sub GetReportServerUrls (ByRef ApplicationName() As String, ByRef URLs()_  
    As String, ByRef Length As Int32, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void GetReportServerUrls(out string[] applicationName,   
    out string[] URLs, out int length, out int HRESULT);  
```  
  
## Parámetros  
 *ApplicationName[]*  
 Una matriz que contiene las aplicaciones instaladas. Los valores son **ReportServerWebService** o **ReportServerWebApp**.  
  
 *URLs[]*  
 Una matriz que contiene las direcciones URL correctamente registradas.  
  
 *Longitud*  
 Un valor entero que contiene la longitud de las matrices devueltas.  
  
 *HRESULT*  
 Un valor que indica éxito o un código de error.  
  
## Valores devueltos  
  
## Comentarios  
 Se llama a los métodos expuestos por objetos de administración de WMI mediante la función InvokeMethod. Para obtener más información, vea "Ejecutar métodos en objetos de administración" en la la documentación de WMI de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework.  
  
## Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspc](../../includes/ssrswminmspc-md.md)]  
  
## Vea también  
 [Miembros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  