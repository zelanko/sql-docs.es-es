---
title: "M&#233;todo ListReportServersInDatabase (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs"
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
  - "ListReportServersInDatabase (WMI MSReportServer_ConfigurationSetting Class)"
apilocation: 
  - "reportingservices.mof"
apitype: "MOFDef"
helpviewer_keywords: 
  - "método ListReportServersInDatabase"
ms.assetid: a4bf5968-c46f-484f-a510-65e2dde65a0d
caps.latest.revision: 18
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# M&#233;todo ListReportServersInDatabase (WMI MSReportServer_ConfigurationSetting)
  Devuelve una lista de las instalaciones del servidor de informes que se encuentran en la base de datos del servidor de informes, sin tener en cuenta si esas instalaciones tienen acceso a la información segura.  
  
## Sintaxis  
  
```vb  
Public Sub ListReportServersInDatabase(ByRef MachineNames() As String, _  
    ByRef InstanceNames() As String, ByRef InstallationIDs() As String, _  
    ByRef IsInitialized() As Boolean, ByRef Length As Int32, _  
    ByRef HRESULT As Int32, ByRef ExtendedErrors() As String)  
```  
  
```csharp  
public void ListReportServersInDatabase (out string[] MachineNames,   
    out string[] InstanceNames, out string[] InstallationIDs,   
    out Boolean[] IsInitialized,out Int32 Length, out Int32 HRESULT,    
    out string[] ExtendedErrors);  
```  
  
## Parámetros  
 *MachineNames[]*  
 [out] Matriz que contiene los nombres de equipo para las instalaciones del servidor de informes en la base de datos.  
  
 *InstanceNames[]*  
 [out] Matriz que contiene los nombres de instancia de cada una de las instalaciones del servidor de informes en la base de datos.  
  
 *InstallationIDs[]*  
 [out] Una matriz que contiene los Id. de instalación de cada instalación del servidor de informes en la base de datos.  
  
 *IsInitialized[]*  
 [out] Una matriz que contiene el estado de inicialización de cada instalación del servidor de informes en la base de datos.  
  
 *Longitud*  
 [out] La longitud de las matrices devueltas por el método. Todas las matrices devueltas tienen la misma longitud.  
  
 *HRESULT*  
 [out] Valor que indica si la llamada se realizó correctamente o no.  
  
 *ExtendedErrors[]*  
 [out] Matriz de cadenas que contiene los errores adicionales devueltos por la llamada.  
  
## Valor devuelto  
 Devuelve *HRESULT* que indica si la llamada al método se realizó correctamente o no. Un valor de 0 indica que la llamada al método se realizó correctamente. Un valor distinto de cero indica que se ha producido un error.  
  
## Comentarios  
 ListReportServersInDatabase enumera las instalaciones del servidor de informes que se encuentran en la base de datos del servidor de informes, sin tener en cuenta si tienen acceso a información segura, y devuelve un conjunto de matrices que contienen información sobre cada instalación.  
  
## Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## Vea también  
 [Miembros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  