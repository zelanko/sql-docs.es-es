---
title: "Método RemoveURL (MSReportServer_ConfigurationSetting de WMI) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: RemoveURL method
ms.assetid: 3d98bd97-e152-48ce-ab1c-bd2c4f8b7fe9
caps.latest.revision: "13"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 6b96a9374f5f25d07c7ba513ae63615b06fc83ba
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="configurationsetting-method---removeurl"></a>Método ConfigurationSetting - RemoveURL
  Quita una dirección URL reservada para el servidor de informes. Si es necesario quitar varias direcciones URL, esta operación debe realizarse una a una llamando a esta API.  
  
## <a name="syntax"></a>Sintaxis  
  
```vb  
Public Sub RemoveURL(ByVal Application As String, _  
    ByVal UrlString As String, ByVal Lcid As Int32, _  
    ByRef [Error] As String, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void RemoveURL(string Application, string UrlString, int Lcid,   
    out string Error, out int HRESULT);  
```  
  
## <a name="parameters"></a>Parámetros  
 *Aplicación*  
 Nombre de la aplicación para la que se quita la reserva.  
  
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
  
## <a name="remarks"></a>Comentarios  
 *UrlString* no incluye el nombre del directorio virtual: el [Método SetVirtualDirectory &#40;MSReportServer_ConfigurationSetting de WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setvirtualdirectory.md) se proporciona para ese propósito.  
  
 Antes de llamar al método [ReserveURL](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-reserveurl.md) , debe proporcionar un valor para la propiedad de configuración VirtualDirectory en el parámetro *Application* . Use el [Método SetVirtualDirectory &#40;MSReportServer_ConfigurationSetting de WMI&#41;](../../reporting-services/wmi-provider-library-reference/configurationsetting-method-setvirtualdirectory.md) para establecer la propiedad VirtualDirectory.  
  
 Si [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ha proporcionado un certificado SSL y ninguna otra dirección URL lo necesita, se quita.  
  
 Este método hace que todos los dominios de aplicación sin configuración sean objeto de reciclaje con reinicio de dominios de aplicación y se detengan durante esta operación; los dominios de aplicación se reinician una vez completada la operación.  
  
## <a name="requirements"></a>Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Miembros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
