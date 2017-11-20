---
title: ODBCCONF. EXE | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- odbcconf.exe
ms.assetid: 3bf2be83-61f9-4183-836b-85204ac7116a
caps.latest.revision: 23
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: db8ff09a2b77f51c97ab73d6d994e1e1b4dce2a1
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="odbcconfexe"></a>ODBCCONF. EXE
ODBCCONF.exe es una herramienta de línea de comandos que le permite configurar los nombres de orígenes de datos y controladores ODBC.  
  
> [!NOTE]  
>  ODBCCONF.exe se quitará en una versión futura de Windows Data Access Components. Evite utilizar esta característica y piense en modificar las aplicaciones que actualmente utilizan esta característica. Puede usar comandos de PowerShell para administrar controladores y orígenes de datos. Para obtener más información acerca de estos comandos de PowerShell, consulte [cmdlets de Windows Data Access Components](https://technet.microsoft.com/library/hh771019.aspx).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
ODBCCONF [switches] action  
```  
  
## <a name="arguments"></a>Argumentos  
 *modificadores*  
 Cero o más opciones de conmutador. Para obtener la lista de modificadores disponibles, vea la sección Comentarios, más adelante en este tema.  
  
 *acción*  
 Una acción que se va a realizar. Para obtener la lista de opciones disponibles, vea la sección Comentarios.  
  
## <a name="remarks"></a>Comentarios  
 Están disponibles los siguientes modificadores:  
  
|Switch|Description|  
|------------|-----------------|  
|/A {*acción*}|Especificar una acción.<br /><br /> /A es opcional si sólo se especifica una acción.|  
|/?|Muestra el uso de ODBCCONF. EXE.|  
|/C|El procesamiento continúa si se produce un error en una acción.|  
|/E|Borrar el archivo de respuesta especificado con /F cuando finalice el procesamiento.|  
|/F|Usar un archivo de respuesta, como `odbcconf /F my.rsp`.<br /><br /> My.rsp podría ser similar al siguiente:`REGSVR c:\my.dll`<br /><br /> /A no se utiliza en un archivo de respuesta.|  
|/H|Muestra el uso (Ayuda). Este modificador es igual que /?.|  
|/ L [*modo*] *nombre de archivo*|Enviar la salida del programa a un archivo en uno de los tres modos: normal (n), detallado (v) y depuración (d). Depurar el modo registra los archivos DLL que se cargan mediante odbcconf.exe.<br /><br /> Si se especifica/l sin un modo, el archivo de registro estará vacío.<br /><br /> Por ejemplo, **/Lv log.txt**.|  
|/R|Se realizará la acción tras un reinicio.|  
|/S|Modo silencioso. No se muestran mensajes de error.|  
  
 Están disponibles las siguientes acciones:  
  
|Acción|Description|  
|------------|-----------------|  
|CONFIGDRIVER *nombreDeControlador**parámetros de configuración específicos del controlador*|Carga el archivo DLL de configuración de controlador adecuado y llama el **ConfigDriver** función.<br /><br /> Equivalente a la [SQLConfigDriver función](../odbc/reference/syntax/sqlconfigdriver-function.md).<br /><br /> Por ejemplo:<br /><br /> /A {CONFIGDRIVER "Nombre de controlador" "CPTimeout = 60"}<br /><br /> /A {CONFIGDRIVER "Nombre de controlador" "DriverODBCVer = 03.80"}|  
|CONFIGDSN *nombreDeControlador* DSN =*nombre* &#124; *atributos*|Agrega o modifica un origen de datos del sistema.<br /><br /> Equivalente a la [SQLConfigDataSource, función](../odbc/reference/syntax/sqlconfigdatasource-function.md).<br /><br /> Por ejemplo:<br /><br /> /A {CONFIGDSN "SQL Server" "DSN = nombre &#124; Server = srv "}|  
|CONFIGSYSDSN *nombreDeControlador* DSN =*nombre* &#124; *atributos*|Agrega o modifica un origen de datos del sistema.<br /><br /> Equivalente a la [SQLConfigDataSource, función](../odbc/reference/syntax/sqlconfigdatasource-function.md).<br /><br /> Por ejemplo:<br /><br /> /A {CONFIGSYSDSN "SQL Server" "DSN = nombre &#124; Server = srv "}|  
|INSTALLDRIVER|Equivalente a [SQLInstallDriverEx función](../odbc/reference/syntax/sqlinstalldriverex-function.md).<br /><br /> Para obtener información acerca de la sintaxis de pares de palabra clave y valor pasada a INSTALLDRIVER, consulte [controlador especificación subclaves](../odbc/reference/install/driver-specification-subkeys.md).<br /><br /> Por ejemplo:<br /><br /> /A {INSTALLDRIVER "el controlador &#124; Driver=c:\Your.dll &#124; Setup=c:\Your.dll &#124; APILevel = 2 &#124; ConnectFunctions = YYY &#124; DriverODBCVer = 03.50 &#124; FileUsage = 0 &#124; SQLLevel = 1"}|  
|INSTALLTRANSLATOR *configuración traductor**ruta de acceso*|Agrega información sobre un traductor para el **HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBCINST. INI\ODBC traductores** clave del registro.<br /><br /> Equivalente a [SQLInstallTranslatorEx función](../odbc/reference/syntax/sqlinstalltranslatorex-function.md).<br /><br /> Para obtener información acerca de la sintaxis de pares de palabra clave y valor pasada a INSTALLDRIVER, consulte [subclaves de la especificación de traductor](../odbc/reference/install/translator-specification-subkeys.md).<br /><br /> Por ejemplo:<br /><br /> /A {INSTALLTRANSLATOR "Mi traductor &#124; Translator=c:\My.dll &#124; Setup=c:\My.dll"}|  
|REGSVR *dll*|Registra un archivo DLL.<br /><br /> Equivalente a regsvr32.exe.<br /><br /> Por ejemplo:<br /><br /> /A {REGSVR c:\my.dll}|  
|SETFILEDSNDIR|Cuando HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC. INI\ODBC archivo DSN\DefaultDSNDir no existe, la acción de SETFILEDSNDIR se crea y asigna el valor en HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\CommonFilesDir, le anexa \ODBC\Data orígenes.<br /><br /> El valor en HKEY_LOCAL_MACHINE\SOFTWARE\ODBC\ODBC. INI\ODBC archivo DSN\DefaultDSNDir especifica la ubicación de predeterminada utilizada por el Administrador de orígenes de datos de ODBC cuando se crea un origen de datos basados en archivos.<br /><br /> Por ejemplo:<br /><br /> /A {SETFILEDSNDIR}|  
  
## <a name="see-also"></a>Vea también  
 [Microsoft Open Database Connectivity (ODBC)](../odbc/microsoft-open-database-connectivity-odbc.md)

