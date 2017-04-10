---
title: "M&#233;todo GenerateDatabaseCreationScript (MSReportServer_ConfigurationSetting de WMI) | Microsoft Docs"
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
apiname: 
  - "GenerateDatabaseCreationScript (WMI MSReportServer_ConfigurationSetting Class)"
apilocation: 
  - "reportingservices.mof"
apitype: "MOFDef"
helpviewer_keywords: 
  - "GenerateDatabaseCreationScript, método"
ms.assetid: 25232dc7-00fe-4cd1-8a1c-7e36d552de00
caps.latest.revision: 25
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
---
# M&#233;todo GenerateDatabaseCreationScript (MSReportServer_ConfigurationSetting de WMI)
  Genera un script SQL que se puede utilizar para crear una base de datos del servidor de informes.  
  
## Sintaxis  
  
```vb  
Public Sub GenerateDatabaseCreationScript(ByVal DatabaseName As String, _  
    ByVal Lcid As Int32, ByVal IsSharePointMode As Boolean, ByRef Script As String, _  
    ByRef HRESULT As Int32)  
```  
  
```csharp  
public void GenerateDatabaseCreationScript(string DatabaseName, Int32 Lcid,   
    Boolean IsSharePointMode, out string Script, out Int32 HRESULT);  
```  
  
## Parámetros  
 *Databasename*  
 Cadena que contiene el nombre de la base de datos del servidor de informes que se va a crear.  
  
 *Lcid*  
 Valor usado para la localización de nombres de roles.  
  
 *IsSharePointMode*  
 Indica si se desea crear la base de datos en modo nativo o en modo de SharePoint.  
  
> [!IMPORTANT]  
>  A partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], *IsSharePointMode*=**True** no se admite, porque en modo de SharePoint [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] es un servicio compartido de SharePoint que el proveedor WMI no controla. Este parámetro siempre debe establecerse en **False**.  
  
 *Script*  
 [out] Cadena que contiene el script SQL generado.  
  
 *HRESULT*  
 [out] Valor que indica si la llamada se realizó correctamente o no.  
  
## Valor devuelto  
 Devuelve *HRESULT* que indica si la llamada al método se realizó correctamente o no. Un valor de 0 indica que la llamada al método se realizó correctamente. Un valor distinto de cero indica que se ha producido un error.  
  
## Comentarios  
 Este método genera un script SQL que crea bases de datos del servidor de informes para la versión del servidor de informes al que se está conectado actualmente.  
  
 El valor proporcionado en el parámetro *DatabaseName* debe cumplir las convenciones de nomenclatura de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 El método no comprueba la existencia de la base de datos al generar el script.  
  
 Este método no comprueba la existencia de la base de datos del servidor de informes al generar el script.  
  
 El script generado admite [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 y [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
## Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## Vea también  
 [Miembros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  