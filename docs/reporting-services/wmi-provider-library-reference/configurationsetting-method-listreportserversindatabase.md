---
title: Método ListReportServersInDatabase (MSReportServer_ConfigurationSetting de WMI) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: ''
ms.component: wmi-provider-library-reference
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- ListReportServersInDatabase (WMI MSReportServer_ConfigurationSetting Class)
apilocation:
- reportingservices.mof
apitype: MOFDef
helpviewer_keywords:
- ListReportServersInDatabase method
ms.assetid: a4bf5968-c46f-484f-a510-65e2dde65a0d
caps.latest.revision: 18
author: markingmyname
ms.author: maghan
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c3e8899e2a3fbb77f218a9b3d2108829d3544a2d
ms.sourcegitcommit: 7e117bca721d008ab106bbfede72f649d3634993
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/09/2018
---
# <a name="configurationsetting-method---listreportserversindatabase"></a>Método de ConfigurationSetting: ListReportServersInDatabase
  Devuelve una lista de las instalaciones del servidor de informes que se encuentran en la base de datos del servidor de informes, sin tener en cuenta si esas instalaciones tienen acceso a la información segura.  
  
## <a name="syntax"></a>Sintaxis  
  
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
  
## <a name="parameters"></a>Parámetros  
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
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve *HRESULT* que indica si la llamada al método se realizó correctamente o no. Un valor de 0 indica que la llamada al método se realizó correctamente. Un valor distinto de cero indica que se ha producido un error.  
  
## <a name="remarks"></a>Notas  
 ListReportServersInDatabase enumera las instalaciones del servidor de informes que se encuentran en la base de datos del servidor de informes, sin tener en cuenta si tienen acceso a información segura, y devuelve un conjunto de matrices que contienen información sobre cada instalación.  
  
## <a name="requirements"></a>Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Ver también  
 [Miembros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
