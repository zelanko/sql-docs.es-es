---
title: Método GenerateDatabaseRightsScript (MSReportServer_ConfigurationSetting de WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
api_name:
- GenerateDatabaseRightsScript (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- GenerateDatabaseRightsScript method
ms.assetid: f2e6dcc9-978f-4c2c-bafe-36c330247fd0
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d9f27779115d510e9f11c0ec54c844ba17a391cb
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/22/2019
ms.locfileid: "59950751"
---
# <a name="generatedatabaserightsscript-method-wmi-msreportserverconfigurationsetting"></a>Método GenerateDatabaseRightsScript (WMI MSReportServer_ConfigurationSetting)
  Genera un script SQL que se puede usar para conceder derechos a un usuario sobre la base de datos del servidor de informes y otras bases de datos necesarias para el funcionamiento de un servidor de informes. Se espera que el autor de la llamada se conecte al servidor de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y ejecute el script.  
  
## <a name="syntax"></a>Sintaxis  
  
```vb  
Public Sub GenerateDatabaseRightsScript(ByVal UserName As String, _  
    ByVal DatabaseName As String, ByVal IsRemote As Boolean, _  
    ByVal IsWindowsUser As Boolean, ByRef Script As String, _  
    ByRef HRESULT As Int32)  
```  
  
```csharp  
public void GenerateDatabaseRightsScript(string UserName, string DatabaseName, bool IsRemote, bool IsWindowsUser, out string Script,   
out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parámetros  
 *UserName*  
 Nombre de usuario o identificador de seguridad de Windows (SID) del usuario al que el script concederá derechos.  
  
 *DatabaseName*  
 Nombre de base de datos para el que el script concederá acceso al usuario.  
  
 *IsRemote*  
 Valor booleano que indica si la base de datos es remota desde el servidor de informes.  
  
 *IsWindowsUser*  
 Valor booleano que indica si el nombre de usuario especificado es un usuario de Windows o un usuario de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 *Script*  
 [out] Una cadena que contiene el script [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generado.  
  
 *HRESULT*  
 [out] Valor que indica si la llamada se realizó correctamente o no.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve *HRESULT* que indica si la llamada al método se realizó correctamente o no. Un valor de 0 indica que la llamada al método se realizó correctamente. Un valor distinto de cero indica que se ha producido un error.  
  
## <a name="remarks"></a>Comentarios  
 Si *DatabaseName* está vacío, *IsRemote* se omite y el valor del archivo de configuración del servidor de informes se usa para el nombre de base de datos.  
  
 Si *IsWindowsUser* está establecido en `true`, *UserName* debe tener el formato \<dominio >\\< nombre de usuario\>.  
  
 Cuando *IsWindowsUser* está establecido en `true`, el script generado concede derechos de inicio de sesión al usuario para el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], establecer la base de datos del servidor de informes como la base de datos predeterminada y concede el **RSExec** rol en la base de datos del servidor de informes, la base de datos temporal del servidor informes, la base de datos maestra y la base de datos del sistema MSDB.  
  
 Cuando *IsWindowsUser* está establecido en `true`, el método acepta los SID de Windows estándar como entrada. Cuando se proporciona un SID de Windows estándar o el nombre de la cuenta de servicio, se traduce a una cadena de nombre de usuario. Si la base de datos es local, la cuenta se traduce a la representación localizada correcta de la cuenta. Si la base de datos es remota, la cuenta se representa como la cuenta del equipo.  
  
 En la tabla siguiente, se muestran las cuentas que están traducidas y su representación remota.  
  
|Cuenta / SID traducido|Nombre común|Nombre remoto|  
|---------------------------------------|-----------------|-----------------|  
|(S-1-5-18)|Sistema local|\<Dominio>\\<nombreDeEquipo\>$|  
|.\LocalSystem|Sistema local|\<Dominio>\\<nombreDeEquipo\>$|  
|NombreDeEquipo\LocalSystem|Sistema local|\<Dominio>\\<nombreDeEquipo\>$|  
|LocalSystem (Sistema local)|Sistema local|\<Dominio>\\<nombreDeEquipo\>$|  
|(S-1-5-20)|Servicio de red|\<Dominio>\\<nombreDeEquipo\>$|  
|NT AUTHORITY\NetworkService|Servicio de red|\<Dominio>\\<nombreDeEquipo\>$|  
|(S-1-5-19)|Servicio local|Error: vea a continuación.|  
|NT AUTHORITY\LocalService|Servicio local|Error: vea a continuación.|  
  
 En [!INCLUDE[win2kfamily](../../includes/win2kfamily-md.md)], si está utilizando una cuenta integrada y la base de datos del servidor de informes es remota, se devuelve un error.  
  
 Si se especifica la cuenta integrada `LocalService` y la base de datos del servidor de informes es remota, se devuelve un error.  
  
 Cuando *IsWindowsUser* es verdadero y el valor proporcionado en *UserName* debe traducirse, el proveedor WMI determina si la base de datos del servidor de informes se encuentra en el mismo equipo o en un equipo remoto. Para determinar si la instalación es local, el proveedor WMI evalúa la propiedad DatabaseServerName con la lista siguiente de valores. Si se encuentra una coincidencia, la base de datos es local. De lo contrario, es remota. La comparación distingue entre mayúsculas y minúsculas.  
  
|Valor de DatabaseServerName|Ejemplo|  
|---------------------------------|-------------|  
|"."||  
|"(local)"||  
|"LOCAL"||  
|localhost||  
|\<Machinename>|testlab14|  
|\<MachineFQDN>|example.redmond.microsoft.com|  
|\<IPAddress>|180.012.345,678|  
  
 Cuando *IsWindowsUser* está establecido en `true`, el proveedor WMI llama a LookupAccountName para obtener el SID de la cuenta y, a continuación, llama a LookupAccountSID para obtener el nombre e insertarlo el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] secuencia de comandos. Esto asegura que el nombre de la cuenta que se utiliza pasará la validación [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Cuando *IsWindowsUser* está establecido en `false`, el script generado concede el **RSExec** rol en la base de datos del servidor de informes, la base de datos temporal del servidor informes y la base de datos MSDB.  
  
 Cuando *IsWindowsUser* está establecido en `false`, el usuario de SQL Server ya debe existir en el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para el script se ejecute correctamente.  
  
 Si el servidor de informes no cuenta con una base de datos del servidor de informes especificada, al llamar a GrantRightsToDatabaseUser se devuelve un error.  
  
 El script generado admite [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2005 y [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
## <a name="requirements"></a>Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Miembros MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
