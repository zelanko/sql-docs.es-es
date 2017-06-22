---
title: "Administración de la autenticación en PowerShell del motor de base de datos | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ab9212a6-6628-4f08-a38c-d3156e05ddea
caps.latest.revision: 9
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 135580dd67315ad9eb07361dcff7b1334398a0aa
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="manage-authentication-in-database-engine-powershell"></a>Administrar la autenticación en PowerShell del motor de base de datos
  De forma predeterminada, los componentes PowerShell de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usan la autenticación de Windows para conectarse a una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Puede usar la autenticación de SQL Server definiendo una unidad virtual de PowerShell o especificando los parámetros **–Username** y **–Password** para **Invoke-Sqlcmd**.  
  
1.  **Before you begin:**  [Permissions](#Permissions)  
  
2.  **To set authentication, using:**  [A Virtual Drive](#SQLAuthVirtDrv), [Invoke-Sqlcmd](#SQLAuthInvSqlCmd)  
  
##  <a name="Permissions"></a> Permisos  
 Todas las acciones que se pueden realizar en una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] se controlan mediante los permisos concedidos a las credenciales de autenticación usadas para conectarse a la instancia. De forma predeterminada, el proveedor y los cmdlets de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa la cuenta de Windows de ejecución para establecer una conexión de autenticación de Windows con [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 Para establecer una conexión de autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe proporcionar un identificador de inicio de sesión y contraseña de autenticación de SQL Server. Al usar el proveedor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , debe asociar las credenciales de inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a una unidad virtual y, después, usar el comando de cambio de directorio (**cd**) para conectarse a esa unidad de disco. En Windows PowerShell, las credenciales de seguridad solo se pueden asociar con unidades virtuales.  
  
##  <a name="SQLAuthVirtDrv"></a> Autenticación de SQL Server mediante una unidad virtual  
 **Para crear una unidad virtual asociada con el inicio de sesión de autenticación de SQL Server**  
  
1.  Crear una función que:  
  
    1.  Tiene parámetros para que el nombre proporcione la unidad virtual, el identificador de inicio de sesión y la ruta de acceso del proveedor para asociarla a la unidad virtual.  
  
    2.  Usa **read-host** para pedir la contraseña al usuario.  
  
    3.  Usa **new-object** para crear un objeto de credenciales.  
  
    4.  Usa **new-psdrive** para crear una unidad virtual con las credenciales proporcionadas.  
  
2.  Invocar la función para crear una unidad virtual con las credenciales proporcionadas.  
  
### <a name="example-virtual-drive"></a>Ejemplo (unidad virtual)  
 En este ejemplo se crea una función denominada **sqldrive** que se puede usar para crear una unidad virtual asociada a la instancia e inicio de sesión de la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificados.  
  
 La función **sqldrive** pide que especifique la contraseña para su inicio de sesión, enmascarándola a medida que la escribe. Siempre que use el comando de cambio de directorio (**cd**) para conectar a una ruta de acceso usando el nombre de la unidad virtual, todas las operaciones se realizan usando las credenciales de inicio de sesión de la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que especificó al crear la unidad.  
  
```  
## Create a function that specifies the login and prompts for the password.  
  
function sqldrive  
{  
    param( [string]$name, [string]$login = "MyLogin", [string]$root = "SQLSERVER:\SQL\MyComputer\MyInstance" )  
    $pwd = read-host -AsSecureString -Prompt "Password"  
    $cred = new-object System.Management.Automation.PSCredential -argumentlist $login,$pwd  
    New-PSDrive $name -PSProvider SqlServer -Root $root -Credential $cred -Scope 1  
}  
  
## Use the sqldrive function to create a SQLAuth virtual drive.  
sqldrive SQLAuth  
  
## CD to the virtual drive, which invokes the supplied authentication credentials.  
cd SQLAuth  
```  
  
##  <a name="SQLAuthInvSqlCmd"></a> Autenticación de SQL Server mediante Invoke-Sqlcmd  
 **Para usar Invoke-Sqlcmd con la autenticación de SQL Server**  
  
1.  Use el parámetro de **–Username** para especificar un identificador de inicio de sesión y el parámetro de **–Password** para especificar la contraseña asociada.  
  
### <a name="example-invoke-sqlcmd"></a>Ejemplo (Invoke-Sqlcmd)  
 En este ejemplo se usa el cmdlet read-host para pedir al usuario una contraseña, y después se conecta con la autenticación de SQL Server.  
  
```  
## Prompt the user for their password.  
$pwd = read-host -AsSecureString -Prompt "Password"  
  
Invoke-Sqlcmd -Query "SELECT GETDATE() AS TimeOfQuery;" -ServerInstance "MyComputer\MyInstance" –Username “MyLogin” –Password $pwd  
```  
  
## <a name="see-also"></a>Vea también  
 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)   
 [Proveedor de PowerShell de SQL Server](../../relational-databases/scripting/sql-server-powershell-provider.md)   
 [cmdlet Invoke-Sqlcmd](../../powershell/invoke-sqlcmd-cmdlet.md)  
  
  
