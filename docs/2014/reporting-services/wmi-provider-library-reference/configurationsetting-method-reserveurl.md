---
title: Método ReserveURL (MSReportServer_ConfigurationSetting de WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ReservedURL method
ms.assetid: b9008a62-3edd-4f8a-99f2-7598c2133899
caps.latest.revision: 14
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: f3f7ee5edc3c9deb73e19f97421c7a0da7206082
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37166076"
---
# <a name="reserveurl-method-wmi-msreportserverconfigurationsetting"></a>Método ReserveURL (MSReportServer_ConfigurationSetting de WMI)
  Agrega una reserva URL para una aplicación determinada.  
  
## <a name="syntax"></a>Sintaxis  
  
```vb  
Public Sub ReserveURL(Application as String, _  
    UrlString as String, Lcid as Int32, _   
    ByRef [Error] as String, ByRef HRESULT as Int32)  
```  
  
```csharp  
public void ReserveURL(string Application, string UrlString, int Lcid,   
    out string error, out int HRESULT);  
```  
  
## <a name="parameters"></a>Parámetros  
 *Aplicación*  
 Nombre de la aplicación para la que se va a reservar la dirección URL.  
  
 *URLString*  
 Dirección URL para la reserva.  
  
 *lcid*  
 Configuración regional que se utilizará para los mensajes de error devueltos.  
  
 *Error*  
 [out] Descripción del error que se produjo.  
  
 *HRESULT*  
 [out] Valor que indica si la llamada se realizó correctamente o no.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve *HRESULT* que indica si la llamada al método se realizó correctamente o no. Un valor de 0 indica que la llamada al método se realizó correctamente; un código de error indica que la llamada no se realizó correctamente.  
  
## <a name="remarks"></a>Notas  
 *UrlString* no incluye el nombre del directorio virtual. El [SetVirtualDirectory](configurationsetting-method-setvirtualdirectory.md) método se proporciona para ese propósito.  
  
 Las reservas de dirección URL se crean para la cuenta de servicio de Windows actual. El cambio de la cuenta de servicio de Windows requiere la actualización manual de todas las reservas de dirección URL.  
  
 Este método produce el reciclaje con reinicio de dominios de aplicación de todos los dominios de aplicación. Los dominios de aplicación se reinician una vez completada esta operación.  
  
## <a name="requirements"></a>Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Miembros MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
