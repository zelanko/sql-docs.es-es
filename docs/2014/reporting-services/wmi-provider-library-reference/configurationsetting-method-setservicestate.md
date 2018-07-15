---
title: Método SetServiceState (MSReportServer_ConfigurationSetting de WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
api_name:
- SetServiceState (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- SetServiceState method
ms.assetid: 9e1ee42d-b388-4929-89c7-8741b956c3be
caps.latest.revision: 17
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: f154e0eb7666fd4c8534e701f42a521b4fb70ff8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37222535"
---
# <a name="setservicestate-method-wmi-msreportserverconfigurationsetting"></a>Método SetServiceState (WMI MSReportServer_ConfigurationSetting)
  Activa y desactiva los servicios web y los servicios del Servidor de informes de Windows.  
  
## <a name="syntax"></a>Sintaxis  
  
```vb  
Public Sub SetServiceState(ByVal EnableWindowsService As Boolean, _  
    ByVal EnableWebService As Boolean, ByVal EnableReportManager As Boolean, _  
    ByRef HRESULT As Int32)  
```  
  
```csharp  
public void SetSecureConnectionLevel(Boolean EnableWindowsService,  
    Boolean EnableWebService, Boolean EnableReportManager, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parámetros  
 *EnableWindowsService*  
 Un `Boolean` valor que indica el estado del servicio de Windows. Un valor de `true` inicia el Windows del servidor de informes de servicio; un valor de `false` detiene el servicio de Windows.  
  
 *EnableWebService*  
 Un `Boolean` valor que indica el estado de la [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] servicio Web. Un valor de `true` inicia el servicio web del servidor de informes; un valor de `false` detiene el servicio web.  
  
 *EnableReportManager*  
 Un `Boolean` valor que indica el estado deseado del Administrador de informes.  
  
 *HRESULT*  
 [out] Valor que indica si la llamada se realizó correctamente o no.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve *HRESULT* que indica si la llamada al método se realizó correctamente o no. Un valor de 0 indica que la llamada al método se realizó correctamente. Un valor distinto de cero indica que se ha producido un error.  
  
## <a name="remarks"></a>Notas  
  
## <a name="requirements"></a>Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Miembros MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
