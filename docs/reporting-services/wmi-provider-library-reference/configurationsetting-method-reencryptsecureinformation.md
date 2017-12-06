---
title: "Método ReencryptSecureInformation (MSReportServer_ConfigurationSetting de WMI) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.service: 
ms.component: wmi-provider-library-reference
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
apiname: ReencryptSecureInformation (WMI MSReportServer_ConfigurationSetting Class)
apilocation: reportingservices.mof
apitype: MOFDef
helpviewer_keywords: ReencryptSecureInformation method
ms.assetid: 8a487497-c207-45b2-8c92-87c58cc68716
caps.latest.revision: "18"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 2023843b8bafc6c6fe0cd73e4510001dab4a52db
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="configurationsetting-method---reencryptsecureinformation"></a>Método ConfigurationSetting - ReencryptSecureInformation
  Genera una nueva clave de cifrado y vuelve a cifrar toda la información segura en el catálogo utilizando esta nueva clave.  
  
## <a name="syntax"></a>Sintaxis  
  
```vb  
Public Sub ReencryptSecureInformation(ByRef HRESULT as Int32, ByRef ExtendedErrors() As String)  
```  
  
```csharp  
public void ReencryptSecureInformation (out Int32 HRESULT, out string[] ExtendedErrors);  
```  
  
## <a name="parameters"></a>Parámetros  
 *HRESULT*  
 [out] Valor que indica si la llamada se realizó correctamente o no.  
  
 *ExtendedErrors[]*  
 [out] Matriz de cadenas que contiene los errores adicionales devueltos por la llamada.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve *HRESULT* que indica si la llamada al método se realizó correctamente o no. Un valor de 0 indica que la llamada al método se realizó correctamente. Un valor distinto de cero indica que se ha producido un error.  
  
## <a name="remarks"></a>Comentarios  
 El método ReencryptSecureInformation permite que el administrador reemplace la clave de cifrado existente por una nueva clave.  
  
 Cuando se invoca este método, el servidor de informes genera una nueva clave de cifrado y la utiliza en todo el contenido cifrado para volver a cifrarlo.  
  
 Las extensiones de entrega pueden almacenar la información segura en sus estructuras de configuración de entrega. Cuando se llama a ReencryptSecureInformation, el servidor de informes carga cada suscripción y la extensión de entrega correspondiente para volver a cifrar la información almacenada en la configuración asociada.  
  
 Si este método se ejecuta en un equipo en una implementación escalada, cada equipo en la implementación escalada deberá inicializarse de nuevo.  
  
## <a name="requirements"></a>Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Miembros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
