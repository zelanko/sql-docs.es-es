---
title: "M&#233;todo ListReservedURLs (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs"
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
  - "método ListReservedURLs"
ms.assetid: 32335af1-5eae-4420-a0ef-b1e8a3267166
caps.latest.revision: 11
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# M&#233;todo ListReservedURLs (WMI MSReportServer_ConfigurationSetting)
  Enumera las direcciones URL reservadas para todas las aplicaciones en el servidor de informes.  
  
## Sintaxis  
  
```vb  
Public Sub ListReservedUrls(ByRef Application() as String, ByRef UrlString() as String, _  
    ByRef Account() as String, ByRef AccountSID() as String, _  
    ByRef length() as Int32, ByRef HRESULT as Int32)  
```  
  
```csharp  
public void ListReservedUrls(out string[] Application, out string[] UrlString,  
        out string[] Account, out string[] AccountSID,  
        out int[] Length, out int[] HRESULT);  
```  
  
## Parámetros  
 *Application[]*  
 [out] Aplicaciones que tienen reservas de direcciones URL.  
  
 *UrlString[]*  
 [out] Direcciones URL reservadas.  
  
 *Account[]*  
 [out] Nombres de cuenta asociados a la cuenta para las reservas de direcciones URL.  
  
 *AccountSID[]*  
 [out] Los SID de cuenta asociados con la cuenta para las reservas URL.  
  
 *Longitud*  
 [out] La longitud de las matrices devueltas por el método.  
  
 *HRESULT*  
 [out] Valor que indica si la llamada se realizó correctamente o no.  
  
## Valor devuelto  
 Devuelve *HRESULT* que indica si la llamada al método se realizó correctamente o no. Un valor de 0 indica que la llamada al método se realizó correctamente; un código de error indica que la llamada no se realizó correctamente.  
  
## Comentarios  
  
## Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## Vea también  
 [Miembros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  