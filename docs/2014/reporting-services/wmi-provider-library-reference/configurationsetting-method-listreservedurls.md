---
title: Método ListReservedURLs (WMI MSReportServer_ConfigurationSetting) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ListReservedURLs method
ms.assetid: 32335af1-5eae-4420-a0ef-b1e8a3267166
caps.latest.revision: 11
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 8dac5ed639e3e06bbcf4ff11a5ea5b21cf03f24b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36109207"
---
# <a name="listreservedurls-method-wmi-msreportserverconfigurationsetting"></a>Método ListReservedURLs (WMI MSReportServer_ConfigurationSetting)
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
  
## <a name="remarks"></a>Notas  
  
## <a name="requirements"></a>Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Miembros MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  