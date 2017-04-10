---
title: "M&#233;todo InitializeReportServer (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs"
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
  - "InitializeReportServer (WMI MSReportServer_ConfigurationSetting Class)"
apilocation: 
  - "reportingservices.mof"
apitype: "MOFDef"
helpviewer_keywords: 
  - "método InitializeReportServer"
ms.assetid: 0304acc2-1fd7-437b-94d9-1c1073dd3ca4
caps.latest.revision: 21
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# M&#233;todo InitializeReportServer (WMI MSReportServer_ConfigurationSetting)
  Inicializa la instancia del servicio de informes especificada.  
  
## Sintaxis  
  
```vb  
Public Sub InitializeReportServer(ByVal InstallationID As String, _  
    ByRef HRESULT As Int32, ByRef ExtendedErrors() As String)  
```  
  
```csharp  
public void InitializeReportServer(string InstallationID,   
    out Int32 HRESULT, out string[] ExtendedErrors);  
```  
  
## Parámetros  
 *InstallationID*  
 Cadena utilizada para cifrar la clave de cifrado antes de devolverse.  
  
 *HRESULT*  
 [out] Valor que indica si la llamada se realizó correctamente o no.  
  
 *ExtendedErrors[]*  
 [out] Matriz de cadenas que contiene los errores adicionales devueltos por la llamada.  
  
## Valor devuelto  
 Devuelve *HRESULT* que indica si la llamada al método se realizó correctamente o no. Un valor de 0 indica que la llamada al método se realizó correctamente. Un valor distinto de cero indica que se ha producido un error.  
  
## Comentarios  
 Cuando se llama a este método, la clave de cifrado que tiene acceso a la información segura de la base de datos del servidor de informes se cifra utilizando la clave pública del servidor de informes identificada por *InstallationID*.  
  
 La clave pública del servidor de informes especificado se debe haber escrito previamente en la base de datos del servidor de informes.  
  
 Se debe llamar al método *InitializeReportServer* en un servidor de informes que ya tenga acceso a la información segura para que pueda descifrar la clave de cifrado. A continuación, la clave de cifrado cifrada resultante se almacena en la base de datos del servidor de informes.  
  
 Si la propiedad [IsInitialized](../../reporting-services/wmi-provider-library-reference/isinitialized-property-wmi-msreportserver-configurationsetting.md) del servidor de informes está establecida en **true** cuando se llama al método InitializeReportServer, este último devuelve valores correctos sin intentar cifrar la clave de cifrado.  
  
## Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## Vea también  
 [Miembros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  