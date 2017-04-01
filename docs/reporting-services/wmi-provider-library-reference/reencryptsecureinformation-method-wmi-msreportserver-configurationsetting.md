---
title: "M&#233;todo ReencryptSecureInformation (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs"
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
  - "ReencryptSecureInformation (WMI MSReportServer_ConfigurationSetting Class)"
apilocation: 
  - "reportingservices.mof"
apitype: "MOFDef"
helpviewer_keywords: 
  - "método ReencryptSecureInformation"
ms.assetid: 8a487497-c207-45b2-8c92-87c58cc68716
caps.latest.revision: 18
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# M&#233;todo ReencryptSecureInformation (WMI MSReportServer_ConfigurationSetting)
  Genera una nueva clave de cifrado y vuelve a cifrar toda la información segura en el catálogo utilizando esta nueva clave.  
  
## Sintaxis  
  
```vb  
Public Sub ReencryptSecureInformation(ByRef HRESULT as Int32, ByRef ExtendedErrors() As String)  
```  
  
```csharp  
public void ReencryptSecureInformation (out Int32 HRESULT, out string[] ExtendedErrors);  
```  
  
## Parámetros  
 *HRESULT*  
 [out] Valor que indica si la llamada se realizó correctamente o no.  
  
 *ExtendedErrors[]*  
 [out] Matriz de cadenas que contiene los errores adicionales devueltos por la llamada.  
  
## Valor devuelto  
 Devuelve *HRESULT* que indica si la llamada al método se realizó correctamente o no. Un valor de 0 indica que la llamada al método se realizó correctamente. Un valor distinto de cero indica que se ha producido un error.  
  
## Comentarios  
 El método ReencryptSecureInformation permite que el administrador reemplace la clave de cifrado existente por una nueva clave.  
  
 Cuando se invoca este método, el servidor de informes genera una nueva clave de cifrado y la utiliza en todo el contenido cifrado para volver a cifrarlo.  
  
 Las extensiones de entrega pueden almacenar la información segura en sus estructuras de configuración de entrega. Cuando se llama a ReencryptSecureInformation, el servidor de informes carga cada suscripción y la extensión de entrega correspondiente para volver a cifrar la información almacenada en la configuración asociada.  
  
 Si este método se ejecuta en un equipo en una implementación escalada, cada equipo en la implementación escalada deberá inicializarse de nuevo.  
  
## Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## Vea también  
 [Miembros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  