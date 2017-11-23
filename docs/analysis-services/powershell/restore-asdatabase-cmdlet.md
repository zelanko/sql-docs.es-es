---
title: Cmdlet Restore-ASDatabase | Documentos de Microsoft
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
ms.assetid: 8ab7a2d0-679c-40e6-b9b9-042184b2dfc9
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ae57bdc2a1f385e06248ab9486b7ef5fc07f7932
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="restore-asdatabase-cmdlet"></a>Cmdlet Restore-ASDatabase

[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  Restaura un archivo de copia de seguridad de base de datos tabular o multidimensional (.abf) a una instancia de Analysis Services.  

>[!NOTE] 
>En este artículo puede contener información no actualizada y ejemplos. Use el cmdlet Get-Help para la versión más reciente.
  
## <a name="syntax"></a>Sintaxis  
 `Restore-ASDatabase [-RestoreFile] <string> [-Name] <string> [-AllowOverwrite <SwitchParameter>] Locations <Microsoft.AnalysisServices.RestoreLocation[]>] [-Security <Microsoft.AnalysisServices.RestoreSecurity>] [-Password <System.SecureString>] [-StorageLocation <System.string>] [-Server <string>] [-Credential <PSCredential>] [<CommonParameters>]`  
  
## <a name="description"></a>Description  
 Permite a un administrador del sistema de Analysis Services restaurar un archivo de copia de seguridad de una base de datos tabular o multidimensional (.abf) en una instancia local o de servidor remoto. Si el archivo que se está restaurando se cifró, puede usar –FilePassword para proporcionar la contraseña que se utiliza para descifrar el archivo.  
  
 Este cmdlet admite el parámetro –Credential, que se puede usar si configuró la instancia de Analysis Services para el acceso HTTP. El parámetro –Credential toma un objeto PSCredential que proporciona una identidad de usuario de Windows. A continuación, IIS suplantará a este usuario al conectarse a Analysis Services. La identidad debe tener permisos de administrador del sistema en la instancia de Analysis Services para restaurar el archivo.  
  
## <a name="parameters"></a>Parámetros  
  
### <a name="-restorefile-string"></a>-RestoreFile \<cadena >  
 Especifica la ruta de acceso y el nombre del archivo que desea restaurar. Si especifica solo el nombre de archivo, sin una ruta de acceso, se supone la ubicación predeterminada de las copias de seguridad.  
  
|||  
|-|-|  
|¿Requerido?|true|  
|¿Posición?|0|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-name-string"></a>-Nombre \<cadena >  
 Especifica la base de datos de Analysis Services que se va a restaurar.  
  
|||  
|-|-|  
|¿Requerido?|true|  
|¿Posición?|1|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-allowoverwrite-switchparameter"></a>-AllowOverwrite \<SwitchParameter >  
 Sobrescribe una base de datos que usa el mismo nombre y ubicación.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-locations-microsoftanalysisservicesrestorelocation"></a>-Ubicaciones \<Microsoft.AnalysisServices.RestoreLocation] >  
 Especifica la ubicación remota de las particiones que se van a restaurar.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-security-microsoftanalysisservicesrestoresecurity"></a>-Security \<Microsoft.AnalysisServices.RestoreSecurity >  
 Representa la configuración de seguridad utilizada para la operación de restauración. Los valores válidos son CopyAll, SkipMembership e IgnoreSecurity. CopyAll restaura los roles y los miembros. SkipMembership vuelve a crear solo el rol. IgnoreSecurity restaura la base de datos, sin roles.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-password-securestring"></a>-Contraseña \<SecureString >  
 Especifica una contraseña que se utilizará para restaurar un archivo de copia de seguridad cifrado. Debe especificar la contraseña que se usó originalmente para cifrar el archivo.  
  
|||  
|-|-|  
|¿Requerido?|false|  
|¿Posición?|con nombre|  
|Valor predeterminado||  
|¿Aceptar la entrada de la canalización?|false|  
|¿Aceptar caracteres comodín?|false|  
  
### <a name="-storagelocation-string"></a>-StorageLocation \<cadena >  
 Especifica la ubicación de almacenamiento de base de datos. Es la ubicación de los archivos de la base de datos en el sistema de archivos. Establezca este parámetro si no utiliza la ubicación predeterminada, que es la carpeta de copia de seguridad de la instancia de destino.  
  
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
  
### <a name="commonparameters"></a>\<CommonParameters >  
 Este cmdlet admite los parámetros comunes: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer y -OutVariable. Para más información, vea [about_CommonParameters](http://go.microsoft.com/fwlink/?linkID=227825).  
  
## <a name="inputs-and-outputs"></a>Entradas y salidas  
 El tipo de entrada es el tipo de objetos que se pueden canalizar al cmdlet. El tipo de valor devuelto es el tipo de objeto que el cmdlet devuelve.  
  
|||  
|-|-|  
|Entradas|System.string<br /><br /> Puede canalizar los valores de cadena al cmdlet.|  
|Salidas|Ninguno.|  
  
## <a name="example-1"></a>Ejemplo 1  
  
```  
PS SQLSERVER:\SQLAS\localhost\default> restore-asdatabase awtest.abf testawrestoredb –security:CopyAll  
```  
  
 Este comando restaura un archivo de copia de seguridad de Analysis Services (awtest.abf) en la carpeta de copia de seguridad local a la instancia local predeterminada de Analysis Services. El nombre de la base de datos no tiene que existir; en este caso, el nombre de la base de datos se especifica como parte de la operación de restauración. Al agregar –Security:CopyAll se rellenan los roles y la pertenencia a roles desde la base de datos a la nueva base de datos restaurada.  
  
## <a name="example-2"></a>Ejemplo 2  
  
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
  
## <a name="example-3-remote-scenario"></a>Ejemplo 3 (escenario remoto)  
 En este ejemplo se proporciona una demostración de cómo restaurar un archivo de copia de seguridad local a partir de un recurso compartido de archivos en una instancia remota de Analysis Services. En este ejemplo, se restaura un archivo de copia de seguridad como una base de datos denominada **internetsales** en una instancia predeterminada de Analysis Services, en un equipo llamado **ssas-aw-srv01**.  
  
 El archivo de copia de seguridad se encuentra en un recurso compartido de red, con acceso de lectura público. Es necesario que la instancia remota de Analysis Services tenga permiso de lectura al archivo. La ubicación del archivo tiene que ser un recurso compartido de red (no pueden ser unidades).  
  
 Tenga en cuenta que este ejemplo no depende del proveedor SQLAS. Puede ejecutar el cmdlet como un comando independiente.  
  
```  
PS SQLSERVER:\> restore-asdatabase -restorefile "\\FileServer01\DBFiles\InternetSalesTabular.abf" -name "internetsales  
" -server "SSAS-AW-SRV01"  
```  
  
## <a name="example-4"></a>Ejemplo 4  
  
```  
PS SQLSERVER:\SQLAS\localhost\default> restore-asdatabase –restorefile “\\myremoteserver\backups\testdb.abf” –name Contoso_Retail –server myremoteserver –storagelocation “\\myremoteserver\restoreDBFiles”  
```  
  
 Este comando restaura un archivo de copia de seguridad cifrado de Analysis Services (testdb.abf) en una carpeta de copia de seguridad remota en una instancia predeterminada de Analysis Services remota. El parámetro –StorageLocation se utiliza para colocar los archivos de base de datos en una ubicación que no es la predeterminada, en este caso, un archivo compartido denominado restoreDBfiles.  
  
