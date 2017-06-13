---
title: "Método ListReservedURLs (WMI MSReportServer_ConfigurationSetting) | Documentos de Microsoft"
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
helpviewer_keywords:
- ListReservedURLs method
ms.assetid: 32335af1-5eae-4420-a0ef-b1e8a3267166
caps.latest.revision: 11
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: cf6f31340eaba5654e2c5fd125eefba07a39d8e5
ms.contentlocale: es-es
ms.lasthandoff: 06/13/2017

---
# <a name="configurationsetting-method---listreservedurls"></a>Método ConfigurationSetting - ListReservedURLs
  Enumera las direcciones URL reservadas para todas las aplicaciones en el servidor de informes.  
  
## <a name="syntax"></a>Sintaxis  
  
```vb  
Public Sub ListReservedUrls(ByRef Application() as String, ByRef UrlString() as String, _  
    ByRef Account() as String, ByRef AccountSID() as String, _  
    ByRef length() as Int32, ByRef HRESULT as Int32)  
```  
  
```csharp  
public void ListReservedUrls(out string[] Application, out string[] UrlString,  
        out string[] Account, out string[] AccountSID,  
        out int[] Length, out int[] HRESULT);  
```  
  
## <a name="parameters"></a>Parámetros  
 *Application[]*  
 [out] Aplicaciones que tienen reservas de direcciones URL.  
  
 *UrlString[]*  
 [out] Direcciones URL reservadas.  
  
 *Account[]*  
 [out] Nombres de cuenta asociados a la cuenta para las reservas de direcciones URL.  
  
 *AccountSID[]*  
 [out] Los SID de cuenta asociados con la cuenta para las reservas URL.  
  
 *Longitud*  
 [out] La longitud de las matrices devueltas por el método.  
  
 *HRESULT*  
 [out] Valor que indica si la llamada se realizó correctamente o no.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve *HRESULT* que indica si la llamada al método se realizó correctamente o no. Un valor de 0 indica que la llamada al método se realizó correctamente; un código de error indica que la llamada no se realizó correctamente.  
  
## <a name="remarks"></a>Comentarios  
  
## <a name="requirements"></a>Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Miembros MSReportServer_ConfigurationSetting](../../reporting-services/wmi-provider-library-reference/msreportserver-configurationsetting-members.md)  
  
  
