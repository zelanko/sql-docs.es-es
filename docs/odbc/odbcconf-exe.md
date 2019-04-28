---
title: ODBCCONF.EXE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- odbcconf.exe
ms.assetid: 3bf2be83-61f9-4183-836b-85204ac7116a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 33688a46be5e5e33aa940f3553c98db5091b159d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62677372"
---
# <a name="odbcconfexe"></a>ODBCCONF.EXE
ODBCCONF.exe es una herramienta de línea de comandos que le permite configurar los nombres de orígenes de datos y los controladores ODBC.  
  
> [!NOTE]  
>  ODBCCONF.exe se quitará en una versión futura de Windows Data Access Components. Evite utilizar esta característica y piense en modificar las aplicaciones que actualmente utilizan esta característica. Puede usar los comandos de PowerShell para administrar los controladores y orígenes de datos. Para obtener más información acerca de estos comandos de PowerShell, consulte [cmdlets de Windows Data Access Components](https://technet.microsoft.com/library/hh771019.aspx).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
ODBCCONF [switches] action  
```  
  
## <a name="arguments"></a>Argumentos  
 *switches*  
 Cero o más opciones de conmutador. Para obtener la lista de modificadores disponibles, vea la sección de comentarios, más adelante en este tema.  
  
 *action*  
 Una acción que se va a realizar. Para obtener la lista de opciones disponibles, vea la sección Comentarios.  
  
## <a name="remarks"></a>Comentarios  
 Están disponibles los siguientes modificadores:  
  
|Modificador|Descripción|  
|------------|-----------------|  
|/A {*acción*}|Especificar una acción.<br /><br /> /A es opcional si solo se especifica una acción.|  
|/?|Muestra el uso de ODBCCONF. EXE.|  
|/C|El procesamiento continúa si se produce un error en una acción.|  
|/E|Borrar el archivo de respuesta especificado con /F cuando haya terminado el procesamiento.|  
|/F|Usar un archivo de respuesta, como `odbcconf /F my.rsp`.<br /><br /> My.rsp podría parecerse a esto: `REGSVR c:\my.dll`<br /><br /> /A no se utiliza en un archivo de respuesta.|  
|/H|Mostrar uso (Ayuda). Este modificador es igual que /?.|  
|/L[*mode*] *filename*|Enviar la salida del programa a un archivo en uno de tres modos: normal (n), detallado (v) y depuración (d). Depurar registros modo los archivos DLL que se cargan mediante odbcconf.exe.<br /><br /> Si especifica/l sin modo, el archivo de registro estará vacío.<br /><br /> Por ejemplo, **/Lv log.txt**.|  
|/R|La acción se realizará tras un reinicio.|  
|/S|Modo silencioso. No se muestran mensajes de error.|  
  
 Están disponibles las siguientes acciones:  
  
|Acción|Descripción|  
|------------|-----------------|  
|CONFIGDRIVER *nombreDeControlador ** parámetros de configuración específicos del controlador*|Carga la DLL de instalación de controlador adecuado y llama a la **ConfigDriver** función.<br /><br /> Equivalente a la [función SQLConfigDriver](../odbc/reference/syntax/sqlconfigdriver-function.md).<br /><br /> Por ejemplo:<br /><br /> /A {CONFIGDRIVER "Nombre de controlador" "CPTimeout = 60"}<br /><br /> /A {CONFIGDRIVER "Nombre de controlador" "DriverODBCVer = 03.80"}|  
|CONFIGDSN *nombreDeControlador* DSN =*nombre* &#124; *atributos*|Agrega o modifica un origen de datos del sistema.<br /><br /> Equivalente a la [función SQLConfigDataSource](../odbc/reference/syntax/sqlconfigdatasource-function.md).<br /><br /> Por ejemplo:<br /><br /> /A {CONFIGDSN "SQL Server" "DSN=name &#124; Server=srv"}|  
|CONFIGSYSDSN *nombreDeControlador* DSN =*nombre* &#124; *atributos*|Agrega o modifica un origen de datos del sistema.<br /><br /> Equivalente a la [función SQLConfigDataSource](../odbc/reference/syntax/sqlconfigdatasource-function.md).<br /><br /> Por ejemplo:<br /><br /> /A {CONFIGSYSDSN "SQL Server" "DSN=name &#124; Server=srv"}|  
|/INSTALLDRIVER|Equivalente a [función SQLInstallDriverEx](../odbc/reference/syntax/sqlinstalldriverex-function.md).<br /><br /> Para obtener información sobre la sintaxis de pares de palabra clave y valor pasada a /INSTALLDRIVER, consulte [subclaves de la especificación de controlador](../odbc/reference/install/driver-specification-subkeys.md).<br /><br /> Por ejemplo:<br /><br /> /A {INSTALLDRIVER  "Your Driver &#124; Driver=c:\your.dll &#124; Setup=c:\your.dll &#124; APILevel=2 &#124; ConnectFunctions=YYY &#124; DriverODBCVer=03.50 &#124; FileUsage=0 &#124; SQLLevel=1"}|  
|INSTALLTRANSLATOR *configuración traductor ** ruta de controlador*|Agrega información sobre un traductor para el **HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST. INI\ODBC traductores** clave del registro.<br /><br /> Equivalente a [función SQLInstallTranslatorEx](../odbc/reference/syntax/sqlinstalltranslatorex-function.md).<br /><br /> Para obtener información sobre la sintaxis de pares de palabra clave y valor pasada a /INSTALLDRIVER, consulte [subclaves de la especificación de traductor](../odbc/reference/install/translator-specification-subkeys.md).<br /><br /> Por ejemplo:<br /><br /> /A {INSTALLTRANSLATOR  "My Translator &#124; Translator=c:\my.dll &#124; Setup=c:\my.dll"}|  
|REGSVR *dll*|Registra un archivo DLL.<br /><br /> Equivalente a regsvr32.exe.<br /><br /> Por ejemplo:<br /><br /> /A {REGSVR c:\my.dll}|  
|SETFILEDSNDIR|Cuando HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC. INI\ODBC DSN\DefaultDSNDir de archivo no existe, la acción SETFILEDSNDIR crearlo y asígnele el valor en HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\CommonFilesDir, anexada \ODBC\Data orígenes.<br /><br /> El valor en HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC. INI\ODBC archivo DSN\DefaultDSNDir especifica la ubicación predeterminado utilizada por el Administrador de orígenes de datos ODBC cuando se crea un origen de datos basados en archivos.<br /><br /> Por ejemplo:<br /><br /> /A {SETFILEDSNDIR}|  
  
## <a name="see-also"></a>Vea también  
 [Microsoft Open Database Connectivity (ODBC)](../odbc/microsoft-open-database-connectivity-odbc.md)
