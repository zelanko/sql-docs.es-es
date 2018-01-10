---
title: "Método SetServiceState (MSReportServer_ConfigurationSetting de WMI) | Microsoft Docs"
ms.custom: 
ms.date: 03/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: wmi-provider-library-reference
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
apiname: SetServiceState (WMI MSReportServer_ConfigurationSetting Class)
apilocation: reportingservices.mof
apitype: MOFDef
helpviewer_keywords: SetServiceState method
ms.assetid: 9e1ee42d-b388-4929-89c7-8741b956c3be
caps.latest.revision: "20"
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8b43b5506c4b604c2270d06a3ca065f664a3bab8
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2018
---
# <a name="configurationsetting-method---setservicestate"></a>Método de ConfigurationSetting: SetServiceState
  Activa y desactiva los servicios web y los servicios del Servidor de informes de Windows.  
  
## <a name="syntax"></a>Sintaxis  
  
```vb  
Public Sub SetServiceState(ByVal EnableWindowsService As Boolean, _  
    ByVal EnableWebService As Boolean, ByVal EnableReportManager As Boolean, _  
    ByRef HRESULT As Int32)  
```  
  
```csharp  
public void SetServiceState(Boolean EnableWindowsService,  
    Boolean EnableWebService, Boolean EnableReportManager, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parámetros  
 *EnableWindowsService*  
 Valor **booleano** que indica el estado del servicio Windows. Un valor de **true** inicia el servicio Windows del servidor de informes; un valor de **false** detiene el servicio Windows.  
  
 *EnableWebService*  
 Valor **booleano** que indica el estado del servicio web de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Un valor de **true** inicia el servicio web del servidor de informes; un valor de **false** detiene el servicio web.  
  
 *EnableReportManager*  
 Valor **booleano** que indica el estado deseado del Administrador de informes.
 
 > [!NOTE] 
 > Esta opción está en desuso desde la actualización acumulativa 2 de SQL Server 2016 Reporting Services. El portal web siempre estará habilitado. El valor se omitirá.
  
 *HRESULT*  
 [out] Valor que indica si la llamada se realizó correctamente o no.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve *HRESULT* que indica si la llamada al método se realizó correctamente o no. Un valor de 0 indica que la llamada al método se realizó correctamente. Un valor distinto de cero indica que se ha producido un error.  
  
## <a name="remarks"></a>Notas  
  
## <a name="requirements"></a>Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Ver también  
 [Miembros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
