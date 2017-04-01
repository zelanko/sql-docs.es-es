---
title: "Cmdlet Restore-ASDatabase | Microsoft Docs"
ms.custom: ""
ms.date: "03/07/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 8ab7a2d0-679c-40e6-b9b9-042184b2dfc9
caps.latest.revision: 11
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 11
---
# Cmdlet Restore-ASDatabase
  Restaura un archivo de copia de seguridad de base de datos tabular o multidimensional (.abf) a una instancia de Analysis Services.  
  
## Sintaxis  
 `Restore-ASDatabase [-RestoreFile] <string> [-Name] <string> [-AllowOverwrite <SwitchParameter>] Locations <Microsoft.AnalysisServices.RestoreLocation[]>] [-Security <Microsoft.AnalysisServices.RestoreSecurity>] [-Password <System.SecureString>] [-StorageLocation <System.string>] [-Server <string>] [-Credential <PSCredential>] [<CommonParameters>]`  
  
## Description  
 Permite a un administrador del sistema de Analysis Services restaurar un archivo de copia de seguridad de una base de datos tabular o multidimensional (.abf) en una instancia local o de servidor remoto. Si el archivo que se está restaurando se cifró, puede usar –FilePassword para proporcionar la contraseña que se utiliza para descifrar el archivo.  
  
 Este cmdlet admite el parámetro –Credential, que se puede usar si configuró la instancia de Analysis Services para el acceso HTTP. El parámetro –Credential toma un objeto PSCredential que proporciona una identidad de usuario de Windows. A continuación, IIS suplantará a este usuario al conectarse a Analysis Services. La identidad debe tener permisos de administrador del sistema en la instancia de Analysis Services para restaurar el archivo.  
  
## Parámetros  
  
### -RestoreFile \<cadena>  
 Especifica la ruta de acceso y el nombre del archivo que desea restaurar. Si especifica solo el nombre de archivo, sin una ruta de acceso, se supone la ubicación predeterminada de las copias de seguridad.  
  
|||  
|-|-|  
|¿Requerido?|true|  
|¿Posición?|0|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### -Name \<cadena>  
 Especifica la base de datos de Analysis Services que se va a restaurar.  
  
