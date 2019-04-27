---
title: Método SetVirtualDirectory (MSReportServer_ConfigurationSetting de WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- SetVirtualDirectory method
ms.assetid: 1a25cb1d-38d5-401a-970b-87b642a780e4
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 5be09f364a0cfcf881cdbedd1db8f1f099819d0d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62646381"
---
# <a name="setvirtualdirectory-method-wmi-msreportserverconfigurationsetting"></a>Método SetVirtualDirectory (WMI MSReportServer_ConfigurationSetting)
  Establece el nombre del directorio virtual para una aplicación dada.  
  
## <a name="syntax"></a>Sintaxis  
  
```vb  
Public Sub SetVirtualDirectory(ByVal Application As String, _  
    ByVal VirtualDirectory As String, ByVal lcid As Int32, _  
    ByRef [Error] As String, ByRef HRESULT As Int32)  
```  
  
```csharp  
public void SetVirtualDirectory(string Application, string VirtualDirectory,   
       int Lcid,out string Error, out int HRESULT);  
```  
  
## <a name="parameters"></a>Parámetros  
 *Aplicación*  
 Nombre de la aplicación para la que se establece el directorio virtual.  
  
 *VirtualDirectory*  
 Nombre del directorio virtual.  
  
 *lcid*  
 Identificador de configuración regional para el directorio virtual.  
  
 *Error*  
 [out] Descripción del error que se produjo.  
  
 *HRESULT*  
 [out] Valor que indica si la llamada se realizó correctamente o no.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve *HRESULT* que indica si la llamada al método se realizó correctamente o no. Un valor de 0 indica que la llamada al método se realizó correctamente; un código de error indica que la llamada no se realizó correctamente.  
  
## <a name="remarks"></a>Comentarios  
 Una aplicación solo puede tener un nombre de directorio virtual para todas las reservas de direcciones URL.  
  
 VirtualDirectory debe cumplir las convenciones de nomenclatura para directorios virtuales. VirtualDirectory no debe ser una cadena vacía ni estar en blanco.  
  
 Actualiza el valor del elemento \Configuration\URLReservations\Application\VirtualDirectory. Se realiza correctamente aunque no se hayan creado todavía reservas de direcciones URL.  
  
## <a name="requirements"></a>Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Miembros MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
