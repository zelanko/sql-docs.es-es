---
title: "M&#233;todo RemoveURL (MSReportServer_ConfigurationSetting de WMI) | Microsoft Docs"
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
helpviewer_keywords: 
  - "RemoveURL, método"
ms.assetid: 3d98bd97-e152-48ce-ab1c-bd2c4f8b7fe9
caps.latest.revision: 13
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# M&#233;todo RemoveURL (MSReportServer_ConfigurationSetting de WMI)
  Quita una dirección URL reservada para el servidor de informes. Si es necesario quitar varias direcciones URL, esta operación debe realizarse una a una llamando a esta API.  
  
## Sintaxis  
  
```vb  
Public Sub RemoveURL(ByVal Application As String, _  
    ByVal UrlString As String, ByVal Lcid As Int32, _  
    ByRef [Error] As String, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void RemoveURL(string Application, string UrlString, int Lcid,   
    out string Error, out int HRESULT);  
```  
  
## Parámetros  
 *Aplicación*  
 Nombre de la aplicación para la que se quita la reserva.  
  
 *URLString*  
 Dirección URL para la reserva.  
  
 *lcid*  
 Configuración regional que se utilizará para los mensajes de error devueltos.  
  
 *Error*  
 [out] Descripción del error que se produjo.  
  
 *HRESULT*  
 [out] Valor que indica si la llamada se realizó correctamente o no.  
  
## Valor devuelto  
 Devuelve *HRESULT* que indica si la llamada al método se realizó correctamente o no. Un valor de 0 indica que la llamada al método se realizó correctamente; un código de error indica que la llamada no se realizó correctamente.  
  
## Comentarios  
 *UrlString* no incluye el nombre del directorio Virtual: el método [Método SetVirtualDirectory &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/setvirtualdirectory-method-wmi-msreportserver-configurationsetting.md) se proporciona para ese propósito.  
  
 Antes de llamar al método [ReserveURL](../../reporting-services/wmi-provider-library-reference/reserveurl-method-wmi-msreportserver-configurationsetting.md), debe proporcionar un valor para la propiedad de configuración VirtualDirectory en el parámetro *Application*. Use el método [Método SetVirtualDirectory &#40;WMI MSReportServer_ConfigurationSetting&#41;](../../reporting-services/wmi-provider-library-reference/setvirtualdirectory-method-wmi-msreportserver-configurationsetting.md) para establecer la propiedad VirtualDirectory.  
  
 Si [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ha proporcionado un certificado SSL y ninguna otra dirección URL lo necesita, se quita.  
  
 Este método hace que todos los dominios de aplicación sin configuración sean objeto de reciclaje con reinicio de dominios de aplicación y se detengan durante esta operación; los dominios de aplicación se reinician una vez completada la operación.  
  
## Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## Vea también  
 [Miembros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  