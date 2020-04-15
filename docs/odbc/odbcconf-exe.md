---
title: ODBCCONF. EXE ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d771f01d292312f8a0f0060c16e3c348bf2e009e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307536"
---
# <a name="odbcconfexe"></a>ODBCCONF. Exe
ODBCCONF.exe es una herramienta de línea de comandos que le permite configurar controladores ODBC y nombres de origen de datos.  
  
> [!NOTE]  
>  ODBCCONF.exe se quitará en una versión futura de los componentes de acceso a datos de Windows. Evite utilizar esta característica y planee modificar las aplicaciones que actualmente utilizan esta característica. Puede usar comandos de PowerShell para administrar controladores y orígenes de datos. Para obtener más información acerca de estos comandos de PowerShell, vea cmdlets de [componentes](/powershell/module/wdac)de acceso a datos de Windows .  
  
## <a name="syntax"></a>Sintaxis  
  
```console  
ODBCCONF [switches] action  
```  
  
## <a name="arguments"></a>Argumentos  
 *Interruptores*  
 Cero o más opciones de conmutación. Para obtener la lista de modificadores disponibles, consulte la sección Comentarios, más adelante en este tema.  
  
 *action*  
 Una acción a realizar. Para obtener la lista de opciones disponibles, consulte la sección Comentarios.  
  
## <a name="remarks"></a>Observaciones  
 Están disponibles los siguientes conmutadores:  
  
|Switch|Descripción|  
|------------|-----------------|  
|/A -*Acción*?|Especifique una acción.<br /><br /> /A es opcional si solo se especifica una acción.|  
|/?|Mostrar el uso de ODBCCONF. Exe.|  
|/C|El procesamiento continúa si se produce un error en una acción.|  
|/E|Borre el archivo de respuesta especificado con /F cuando finalice el procesamiento.|  
|/F|Utilice un archivo de `odbcconf /F my.rsp`respuesta, como .<br /><br /> my.rsp podría tener este aspecto:`REGSVR c:\my.dll`<br /><br /> /A no se utiliza en un archivo de respuesta.|  
|/H|Uso de la pantalla (Ayuda). Este modificador es el mismo que /?.|  
|/L[ modo ] nombre*de* *archivo* ]|Enviar la salida del programa a un archivo en uno de los tres modos: normal (n), detallado (v) y depuración (d). El modo de depuración registra los archivos DLL cargados por odbcconf.exe.<br /><br /> Si especifica /L sin un modo, el archivo de registro estará vacío.<br /><br /> Por ejemplo, **/Lv log.txt**.|  
|/R|La acción se realizará después de un reinicio.|  
|/S|Modo silencioso. No muestre mensajes de error.|  
  
 Están disponibles las siguientes acciones:  
  
|Acción|Descripción|  
|------------|-----------------|  
|CONFIGDRIVER *driver_name** parámetros de configuración específicos del conductor*|Carga el archivo DLL de instalación del controlador adecuado y llama a la función **ConfigDriver.**<br /><br /> Equivalente a la [función SQLConfigDriver](../odbc/reference/syntax/sqlconfigdriver-function.md).<br /><br /> Por ejemplo:<br /><br /> /A "CONFIGDRIVER " Nombre del controlador" "Pretiempo de "CPTimeout"60"<br /><br /> /A "CONFIGDRIVER " Nombre del controlador" "DriverODBCVer-03.80"|  
|CONFIGDSN *driver_name* el*nombre* DSN &#124; *atributos*|Agrega o modifica un origen de datos del sistema.<br /><br /> Equivalente a la [función SQLConfigDataSource](../odbc/reference/syntax/sqlconfigdatasource-function.md).<br /><br /> Por ejemplo:<br /><br /> /A "SERVIDOR SQL" "DSN-nombre &#124; Servidor-srv"|  
|CONFIGSYSDSN *driver_name* *nombre* DSN &#124; *atributos*|Agrega o modifica un origen de datos del sistema.<br /><br /> Equivalente a la [función SQLConfigDataSource](../odbc/reference/syntax/sqlconfigdatasource-function.md).<br /><br /> Por ejemplo:<br /><br /> /A "SERVIDOR SQL" "DSN-nombre &#124; Servidor-srv"|  
|INSTALLDRIVER|Equivalente a [SQLInstallDriverEx (función).](../odbc/reference/syntax/sqlinstalldriverex-function.md)<br /><br /> Para obtener información sobre la sintaxis de pares palabra clave-valor pasada a INSTALLDRIVER, consulte Subclaves de [especificación](../odbc/reference/install/driver-specification-subkeys.md)de controlador .<br /><br /> Por ejemplo:<br /><br /> /A -INSTALLDRIVER "Su controlador &#124; controlador-c:-su.dll &#124; Setup-c:-su.dll &#124; APILevel-2 &#124; ConnectFunctions-YYY &#124; DriverODBCVer-03.50 &#124; FileUsage-0 &#124; SQLLevel-1"|  
|Configuración *del traductor INSTALLTRANSLATOR**ruta del controlador*|Agrega información acerca de un traductor al **HKEY_LOCAL_MACHINE, SOFTWARE, ODBC, ODBCINST. Clave del Registro INI-ODBC Translators.**<br /><br /> Equivalente a [SQLInstallTranslatorEx (función).](../odbc/reference/syntax/sqlinstalltranslatorex-function.md)<br /><br /> Para obtener información sobre la sintaxis de pares palabra clave-valor pasada a INSTALLDRIVER, consulte Subclaves de [especificación](../odbc/reference/install/translator-specification-subkeys.md)de traductor .<br /><br /> Por ejemplo:<br /><br /> /A -INSTALLTRANSLATOR "Mi traductor &#124; traductor.c:-mi.dll &#124; setup-c:-mi.dll"|  
|REGSVR *dll*|Registra un archivo DLL.<br /><br /> Equivalente a regsvr32.exe.<br /><br /> Por ejemplo:<br /><br /> /A 'REGSVR c:'my.dll'|  
|SETFILEDSNDIR|Cuando HKEY_LOCAL_MACHINE, SOFTWARE, ODBC, ODBC. InI-ODBC File DSN-DefaultDSNDir no existe, la acción SETFILEDSNDIR lo creará y le asignará el valor en HKEY_LOCAL_MACHINE, SOFTWARE, Microsoft, Windows, CurrentVersion, CommonFilesDir, anexado con el archivo de datos.<br /><br /> El valor de HKEY_LOCAL_MACHINE, SOFTWARE, ODBC y ODBC. INI-ODBC Archivo DSN-DefaultDSNDir especifica la ubicación predeterminada utilizada por el Administrador de orígenes de datos ODBC al crear un origen de datos basado en archivos.<br /><br /> Por ejemplo:<br /><br /> /A 'SETFILEDSNDIR'|  
  
## <a name="see-also"></a>Consulte también  
 [Microsoft Open Database Connectivity (ODBC)](../odbc/microsoft-open-database-connectivity-odbc.md)
