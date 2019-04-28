---
title: Método ListInstalledSharePointVersions (WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- ListInstalledSharePointVersions method
ms.assetid: 8f0a5e9f-23f1-41e5-9a90-dfec19ef1df7
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e94582de5f086339cb8dc08892904fd054a5c18a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62647234"
---
# <a name="listinstalledsharepointversions-method-wmi"></a>Método ListInstalledSharePointVersions (WMI)
  Devuelve un conjunto de tokens que representan las versiones de Microsoft [!INCLUDE[winSPServ](../../includes/winspserv-md.md)], [!INCLUDE[offSPServ](../../includes/offspserv-md.md)], [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]o [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] que se instalan en el mismo equipo que el servidor de informes.  
  
## <a name="syntax"></a>Sintaxis  
  
```vb  
Public Sub ListInstalledSharePointVersions(ByRef VersionTokens() _  
    As String, ByRef Length As Int32, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void ListReportServersInDatabase (out string[] VersionTokens,   
    out Int32 Length, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parámetros  
 *VersionTokens[]*  
 [out] Una matriz que contiene los tokens que representan la versión de un producto o tecnología de SharePoint que es compatible con el servidor de informes instalado.  
  
 *Longitud*  
 [out] La longitud de la matriz de tokens de versión.  
  
 *HRESULT*  
 [out] Valor que indica si la llamada se realizó correctamente o no.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve *HRESULT* que indica si la llamada al método se realizó correctamente o no. Un valor de 0 indica que la llamada al método se realizó correctamente. Un valor distinto de cero indica que se ha producido un error.  
  
## <a name="remarks"></a>Comentarios  
 Cada token que se devuelve representa una versión de [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] o [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] que es compatible con el servidor de informes instalado actualmente. Si una versión determinada de SharePoint es compatible con versiones anteriores de SharePoint, se devuelven los tokens para cada versión de SharePoint compatible.  
  
 La tabla siguiente muestra los tokens de SharePoint que se devuelven.  
  
|**Tokens de versión**|**Descripción**|  
|------------------------|---------------------|  
|WSS_V2_Compatible|Se instala una instalación de [!INCLUDE[winSPServ](../../includes/winspserv-md.md)], [!INCLUDE[winSPServ](../../includes/winspserv-md.md)], [!INCLUDE[offSPServ](../../includes/offspserv-md.md)], [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]o [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] que es compatible con [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 2.0.|  
|WSS_V3_Compatible|Se instala una instalación de [!INCLUDE[winSPServ](../../includes/winspserv-md.md)], [!INCLUDE[winSPServ](../../includes/winspserv-md.md)], [!INCLUDE[offSPServ](../../includes/offspserv-md.md)], [!INCLUDE[SPF2010](../../includes/spf2010-md.md)]o [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] que es compatible con [!INCLUDE[winSPServ](../../includes/winspserv-md.md)] 3.0.|  
|WSS_V4_Compatible|Se instala una instalación de [!INCLUDE[SPF2010](../../includes/spf2010-md.md)] o [!INCLUDE[SPS2010](../../includes/sps2010-md.md)] que es compatible con Office 14.|  
  
## <a name="requirements"></a>Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Miembros MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
