---
title: "M&#233;todo SetServiceState (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs"
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
apiname: 
  - "SetServiceState (WMI MSReportServer_ConfigurationSetting Class)"
apilocation: 
  - "reportingservices.mof"
apitype: "MOFDef"
helpviewer_keywords: 
  - "SetServiceState, método"
ms.assetid: 9e1ee42d-b388-4929-89c7-8741b956c3be
caps.latest.revision: 20
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# M&#233;todo SetServiceState (WMI MSReportServer_ConfigurationSetting)
  Activa y desactiva los servicios web y los servicios del Servidor de informes de Windows.  
  
## Sintaxis  
  
```vb  
Public Sub SetServiceState(ByVal EnableWindowsService As Boolean, _  
    ByVal EnableWebService As Boolean, ByVal EnableReportManager As Boolean, _  
    ByRef HRESULT As Int32)  
```  
  
```csharp  
public void SetSecureConnectionLevel(Boolean EnableWindowsService,  
    Boolean EnableWebService, Boolean EnableReportManager, out Int32 HRESULT);  
```  
  
## Parámetros  
 *EnableWindowsService*  
 Valor **booleano** que indica el estado del servicio Windows. Un valor de **true** inicia el servicio Windows del servidor de informes; un valor de **false** detiene el servicio Windows.  
  
 *EnableWebService*  
 Valor **booleano** que indica el estado del servicio web de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Un valor de **true** inicia el servicio web del servidor de informes; un valor de **false** detiene el servicio web.  
  
 *EnableReportManager*  
 Valor **booleano** que indica el estado deseado del Administrador de informes.  
  
 *HRESULT*  
 [out] Valor que indica si la llamada se realizó correctamente o no.  
  
## Valor devuelto  
 Devuelve *HRESULT* que indica si la llamada al método se realizó correctamente o no. Un valor de 0 indica que la llamada al método se realizó correctamente. Un valor distinto de cero indica que se ha producido un error.  
  
## Comentarios  
  
## Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## Vea también  
 [Miembros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  