---
title: "Método CreateSSLCertificateBinding (MSReportServer_ConfigurationSetting de WMI) | Microsoft Docs"
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
helpviewer_keywords: CreateSSLCertificateBinding
ms.assetid: 407d50e4-0a55-43cb-8ddf-2d82714071b1
caps.latest.revision: "14"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 68df063c02108366df07867d51cac029218e16c4
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="configurationsetting-method---createsslcertificatebinding"></a>Método de ConfigurationSetting: CreateSSLCertificateBinding
  Crea un enlace de certificado SSL.  
  
## <a name="syntax"></a>Sintaxis  
  
```vb  
Public Sub CreateSSLCertificateBinding(ByVal Application As String, _  
    ByVal CertificateHash As String, ByVal IPAddress As String, _  
    ByVal Port As Int32, ByVal lcid As Int32, _  
    ByRef [Error] As String, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void CreateSSLCertificateBinding(string application,   
    string certificateHash, string IPAddress, int Port,   
    int lcid, out string error, out int HRESULT);  
```  
  
## <a name="parameters"></a>Parámetros  
 *Aplicación*  
 Nombre de la aplicación para la que se debe crear el enlace de certificado.  
  
 *CertificateHash*  
 Valor hash del certificado.  
  
 *IPAddress*  
 Dirección IP para la aplicación.  
  
 *Puerto*  
 Puerto SSL asociado al enlace.  
  
 *Lcid*  
 Configuración regional que se utilizará para los mensajes de error devueltos.  
  
 *Error*  
 [out] Descripción de los errores que se produjeron.  
  
 *HRESULT*  
 [out] Valor que indica si la llamada se realizó correctamente o no.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve *HRESULT* que indica si la llamada al método se realizó correctamente o no. Un valor de 0 indica que la llamada al método se realizó correctamente; un código de error indica que la llamada no se realizó correctamente.  
  
## <a name="remarks"></a>Comentarios  
 Este método agrega un enlace a rsreportserver.config para la aplicación. Si no existe todavía un enlace en HTTP.SYS, se crea ahí.  
  
 Antes de crear el enlace, la llamada al método examina las reservas de direcciones URL para la aplicación especificada con el fin de determinar si el enlace de certificado SSL es válido.  
  
 Las condiciones siguientes se validan y pueden dar lugar a errores:  
  
1.  El certificado no existe.  
  
2.  La dirección IP especificada no corresponde a una dirección IP de este equipo.  
  
3.  La dirección IP especificada es una dirección IP para DHCP (cambia periódicamente): en su lugar, use la dirección IP con un carácter comodín (0.0.0.0).  
  
4.  La dirección IP especificada no coincide con la dirección IP de una reserva de dirección URL y no existe una reserva de dirección URL de nombre de host o con un carácter comodín.  
  
5.  Existe una reserva de dirección URL que especifica un nombre de host, pero el nombre de host no coincide con el nombre de host del certificado.  
  
## <a name="requirements"></a>Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Miembros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
