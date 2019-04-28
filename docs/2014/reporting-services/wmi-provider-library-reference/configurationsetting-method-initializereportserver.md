---
title: Método InitializeReportServer (MSReportServer_ConfigurationSetting de WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
api_name:
- InitializeReportServer (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- InitializeReportServer method
ms.assetid: 0304acc2-1fd7-437b-94d9-1c1073dd3ca4
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b4e01f1a0e6ab49939e3c8ad8339402a7d2b8431
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62647108"
---
# <a name="initializereportserver-method-wmi-msreportserverconfigurationsetting"></a>Método InitializeReportServer (WMI MSReportServer_ConfigurationSetting)
  Inicializa la instancia del servicio de informes especificada.  
  
## <a name="syntax"></a>Sintaxis  
  
```vb  
Public Sub InitializeReportServer(ByVal InstallationID As String, _  
    ByRef HRESULT As Int32, ByRef ExtendedErrors() As String)  
```  
  
```csharp  
public void InitializeReportServer(string InstallationID,   
    out Int32 HRESULT, out string[] ExtendedErrors);  
```  
  
## <a name="parameters"></a>Parámetros  
 *InstallationID*  
 Cadena utilizada para cifrar la clave de cifrado antes de devolverse.  
  
 *HRESULT*  
 [out] Valor que indica si la llamada se realizó correctamente o no.  
  
 *ExtendedErrors[]*  
 [out] Matriz de cadenas que contiene los errores adicionales devueltos por la llamada.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve *HRESULT* que indica si la llamada al método se realizó correctamente o no. Un valor de 0 indica que la llamada al método se realizó correctamente. Un valor distinto de cero indica que se ha producido un error.  
  
## <a name="remarks"></a>Comentarios  
 Cuando se llama a este método, la clave de cifrado que tiene acceso a la información segura de la base de datos del servidor de informes se cifra utilizando la clave pública del servidor de informes identificada por *InstallationID*.  
  
 La clave pública del servidor de informes especificado se debe haber escrito previamente en la base de datos del servidor de informes.  
  
 Se debe llamar al método *InitializeReportServer* en un servidor de informes que ya tenga acceso a la información segura para que pueda descifrar la clave de cifrado. A continuación, la clave de cifrado cifrada resultante se almacena en la base de datos del servidor de informes.  
  
 Si el servidor de informes [IsInitialized](configurationsetting-property-isinitialized.md) propiedad está establecida en `true` cuando se llama al método InitializeReportServer, el método devuelve valores correctos sin intentar cifrar la clave de cifrado.  
  
## <a name="requirements"></a>Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Miembros MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