|||  
|-|-|  
|¿Requerido?|true|  
|¿Posición?|1|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### -AllowOverwrite \<parámetroDeModificador>  
 Sobrescribe una base de datos que usa el mismo nombre y ubicación.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### -Locations \<Microsoft.AnalysisServices.RestoreLocation[]>  
 Especifica la ubicación remota de las particiones que se van a restaurar.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### -Security \<Microsoft.AnalysisServices.RestoreSecurity>  
 Representa la configuración de seguridad utilizada para la operación de restauración. Los valores válidos son CopyAll, SkipMembership e IgnoreSecurity. CopyAll restaura los roles y los miembros. SkipMembership vuelve a crear solo el rol. IgnoreSecurity restaura la base de datos, sin roles.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### -Password \<CadenaSegura>  
 Especifica una contraseña que se utilizará para restaurar un archivo de copia de seguridad cifrado. Debe especificar la contraseña que se usó originalmente para cifrar el archivo.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### -StorageLocation \<cadena>  
 Especifica la ubicación de almacenamiento de base de datos. Es la ubicación de los archivos de la base de datos en el sistema de archivos. Establezca este parámetro si no utiliza la ubicación predeterminada, que es la carpeta de copia de seguridad de la instancia de destino.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### -Server \<cadena>  
 Especifica la instancia de Analysis Services a la que el cmdlet se conectará y ejecutará. Si no se proporciona un nombre de servidor, se establecerá una conexión al host local. Para las instancias predeterminadas, especifique solo el nombre del servidor. Para las instancias con nombre, utilice el formato nombreDeServidor\nombreDeInstancia. En las conexiones HTTP, utilice el formato http[s]://server[:port]/virtualdirectory/msmdpump.dll.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado|localhost|  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### -Credential \<PSCredential>  
 Especifica un objeto PSCredential que proporciona el nombre de usuario y contraseña de Windows. Especifique este parámetro solo si la instancia de Analysis Services está configurada para el acceso HTTP con autenticación básica. Para las conexiones nativas que usan seguridad integrada, este parámetro se omite.  
  
 Si este parámetro está presente, las credenciales que proporcione se anexan a la cadena de conexión. IIS suplantará esta identidad de usuario al conectarse a Analysis Services. Si no se especifica ninguna credencial, se usará la cuenta predeterminada de Windows del usuario que ejecuta la herramienta.  
  
 Para usar este parámetro, cree primero un objeto PSCredential con Get-Credential para especificar el nombre de usuario y la contraseña (por ejemplo, `$Cred=Get-Credential “adventure-works\admin”`. Después, puede canalizar este objeto al parámetro -Credential `(-Credential:$Cred`).  
  
 Para más información sobre el uso de la autenticación y credenciales, vea [PowerShell scripting in Analysis Services](../../analysis-services/instances/powershell-scripting-in-analysis-services.md) (Scripting de PowerShell en Analysis Services). Para más información sobre el acceso HTTP, vea [Configurar el acceso HTTP a Analysis Services en Internet Information Services &#40;IIS&#41; 8.0](../../analysis-services/instances/configure http access to analysis services on iis 8.0.md).  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|True (ByValue)|  
|¿Aceptar caracteres comodín?|false|  
  
### \<ParámetrosComunes>  
 Este cmdlet admite los parámetros comunes: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer y -OutVariable. Para más información, vea [about_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## Entradas y salidas  
 El tipo de entrada es el tipo de objetos que se pueden canalizar al cmdlet. El tipo de valor devuelto es el tipo de objeto que el cmdlet devuelve.  
  
|||  
|-|-|  
|Entradas|System.string<br /><br /> Puede canalizar los valores de cadena al cmdlet.|  
|Salidas|Ninguno.|  
  
## Ejemplo 1  
  
```  
PS SQLSERVER:\SQLAS\localhost\default> restore-asdatabase awtest.abf testawrestoredb –security:CopyAll  
```  
  
 Este comando restaura un archivo de copia de seguridad de Analysis Services (awtest.abf) en la carpeta de copia de seguridad local a la instancia local predeterminada de Analysis Services. El nombre de la base de datos no tiene que existir; en este caso, el nombre de la base de datos se especifica como parte de la operación de restauración. Al agregar –Security:CopyAll se rellenan los roles y la pertenencia a roles desde la base de datos a la nueva base de datos restaurada.  
  
## Ejemplo 2  
  
```  
PS SQLSERVER:\SQLAS\Localhost\default > $pwd = read-host –AsSecureString –Prompt “Password”   
PS SQLSERVER:\SQLAS\Localhost\default > $pwd -is [System.IDisposable]   
PS SQLSERVER:\SQLAS\localhost\default> restore-asdatabase –restorefile testdb.abf –name AWTEST2 –password:$pwd  
PS SQLSERVER:\SQLAS\Localhost\default >$pwd.Dispose()  
PS SQLSERVER:\SQLAS\Localhost\default >Remove-Variable –Name pwd  
```  
  
 Las líneas 1 y 2 se usan para solicitar la contraseña que se usó para cifrar el archivo.  
  
 La línea 3 restaura un archivo de copia de seguridad cifrado de Analysis Services (testdb.abf) de una carpeta de copia de seguridad local de una instancia predeterminada de Analysis Services.  
  
 Las líneas 4 y 5 quitan la contraseña.  
  
## Ejemplo 3 (escenario remoto)  
 En este ejemplo se proporciona una demostración de cómo restaurar un archivo de copia de seguridad local a partir de un recurso compartido de archivos en una instancia remota de Analysis Services. En este ejemplo, se restaura un archivo de copia de seguridad como una base de datos denominada **internetsales** en una instancia predeterminada de Analysis Services, en un equipo llamado **ssas-aw-srv01**.  
  
 El archivo de copia de seguridad se encuentra en un recurso compartido de red, con acceso de lectura público. Es necesario que la instancia remota de Analysis Services tenga permiso de lectura al archivo. La ubicación del archivo tiene que ser un recurso compartido de red (no pueden ser unidades).  
  
 Tenga en cuenta que este ejemplo no depende del proveedor SQLAS. Puede ejecutar el cmdlet como un comando independiente.  
  
```  
PS SQLSERVER:\> restore-asdatabase -restorefile "\\FileServer01\DBFiles\InternetSalesTabular.abf" -name "internetsales  
" -server "SSAS-AW-SRV01"  
```  
  
## Ejemplo 4  
  
```  
PS SQLSERVER:\SQLAS\localhost\default> restore-asdatabase –restorefile “\\myremoteserver\backups\testdb.abf” –name Contoso_Retail –server myremoteserver –storagelocation “\\myremoteserver\restoreDBFiles”  
```  
  
 Este comando restaura un archivo de copia de seguridad cifrado de Analysis Services (testdb.abf) en una carpeta de copia de seguridad remota en una instancia predeterminada de Analysis Services remota. El parámetro –StorageLocation se utiliza para colocar los archivos de base de datos en una ubicación que no es la predeterminada, en este caso, un archivo compartido denominado restoreDBfiles.  
  
## Vea también  
 [PowerShell scripting in Analysis Services](../../analysis-services/instances/powershell-scripting-in-analysis-services.md)   
 [Administrar modelos tabulares con PowerShell](http://go.microsoft.com/fwlink/?linkID=227685)  
  
  