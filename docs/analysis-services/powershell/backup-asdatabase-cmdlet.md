---
title: Cmdlet backup-ASDatabase | Documentos de Microsoft
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: powershell
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 03d58a82-021c-4e13-b265-c084f42a8bb2
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: cc648f0ad73c9ed39f49e823fe4293b57ff0d470
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="backup-asdatabase-cmdlet"></a>Cmdlet Backup-ASDatabase

[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  Copia de seguridad de base de datos multidimensional o tabular de Analysis Services en un archivo de copia de seguridad de Analysis Services (.abf).  

>[!NOTE] 
>En este artículo puede contener información no actualizada y ejemplos. Use el cmdlet Get-Help para la versión más reciente.
  
## <a name="syntax"></a>Sintaxis  
 `Backup-ASDatabase [-BackupFile] <string> [-Name] <string> [-AllowOverwrite <SwitchParameter>] [-BackupRemotePartitions <SwitchParameter>] [-ApplyCompression <SwitchParameter>] [-FilePassword <SecureString>] [-Locations <Microsoft.AnalysisServices.BackupLocation[]>] [-Server <string>] [-Credential <PSCredential>] [<CommonParameters>]`  
  
 `Backup-ASDatabase –Database <Microsoft.AnalysisServices.Database> [-AllowOverwrite <SwitchParameter>] [-BackupRemotePartitions <SwitchParameter>] [-ApplyCompression <SwitchParameter>] [-FilePassword <SecureString>] [-Locations <Microsoft.AnalysisServices.BackupLocation[]>] [-Server <string>] [-Credential <PSCredential>] [<CommonParameters>]`  
  
## <a name="description"></a>Description  
 Permite a un administrador del sistema de Analysis Services realizar la copia de seguridad de una base de datos multidimensional o tabular en un archivo de copia de seguridad. Si no especifica ninguna ubicación, se utiliza la ubicación predeterminada de las copias de seguridad que se especificó durante la instalación.  
  
 Los archivos de los que realice la copia de seguridad pueden estar cifrados. Use –FilePassword para cifrar el archivo. Al restaurar el archivo más adelante, debe proporcionar la misma contraseña que especificó para cifrarlo.  
  
 Este cmdlet admite el parámetro –Credential, que se puede usar si configuró la instancia de Analysis Services para el acceso HTTP. El parámetro –Credential toma un objeto PSCredential que proporciona una identidad de usuario de Windows. A continuación, IIS suplantará a este usuario al conectarse a Analysis Services. La identidad debe tener permisos de administrador del sistema en la instancia de Analysis Services para realizar la copia de seguridad.  
  
## <a name="parameters"></a>Parámetros  
  
### <a name="-backupfile-string"></a>-BackupFile \<cadena >  
 Especifica la ruta de acceso y el nombre del archivo de copia de seguridad. Si especifica solo un nombre de archivo sin una ruta de acceso, se utilizará la ubicación predeterminada de las copias de seguridad. Este parámetro solo se utiliza con el parámetro –Name.  
  
|||  
|-|-|  
|¿Requerido?|true|  
|¿Posición?|0|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-name-string"></a>-Nombre \<cadena >  
 Especifica la base de datos de Analysis Services de la que se va a hacer una copia de seguridad. Puede especificar una base de datos con el parámetro –Database o –Name, si desea pasar el nombre como una cadena.  
  
|||  
|-|-|  
|¿Requerido?|true|  
|¿Posición?|1|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-allowoverwrite-switchparameter"></a>-AllowOverwrite \<SwitchParameter >  
 Sobrescribe un archivo de copia de seguridad del mismo nombre.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-backupremotepartitions-switchparameter"></a>-BackupRemotePartitions \<SwitchParameter >  
 Especifica si las particiones remotas se incluirán en la copia de seguridad.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-applycompressionswitchparameter"></a>-ApplyCompression\<SwitchParameter >  
 Especifica si se comprime el archivo de copia de seguridad.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-filepassword-securestring"></a>-FilePassword \<SecureString >  
 Especifica una contraseña que se va a usar con el cifrado del archivo de copia de seguridad.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-locations-microsoftanalysisservicesbackuplocation"></a>-Ubicaciones \<Microsoft.AnalysisServices.BackupLocation] >  
 Especifica la ubicación en la que se almacenará el archivo de copia de seguridad.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-server-string"></a>-Server \<cadena >  
 Especifica la instancia de Analysis Services a la que el cmdlet se conectará y ejecutará. Si no se proporciona un nombre de servidor, se establecerá una conexión al host local. Para las instancias predeterminadas, especifique solo el nombre del servidor. Para las instancias con nombre, utilice el formato nombreDeServidor\nombreDeInstancia. En las conexiones HTTP, utilice el formato http[s]://server[:port]/virtualdirectory/msmdpump.dll.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado|localhost|  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-credential-pscredential"></a>-Credential \<PSCredential >  
 Especifica un objeto PSCredential que proporciona el nombre de usuario y contraseña de Windows. Especifique este parámetro solo si la instancia de Analysis Services está configurada para el acceso HTTP con autenticación básica. Para las conexiones nativas que usan seguridad integrada, este parámetro se omite.  
  
 Si este parámetro está presente, las credenciales que proporcione se anexan a la cadena de conexión. IIS suplantará esta identidad de usuario al conectarse a Analysis Services. Si no se especifica ninguna credencial, se usará la cuenta predeterminada de Windows del usuario que ejecuta la herramienta.  
  
 Para usar este parámetro, cree primero un objeto PSCredential con Get-Credential para especificar el nombre de usuario y la contraseña (por ejemplo, `$Cred=Get-Credential “adventure-works\admin”`. Después, puede canalizar este objeto al parámetro -Credential `(-Credential:$Cred`).  
  
Para más información, vea [Configurar el acceso HTTP a Analysis Services en Internet Information Services &#40;IIS&#41; 8.0](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md).  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|True (ByValue)|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-database-microsoftanalysisservicesdatabase"></a>-Base de datos \<Microsoft.AnalysisServices.Database] >  
 Especifica un objeto de base de datos de Analysis Services cuya copia de seguridad se va a hacer. Puede especificar una base de datos mediante el parámetro –Database o –Nombre. Use –Database si desea canalizar el nombre de la base de datos.  
  
|||  
|-|-|  
|¿Requerido?|true|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|true|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="commonparameters"></a>\<CommonParameters >  
 Este cmdlet admite los parámetros comunes: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer y -OutVariable. Para más información, vea [about_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## <a name="inputs-and-outputs"></a>Entradas y salidas  
 El tipo de entrada es el tipo de objetos que se pueden canalizar al cmdlet. El tipo de valor devuelto es el tipo de objeto que el cmdlet devuelve.  
  
|||  
|-|-|  
|Entradas|Microsoft.AnalysisServices.Database<br /><br /> Puede canalizar varias bases de datos de las que desee realizar una copia de seguridad, por ejemplo, todas las bases de datos de una instancia específica.|  
|Salidas|Ninguno.|  
  
## <a name="example-1"></a>Ejemplo 1  
  
```  
PS SQLSERVER:\SQLAS\Localhost\default >backup-asdatabase awdb-20110930.abf “Adventure Works” -AllowOverwrite -ApplyCompression  
```  
  
 Este comando realiza la copia de seguridad de la base de datos Adventure Works un archivo .abf en la ubicación predeterminada de copia de seguridad. Si existe un archivo con el mismo nombre en la ubicación, se sobrescribe.  
  
## <a name="example-2"></a>Ejemplo 2  
  
```  
PS SQLSERVER:\SQLAS\Localhost\default >$AWDB = get-item “databases\Adventure Works”   
PS SQLSERVER:\SQLAS\Localhost\default >Backup-asdatabase –database:$AWDB –AllowOverwrite  
```  
  
 Este comando utiliza –Database en lugar de -Backupfile y -Name. Utilice el parámetro –Database cuando desee canalizar el nombre de la base de datos al cmdlet.  
  
## <a name="example-3"></a>Ejemplo 3  
  
```  
PS SQLSERVER:\SQLAS\Localhost\default\databases >dir * | backup-asdatabase  
```  
  
 Este comando realiza la copia de seguridad de todas las bases de datos del servidor local.  
  
## <a name="example-4"></a>Ejemplo 4  
  
```  
PS SQLSERVER:\SQLAS\Localhost\default > $pwd = read-host –AsSecureString –Prompt “Password”   
PS SQLSERVER:\SQLAS\Localhost\default > $pwd -is [System.IDisposable]   
PS SQLSERVER:\SQLAS\Localhost\default > backup-asdatabase –backupfile test.abf –name contoso_retail –filepassword:$pwd server myremoteserver  
PS SQLSERVER:\SQLAS\Localhost\default >$pwd.Dispose()  
PS SQLSERVER:\SQLAS\Localhost\default >Remove-Variable –Name pwd  
```  
  
 Las líneas 1 y 2 se usan para solicitar una contraseña que se utilizará para cifrar el archivo.  
  
 En la línea 3 se hace una copia de seguridad de la base de datos de ejemplo Contoso_Retail de un servidor remoto de Analysis Services en un archivo de copia de seguridad de Analysis Services denominado test.abf, también situado en el servidor remoto. El archivo se guarda en la carpeta de copia de seguridad predeterminada de la instancia predeterminada.  
  
 Las líneas 4 y 5 quitan la contraseña.  
  
  
  
