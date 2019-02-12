---
title: rsconfig (utilidad) (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- connections [Reporting Services], configuring
- rsconfig utility
- report servers [Reporting Services], connections
- command prompt utilities [Reporting Services]
- command prompt utilities [SQL Server], rsconfig
ms.assetid: 84e45a2f-3ca6-4c16-8259-c15ff49d72ad
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: cebdfdbccf21ca3370cf2670d97d6cea6e4c7836
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56036886"
---
# <a name="rsconfig-utility-ssrs"></a>rsconfig (utilidad) (SSRS)
  La utilidad **rsconfig.exe** cifra y almacena valores de cuenta y conexión en el archivo RSReportServer.config. Los valores cifrados incluyen la información de conexión de la base de datos del servidor de informes y los valores de cuenta utilizados para el procesamiento de informes desatendido.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
      rsconfig {-?}  
{-cconnection}  
{-eunattendedaccount}  
{-mcomputername}  
{-iinstancename}  
{-sservername}  
{-ddatabasename}  
{-aauthmethod}  
{-uusername}  
{-ppassword}  
{-ttrace}  
```  
  
## <a name="arguments"></a>Argumentos  
  
|Término|Opcional/?Requerido|Definición|  
|----------|------------------------|----------------|  
|**-?**|Opcional.|Muestra la sintaxis de los argumentos de Rsconfig.exe.|  
|`-c`|Requerido si no se utiliza el argumento `-e`.|Especifica la cadena de conexión, las credenciales y los valores de origen de datos que se utilizan para conectar un servidor de informes a la base de datos del servidor de informes.<br /><br /> Este argumento no toma ningún valor. No obstante, deben especificarse argumentos adicionales para proporcionar todos los valores de conexión requeridos.<br /><br /> Argumentos que se pueden especificar con `-c` incluyen `-m`, **-s**, `-i`,`-d`,`-a`,`-u`,`-p`, y`-t`.|  
|`-e`|Requerido si no se utiliza el argumento `-c`.|Especifica la cuenta de ejecución desatendida del informe.<br /><br /> Este argumento no toma ningún valor. Sin embargo, deben incluirse argumentos adicionales en la línea de comandos para especificar los valores que están cifrados en el archivo de configuración.<br /><br /> Los argumentos que puede especificar con `-e` son `-u` y `-p`. También puede establecer `-t`.|  
|`-m`  *ComputerName*|Requerido si configura una instancia de servidor de informes remoto.|Especifica el nombre del equipo donde está hospedado el servidor de informes. Si se omite este argumento, el valor predeterminado es `localhost`.|  
|**-s**  *nombreDeServidor*|Requerido.|Especifica la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que hospeda la base de datos del servidor de informes.|  
|`-i`  *nombreDeInstancia*|Requerido si utiliza instancias con nombre.|Si ha utilizado una instancia con nombre de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para hospedar la base de datos del servidor de informes, este valor especifica la instancia con nombre.|  
|`-d`  *databasename*|Requerido.|Especifica el nombre de la base de datos de servidor de informes.|  
|`-a`  *método AuthMethod*|Requerido.|Especifica el método de autenticación que el servidor de informes utiliza para conectarse a la base de datos de servidor de informes. Los valores válidos son `Windows` o `SQL` (este argumento no distingue entre mayúsculas y minúsculas).<br /><br /> `Windows` especifica que el servidor de informes utilice la autenticación de Windows.<br /><br /> `SQL` especifica que el servidor de informes utilice la autenticación de SQL Server.|  
|`-u`  *[dominio\\] nombre de usuario*|Requerido con `-e`. Opcional con `-c`.|Especifica una cuenta de usuario para la conexión de base de datos del servidor de informes o para la cuenta desatendida.<br /><br /> Para **rsconfig -e**, este argumento es obligatorio. Debe ser una cuenta de usuario de dominio.<br /><br /> Para **rsconfig - c** y `-a SQL`, este argumento debe especificar un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inicio de sesión.<br /><br /> Para **rsconfig - c** y `-a Windows`, este argumento puede especificar un usuario de dominio, una cuenta integrada o credenciales de cuenta de servicio. Si especifica una cuenta de dominio, especifique un *dominio* y un *nombre de usuario* en el formato *dominio\nombre de usuario*. Si está utilizando una cuenta integrada, este argumento es opcional. Si desea utilizar las credenciales de la cuenta de servicio, omita este argumento.|  
|`-p`  *Contraseña*|Requerido si se especifica `-u`.|Especifica la contraseña que se utilizará con el argumento *username* . Este argumento se puede establecer en un valor en blanco si la cuenta no requiere una contraseña. Este valor distingue entre mayúsculas y minúsculas para cuentas de dominio.|  
|`-t`|Opcional.|Registra los mensajes de error en el registro de seguimiento. Este argumento no toma ningún valor. Para obtener más información, consulte [Report Server Service Trace Log](../report-server/report-server-service-trace-log.md).|  
  
## <a name="permissions"></a>Permisos  
 Debe ser administrador local del equipo que hospeda el servidor de informes que va a configurar.  
  
## <a name="file-location"></a>Ubicación del archivo  
 Rsconfig.exe se encuentra en **\Archivos de programa\Microsoft SQL Server\110\Tools\Binn**. Puede ejecutar la utilidad desde cualquier carpeta del sistema de archivos.  
  
## <a name="remarks"></a>Comentarios  
 Rsconfig.exe se utiliza con dos objetivos:  
  
-   Modificar la información de conexión que un servidor de informes utiliza para conectar con una base de datos de servidor de informes.  
  
-   Para configurar una cuenta especial que el servidor de informes usa para iniciar sesión en un servidor de bases de datos remoto cuando otras credenciales no están disponibles.  
  
 Puede ejecutar la utilidad**rsconfig** en una instancia local o remota de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. No puede usar la utilidad **rsconfig** para descifrar y ver los valores que ya están establecidos.  
  
 Para ejecutar esta utilidad, es necesario que Instrumental de administración de Windows (WMI) esté instalado en el equipo que va a configurarse.  
  
## <a name="examples"></a>Ejemplos  
 Los siguientes ejemplos muestran algunas formas de usar **rsconfig**.  
  
#### <a name="specifying-a-domain-user-account"></a>Especificar una cuenta de usuario de dominio  
 Este ejemplo muestra cómo configurar un servidor de informes para usar una cuenta de usuario de dominio cuando se conecta a una base de datos del servidor de informes local.  
  
```  
rsconfig -c -s <SQLSERVERNAME> -d reportserver -a Windows -u <MYDOMAIN\MYACCOUNT> -p <PASSWORD>  
```  
  
#### <a name="specifying-a-sql-server-database-user-account"></a>Especificar una cuenta de usuario de base de datos de SQL Server  
 Este ejemplo muestra cómo configurar un servidor de informes para usar el inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para conectar con una base de datos de servidor de informes remota.  
  
```  
rsconfig -c -m <REMOTECOMPUTERNAME> -s <SQLSERVERNAME> -d reportserver -a SQL -u SA -p <SAPASSWORD>  
```  
  
#### <a name="specifying-a-built-in-account"></a>Especificar una cuenta integrada  
 Este ejemplo muestra cómo configurar un servidor de informes para usar una cuenta integrada cuando se conecta a una base de datos de servidor de informes local. Tenga en cuenta que no se utiliza `-u`. Algunos ejemplos de valores de una cuenta integrada compatibles son NT AUTHORITY\SYSTEM para el Sistema local y NT AUTHORITY\NETWORKSERVICE para el Servicio de red (solo[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] ).  
  
```  
rsconfig -c -s <SQLSERVERNAME> -d reportserver -a Windows "NT AUTHORITY\SYSTEM"  
```  
  
#### <a name="specifying-a-service-account"></a>Especificar una cuenta de servicio  
 Este ejemplo muestra cómo configurar un servidor de informes para usar la cuenta de servicio de Windows del Servidor de informes y la cuenta del servicio web cuando se conecte con una base de datos de servidor de informes local. Tenga en cuenta que `-u` no se usa y que no se ha especificado ninguna información de cuenta. Cuando elimine los valores de cuenta del comando, la utilidad **rsconfig** usará la seguridad integrada y la cuenta de servicio en la que se ejecuta cada servicio.  
  
```  
rsconfig -c -s <SQLSERVERNAME> -d reportserver -a Windows  
```  
  
#### <a name="specifying-the-unattended-account-on-a-local-server"></a>Especificar la cuenta de modo desatendido en un servidor local  
 Este ejemplo muestra cómo configurar la cuenta para la ejecución desatendida de informes para informes que no pasan credenciales al origen de datos externo. La cuenta debe ser una cuenta de dominio de Windows. No puede especificar un inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para el nombre de usuario y la contraseña. La cuenta está configurada en una instancia de servidor de informes local. Los mensajes de error se capturan en los registros de seguimiento de la carpeta ReportingServices\LogFiles.  
  
```  
rsconfig -e -u <DOMAIN\ACCOUNT> -p <PASSWORD> -t  
```  
  
#### <a name="specifying-the-unattended-account-on-a-remote-server"></a>Especificar la cuenta de modo desatendido en un servidor remoto  
 En este ejemplo se muestra cómo configurar la cuenta en una instancia de servidor de informes remoto que es de la misma versión que Rsconfig.exe (por ejemplo, el servidor de informes y Rsconfig.exe son de la versión [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 2008 R2). La información de mensaje de error se captura en los registros de seguimiento en el servidor remoto.  
  
```  
rsconfig -e -m <REMOTECOMPUTERNAME> -s <SQLSERVERNAME> -u <DOMAIN\ACCOUNT> -p <PASSWORD> -t  
```  
  
## <a name="see-also"></a>Vea también  
 [Configurar una conexión a la base de datos del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../sql-server/install/configure-a-report-server-database-connection-ssrs-configuration-manager.md)   
 [Configurar la cuenta de ejecución desatendida &#40;Administrador de configuración de SSRS&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md)   
 [Servidor de informes de Reporting Services &#40;modo nativo&#41;](../report-server/reporting-services-report-server-native-mode.md)   
 [Almacenar datos cifrados del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [Archivos de configuración de Reporting Services](../report-server/reporting-services-configuration-files.md)   
 [Utilidades del símbolo del sistema del servidor de informes &#40;SSRS&#41;](report-server-command-prompt-utilities-ssrs.md)   
 [Archivo de configuración RSReportServer](../report-server/rsreportserver-config-configuration-file.md)  
  
  
