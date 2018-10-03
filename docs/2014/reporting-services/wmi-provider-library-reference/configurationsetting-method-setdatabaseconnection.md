---
title: Método SetDatabaseConnection (MSReportServer_ConfigurationSetting de WMI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
api_name:
- SetDatabaseConnection (WMI MSReportServer_ConfigurationSetting Class)
api_location:
- reportingservices.mof
topic_type:
- apiref
helpviewer_keywords:
- SetDatabaseConnection method
ms.assetid: c040aa78-92b8-41e4-9ae2-eff9fcdddc5b
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 68907320922f0181521a9ff30de708f660e8dd8c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48207105"
---
# <a name="setdatabaseconnection-method-wmi-msreportserverconfigurationsetting"></a>Método SetDatabaseConnection (WMI MSReportServer_ConfigurationSetting)
  Define la conexión de la base de datos del servidor de informes a una base de datos de servidor de informes concreta.  
  
## <a name="syntax"></a>Sintaxis  
  
```vb  
Public Sub SetDatabaseConnection(Server as String, _  
    DatabaseName as string, CredentialsType as Integer, _  
    Username as String, Password as String, ByRef HRESULT as Int32)  
```  
  
```csharp  
public void BackupEncryptionKey(string Server,   
    string DatabaseName, Int32 CredentialsType,   
    string UserName, string Password, out Int32 HRESULT);  
```  
  
## <a name="parameters"></a>Parámetros  
 *Server*  
 Nombre de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se usa para hospedar la base de datos del servidor de informes.  
  
 *DatabaseName*  
 El nombre de la base de datos del servidor de informes.  
  
 *CredentialsType*  
 El tipo de credenciales que se utilizará para la conexión. Los valores pueden ser:  
  
-   0 - Windows  
  
-   1 – [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   2 - Servicio de Windows  
  
 *UserName*  
 El nombre de la cuenta utilizada para conectarse a la base de datos del servidor de informes.  
  
 *Contraseña*  
 La contraseña utilizada para conectarse a la base de datos del servidor de informes.  
  
 *HRESULT*  
 [out] Valor que indica si la llamada se realizó correctamente o no.  
  
## <a name="return-value"></a>Valor devuelto  
 Devuelve *HRESULT* que indica si la llamada al método se realizó correctamente o no. Un valor de 0 indica que la llamada al método se realizó correctamente. Un valor distinto de cero indica que se ha producido un error.  
  
## <a name="remarks"></a>Comentarios  
 Cuando el parámetro *CredentialsType* se define en 0 (Windows), deben definirse los parámetros *UserName* y *Password* . El parámetro *UserName* debe tener el formato "dominio\nombre de usuario" y el valor debe representar un inicio de sesión de Windows válido.  
  
 Cuando el parámetro *CredentialsType* se establece en 1 ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]), el valor pasado en el parámetro *UserName* debe cumplir los requisitos de un nombre de inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Cuando el parámetro *CredentialsType* se establece en 2 (servicio de Windows), el servidor de informes usa la seguridad integrada para conectarse a la base de datos del servidor de informes y se omiten los parámetros *UserName* y *Password* . El servicio web del servidor de informes utilizará la cuenta [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] o una cuenta de un grupo de aplicaciones y la cuenta del servicio de Windows para tener acceso a la base de datos del servidor de informes.  
  
 Cuando se llama, el método SetDatabaseConnection cifra y almacena las credenciales y la información de la base de datos en el archivo de configuración del servidor de informes especificado.  
  
 El método SetDatabaseConnection no comprueba que el servidor de informes pueda conectarse a la base de datos del servidor de informes usando los datos especificados.  
  
 Cuando se establece por primera vez, la propiedad ConnectionPoolSize se establece en función de los procesadores siguientes: ConnectionPoolSize = #Processors * 75.  
  
 El método SetDatabaseConnection no concede permisos a las cuentas especificadas. Debe llamar a la [GenerateDatabaseRightsScript](configurationsetting-method-generatedatabaserightsscript.md) método para cada cuenta que requiere acceso a la base de datos del servidor de informes y ejecuta el script resultante.  
  
## <a name="requirements"></a>Requisitos  
 **Espacio de nombres:** [!INCLUDE[ssRSWMInmspcA](../../includes/ssrswminmspca-md.md)]  
  
## <a name="see-also"></a>Vea también  
 [Miembros MSReportServer_ConfigurationSetting](msreportserver-configurationsetting-members.md)  
  
  
