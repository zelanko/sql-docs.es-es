---
title: Método GenerateDatabaseCreationScript (MSReportServer_ConfigurationSetting de WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
api_name:
- GenerateDatabaseCreationScript (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- GenerateDatabaseCreationScript method
ms.assetid: 25232dc7-00fe-4cd1-8a1c-7e36d552de00
caps.latest.revision: 25
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 42898aba8f621688ba229fcf01d367b4da1a4f71
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37149036"
---
# <a name="generatedatabasecreationscript-method-wmi-msreportserverconfigurationsetting"></a>Método GenerateDatabaseCreationScript (MSReportServer_ConfigurationSetting de WMI)
  Genera un script SQL que se puede utilizar para crear una base de datos del servidor de informes.  
  
## <a name="syntax"></a>Sintaxis  
  
```vb  
Public Sub GenerateDatabaseCreationScript(ByVal DatabaseName As String, _  
    ByVal Lcid As Int32, ByVal IsSharePointMode As Boolean, ByRef Script As String, _  
    ByRef HRESULT As Int32)  
```  
  
```csharp  
public void GenerateDatabaseCreationScript(string DatabaseName, Int32 Lcid,   
    Boolean IsSharePointMode, out string Script, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parámetros  
 *Databasename*  
 Cadena que contiene el nombre de la base de datos del servidor de informes que se va a crear.  
  
 *Lcid*  
 Valor usado para la localización de nombres de roles.  
  
 *IsSharePointMode*  
 Indica si se desea crear la base de datos en modo nativo o en modo de SharePoint.  
  
> [!IMPORTANT]  
>  A partir de [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], *IsSharePointMode* = `True` no se admite porque en el modo de SharePoint, [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] es el servicio compartido de SharePoint y no esté controlado por el proveedor de WMI. Este parámetro siempre debe establecerse `False`.  
  
 *Script*  
 [out] Cadena que contiene el script SQL generado.  
  
 *HRESULT*  
 [out] Valor que indica si la llamada se realizó correctamente o no.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve *HRESULT* que indica si la llamada al método se realizó correctamente o no. Un valor de 0 indica que la llamada al método se realizó correctamente. Un valor distinto de cero indica que se ha producido un error.  
  
## <a name="remarks"></a>Notas  
 Este método genera un script SQL que crea bases de datos del servidor de informes para la versión del servidor de informes al que se está conectado actualmente.  
  
 El valor proporcionado en el parámetro *DatabaseName* debe cumplir las convenciones de nomenclatura de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 El método no comprueba la existencia de la base de datos al generar el script.  
  
 Este método no comprueba la existencia de la base de datos del servidor de informes al generar el script.  
  
 El script generado admite [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 y [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
## <a name="requirements"></a>Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Miembros MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
