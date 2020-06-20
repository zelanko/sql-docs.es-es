---
title: Administración de la autenticación en PowerShell del motor de base de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: ab9212a6-6628-4f08-a38c-d3156e05ddea
author: stevestein
ms.author: sstein
ms.openlocfilehash: cd9919b17e0422a9308e36cd1befb6865a67ff67
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84960405"
---
# <a name="manage-authentication-in-database-engine-powershell"></a>Administrar la autenticación en PowerShell del motor de base de datos
  De forma predeterminada, los componentes PowerShell de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usan la autenticación de Windows para conectarse a una instancia de [!INCLUDE[ssDE](../includes/ssde-md.md)]. Puede usar la autenticación de SQL Server definiendo una unidad virtual de PowerShell o especificando los parámetros de `-Username` y de `-Password` para `Invoke-Sqlcmd`.  
  
1.  **Antes de empezar:**  [Permisos](#Permissions)  
  
2.  **Para establecer la autenticación con:**  [Una unidad virtual](#SQLAuthVirtDrv), [Invoke-Sqlcmd](#SQLAuthInvSqlCmd)  
  
##  <a name="permissions"></a><a name="Permissions"></a> Permisos  
 Todas las acciones que se pueden realizar en una instancia de [!INCLUDE[ssDE](../includes/ssde-md.md)] se controlan mediante los permisos concedidos a las credenciales de autenticación usadas para conectarse a la instancia. De forma predeterminada, el proveedor y los cmdlets de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] usa la cuenta de Windows de ejecución para establecer una conexión de autenticación de Windows con [!INCLUDE[ssDE](../includes/ssde-md.md)].  
  
 Para establecer una conexión de autenticación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] debe proporcionar un identificador de inicio de sesión y contraseña de autenticación de SQL Server. Al usar el [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] proveedor, debe asociar las [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] credenciales de inicio de sesión a una unidad virtual y, a continuación, usar el comando de cambio de directorio ( `cd` ) para conectarse a esa unidad. En Windows PowerShell, las credenciales de seguridad solo se pueden asociar con unidades virtuales.  
  
##  <a name="sql-server-authentication-using-a-virtual-drive"></a><a name="SQLAuthVirtDrv"></a> Autenticación de SQL Server mediante una unidad virtual  
 **Para crear una unidad virtual asociada con el inicio de sesión de autenticación de SQL Server**  
  
1.  Crear una función que:  
  
    1.  Tiene parámetros para que el nombre proporcione la unidad virtual, el identificador de inicio de sesión y la ruta de acceso del proveedor para asociarla a la unidad virtual.  
  
    2.  Usa `read-host` para solicitar la contraseña al usuario.  
  
    3.  Usa `new-object` para crear un objeto de credenciales.  
  
    4.  Usa `new-psdrive` para crear una unidad virtual con las credenciales proporcionadas.  
  
2.  Invocar la función para crear una unidad virtual con las credenciales proporcionadas.  
  
### <a name="example-virtual-drive"></a>Ejemplo (unidad virtual)  
 En este ejemplo se crea una función denominada **sqldrive** que se puede usar para crear una unidad virtual asociada a la instancia e inicio de sesión de la autenticación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] especificados.  
  
 La función **sqldrive** pide que especifique la contraseña para su inicio de sesión, enmascarándola a medida que la escribe. Después, siempre que use el comando de cambio de directorio ( `cd` ) para conectarse a una ruta de acceso mediante el nombre de la unidad virtual, todas las operaciones se realizan mediante las [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] credenciales de inicio de sesión de autenticación que proporcionó al crear la unidad.  
  
```powershell
## Create a function that specifies the login and prompts for the password.  
  
function sqldrive  
{  
    param( [string]$name, [string]$login = "MyLogin", [string]$root = "SQLSERVER:\SQL\MyComputer\MyInstance" )  
    $pwd = Read-Host -AsSecureString -Prompt "Password"  
    $cred = New-Object System.Management.Automation.PSCredential -argumentlist $login, $pwd  
    New-PSDrive $name -PSProvider SqlServer -Root $root -Credential $cred -Scope 1  
}  
  
## Use the sqldrive function to create a SQLAuth virtual drive.  
sqldrive SQLAuth  
  
## CD to the virtual drive, which invokes the supplied authentication credentials.  
cd SQLAuth  
```  
  
##  <a name="sql-server-authentication-using-invoke-sqlcmd"></a><a name="SQLAuthInvSqlCmd"></a> Autenticación de SQL Server mediante Invoke-Sqlcmd  
 **Para usar Invoke-Sqlcmd con la autenticación de SQL Server**  
  
1.  Use el parámetro de `-Username` para especificar un identificador de inicio de sesión y el parámetro de `-Password` para especificar la contraseña asociada.  
  
### <a name="example-invoke-sqlcmd"></a>Ejemplo (Invoke-Sqlcmd)  
 En este ejemplo se usa el cmdlet read-host para pedir al usuario una contraseña, y después se conecta con la autenticación de SQL Server.  
  
```powershell
## Prompt the user for their password.  
$pwd = Read-Host -AsSecureString -Prompt "Password"  
  
Invoke-Sqlcmd -Query "SELECT GETDATE() AS TimeOfQuery;" -ServerInstance "MyComputer\MyInstance" -Username "MyLogin" -Password $pwd  
```  
  
## <a name="see-also"></a>Consulte también  
 [SQL Server PowerShell](sql-server-powershell.md)   
 [Proveedor de SQL Server PowerShell](sql-server-powershell-provider.md)   
 [cmdlet Invoke-Sqlcmd](../database-engine/invoke-sqlcmd-cmdlet.md)  
