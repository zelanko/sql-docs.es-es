---
title: Método RemoveURL (MSReportServer_ConfigurationSetting de WMI) | Microsoft Docs
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
- RemoveURL method
ms.assetid: 3d98bd97-e152-48ce-ab1c-bd2c4f8b7fe9
caps.latest.revision: 13
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 464a37912e7751b4fa33b5a134b29e456a6ae573
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37258291"
---
# <a name="removeurl-method-wmi-msreportserverconfigurationsetting"></a>Método RemoveURL (MSReportServer_ConfigurationSetting de WMI)
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
  
## <a name="remarks"></a>Notas  
 *UrlString* no incluye el nombre del directorio virtual: el [Método SetVirtualDirectory &#40;MSReportServer_ConfigurationSetting de WMI&#41;](configurationsetting-method-setvirtualdirectory.md) se proporciona para ese propósito.  
  
 Antes de llamar a la [ReserveURL](configurationsetting-method-reserveurl.md) método, debe proporcionar un valor para la propiedad de configuración VirtualDirectory el *aplicación* parámetro. Use el [Método SetVirtualDirectory &#40;MSReportServer_ConfigurationSetting de WMI&#41;](configurationsetting-method-setvirtualdirectory.md) para establecer la propiedad VirtualDirectory.  
  
 Si [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ha proporcionado un certificado SSL y ninguna otra dirección URL lo necesita, se quita.  
  
 Este método hace que todos los dominios de aplicación sin configuración sean objeto de reciclaje con reinicio de dominios de aplicación y se detengan durante esta operación; los dominios de aplicación se reinician una vez completada la operación.  
  
## <a name="requirements"></a>Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Miembros MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
