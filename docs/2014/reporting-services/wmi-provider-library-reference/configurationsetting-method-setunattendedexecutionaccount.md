---
title: Método SetUnattendedExecutionAccount ( MSeportServer_ConfigurationSetting de WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
api_name:
- SetUnattendedExecutionAccount (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- SetUnattendedExecutionAccount method
ms.assetid: 1ba6be6f-b05c-4ea0-af98-cd0780290b70
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 095929c60d586fa0ed6c857412a369171acdaa10
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66097931"
---
# <a name="setunattendedexecutionaccount-method-wmi-msreportserver_configurationsetting"></a>Método SetUnattendedExecutionAccount (WMI MSReportServer_ConfigurationSetting)
  Especifica la cuenta utilizada para ejecutar informes de forma desatendida.  
  
## <a name="syntax"></a>Sintaxis  
  
```vb  
Public Sub SetUnattendedExecutionAccount(UserName as String, _  
    Password as String, ByRef HRESULT as Int32)  
```  
  
```csharp  
public void SetUnattendedExecutionAccount (string UserName,   
    string Password, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parámetros  
 *Nombre*  
 Una cuenta de Windows que se utilizará para las ejecuciones desatendidas.  
  
 *Contraseña*  
 La contraseña de la cuenta especificada.  
  
 *VALOR*  
 [out] Valor que indica si la llamada se realizó correctamente o no.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve *HRESULT* que indica si la llamada al método se realizó correctamente o no. Un valor de 0 indica que la llamada al método se realizó correctamente. Un valor distinto de cero indica que se ha producido un error.  
  
## <a name="remarks"></a>Observaciones  
 El método SetUnattendedExecutionAccount no comprueba si el servidor de informes puede iniciar sesión como el usuario especificado.  
  
 No se puede usar el método SetUnattendedExecutionAccount para las ejecuciones desatendidas en el contexto del servicio Servidor de informes de Windows.  
  
## <a name="requirements"></a>Requisitos  
 **Espacio de nombres:**[!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Consulte también  
 [Miembros MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
