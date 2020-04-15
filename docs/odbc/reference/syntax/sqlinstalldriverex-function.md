---
title: Función SQLInstallDriverEx ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLInstallDriverEx
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLInstallDriverEx
helpviewer_keywords:
- SQLInstallDriverEx function [ODBC]
ms.assetid: 1dd74544-f4e9-46e1-9b5f-c11d84fdab4c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 054e8b6b9eae26bd5f973f3d46d7ef37363a8e79
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302127"
---
# <a name="sqlinstalldriverex-function"></a>Función SQLInstallDriverEx
**Conformidad**  
 Versión introducida: ODBC 3.0  
  
 **Resumen**  
 **SQLInstallDriverEx** agrega información sobre el controlador a la entrada Odbcinst.ini en la información del sistema e incrementa *usageCount* del controlador en 1. Sin embargo, si ya existe una versión del controlador pero el valor *UsageCount* para el controlador no existe, el nuevo valor *UsageCount* se establece en 2.  
  
 Esta función no copia realmente ningún archivo. Es responsabilidad del programa que realiza la llamada copiar los archivos del controlador en el directorio de destino correctamente.  
  
 También se puede tener acceso a la funcionalidad de **SQLInstallDriverEx** con [ODBCCONF. EXE](../../../odbc/odbcconf-exe.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
BOOL SQLInstallDriverEx(  
     LPCSTR    lpszDriver,  
     LPCSTR    lpszPathIn,  
     LPSTR     lpszPathOut,  
     WORD      cbPathOutMax,  
     WORD *    pcbPathOut,  
     WORD      fRequest,  
     LPDWORD   lpdwUsageCount);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszDriver*  
 [Entrada] La descripción del controlador (normalmente el nombre del DBMS asociado) se presenta a los usuarios en lugar del nombre del controlador físico. El argumento *lpszDriver* debe contener una lista doblemente terminada en null de pares palabra clave-valor que describen el controlador. Para obtener más información acerca de los pares palabra clave-valor, vea Subclaves de [especificación de controlador](../../../odbc/reference/install/driver-specification-subkeys.md). Para obtener más información acerca de la cadena con terminación doble de null, vea [Función ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md).  
  
 *lpszPathIn*  
 [Entrada] Ruta de acceso completa del directorio de destino de la instalación o un puntero nulo. Si *lpszPathIn* es un puntero nulo, los controladores se instalarán en el directorio del sistema.  
  
 *lpszPathOut*  
 [Salida] Ruta de acceso del directorio de destino donde se debe instalar el controlador. Si el controlador no se ha instalado previamente, *lpszPathOut* debe ser el mismo que *lpszPathIn*. Si el controlador se instaló anteriormente, *lpszPathOut* es la ruta de acceso de la instalación anterior.  
  
 *cbPathOutMax*  
 [Entrada] Longitud de *lpszPathOut*.  
  
 *pcbPathOut*  
 [Salida] Número total de bytes (excluyendo el carácter de terminación nula) disponibles para devolver en *lpszPathOut*. Si el número de bytes disponibles para devolver es mayor o igual que *cbPathOutMax*, la ruta de acceso de salida en *lpszPathOut* se trunca a *cbPathOutMax* menos el carácter de terminación null. El argumento *pcbPathOut* puede ser un puntero nulo.  
  
 *fRequest*  
 [Entrada] Tipo de solicitud. El argumento *fRequest* debe contener uno de los siguientes valores:  
  
 ODBC_INSTALL_INQUIRY: Pregunte dónde se puede instalar un controlador.  
  
 ODBC_INSTALL_COMPLETE: Complete la solicitud de instalación.  
  
 *lpdwUsageCount*  
 [Salida] El recuento de uso del controlador después de llamar a esta función.  
  
 Las aplicaciones no deben establecer el recuento de uso. ODBC mantendrá este recuento.  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si se realiza correctamente, FALSE si se produce un error.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLInstallDriverEx** devuelve FALSE, se puede obtener un valor * \*pfErrorCode* asociado llamando a **SQLInstallerError**. En la tabla * \** siguiente se enumeran los valores pfErrorCode que puede devolver **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Descripción|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Error general del instalador|Se ha producido un error para el que no se ha producido ningún error específico del instalador.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Longitud de búfer no válida|El argumento *lpszPathOut* no era lo suficientemente grande como para contener la ruta de acceso de salida. El búfer contiene la ruta truncada.<br /><br /> El argumento *cbPathOutMax* era 0 y *fRequest* se ODBC_INSTALL_COMPLETE.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitud no válido|El argumento *fRequest* no era uno de los siguientes:<br /><br /> ODBC_INSTALL_INQUIRY ODBC_INSTALL_COMPLETE|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|Pares palabra clave-valor no válidos|El argumento *lpszDriver* contenía un error de sintaxis.|  
|ODBC_ERROR_INVALID_PATH|Ruta de instalación no válida|El argumento *lpszPathIn* contenía una ruta de acceso no válida.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|No se pudo cargar la biblioteca de configuración del controlador o traductor|No se ha podido cargar la biblioteca de configuración del controlador.|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|Secuencia de parámetros no válida|El argumento *lpszDriver* no contenía una lista de pares palabra clave-valor.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|No se pudo incrementar o disminuir el recuento de uso de componentes|El instalador no pudo incrementar el número de uso del controlador.|  
  
## <a name="comments"></a>Comentarios  
 El argumento *lpszDriver* es una lista de atributos en forma de pares palabra clave-valor. Cada par se termina con un byte nulo y toda la lista se termina con un byte nulo. (Es decir, dos bytes nulos marcan el final de la lista.) El formato de esta lista es el siguiente:  
  
 _driver-desc_ **\\**0Driver**=**_driver-DLL-filename_**\\****=** 0[Setup_setup-DLL-filename_<b>\\</b>0]  
  
 [_driver-attr-keyword1_**=**_value1_<b>\\</b>0] [_driver-attr-keyword2_**=**_value2_<b>\\</b>0]... <b>\\</b>0  
  
 donde el valor 0 es un byte nulo y *driver-attr-keywordn* es cualquier palabra clave de atributo de controlador. Las palabras clave deben aparecer en el orden especificado. Por ejemplo, supongamos que un controlador para archivos de texto con formato tiene archivos DLL de configuración y controlador independientes y puede usar archivos con las extensiones .txt y .csv. El argumento *lpszDriver* para este controlador podría ser el siguiente:  
  
```  
Text\0Driver=TEXT.DLL\0Setup=TXTSETUP.DLL\0FileUsage=1\0  
FileExtns=*.txt,*.csv\0\0  
```  
  
 Supongamos que un controlador para SQL ServerSQL Server no tiene un archivo DLL de instalación independiente y no tiene ninguna palabra clave de atributo de controlador. El argumento *lpszDriver* para este controlador podría ser el siguiente:  
  
```  
SQL Server\0Driver=SQLSRVR.DLL\0\0  
```  
  
 Después de **SQLInstallDriverEx** recupera información sobre el controlador desde el *lpszDriver* argumento, agrega la descripción del controlador a la [ODBC Drivers] sección de la Odbcinst.ini entrada en la información del sistema. A continuación, crea una sección titulada con la descripción del controlador y agrega las rutas de acceso completas del archivo DLL del controlador y el archivo DLL de instalación. Por último, devuelve la ruta de acceso del directorio de destino de la instalación, pero no copia los archivos de controlador en él. El programa que realiza la llamada debe copiar los archivos de controlador en el directorio de destino.  
  
 **SQLInstallDriverEx** incrementa el recuento de uso de componentes para el controlador instalado en 1. Si ya existe una versión del controlador pero el recuento de uso de componentes para el controlador no existe, el nuevo valor de recuento de uso de componentes se establece en 2.  
  
 El programa de instalación de la aplicación es responsable de copiar físicamente el archivo de controlador y mantener el recuento de uso del archivo. Si el archivo de controlador no se ha instalado previamente, el programa de instalación de la aplicación debe copiar el archivo en la ruta de acceso *lpszPathIn* y crear el recuento de uso del archivo. Si el archivo se ha instalado previamente, el programa de instalación simplemente incrementa el recuento de uso de archivos y devuelve la ruta de acceso de la instalación anterior en el argumento *lpszPathOut.*  
  
> [!NOTE]  
>  Para obtener más información sobre los recuentos de uso de componentes y los recuentos de uso de archivos, consulte [Recuento de](../../../odbc/reference/install/usage-counting.md)uso .  
  
 Si la aplicación instaló previamente una versión anterior del archivo de controlador, el controlador debe desinstalarse y, a continuación, volver a instalarlo, de modo que el recuento de uso del componente del controlador sea válido. **SQLConfigDriver** (con un *fRequest* de ODBC_REMOVE_DRIVER) primero debe llamarse y, a continuación, **SQLRemoveDriver** debe llamarse para disminuir el recuento de uso de componentes. **SQLInstallDriverEx,** a continuación, debe llamarse para reinstalar el controlador, incrementando el recuento de uso de componentes. El programa de instalación de la aplicación debe reemplazar el archivo antiguo con el nuevo archivo. El recuento de uso de archivos seguirá siendo el mismo, y cualquier otra aplicación que haya utilizado el archivo de versión anterior ahora usará la versión más reciente.  
  
> [!NOTE]  
>  Si el controlador se instaló previamente y **SQLInstallDriverEx** se llama para instalar el controlador en un directorio diferente, la función devolverá TRUE, pero *lpszPathOut* incluirá el directorio donde el controlador ya estaba instalado. No incluirá el directorio especificado en el argumento *lpszDriver.*  
  
 La longitud de la ruta de acceso en *lpszPathOut* en **SQLInstallDriverEx** permite un proceso de instalación en dos fases, por lo que una aplicación puede determinar qué debe ser *cbPathOutMax* llamando a **SQLInstallDriverEx** con un *fRequest* de modo ODBC_INSTALL_INQUIRY. Esto devolverá el número total de bytes disponibles en el búfer *pcbPathOut.* **SQLInstallDriverEx,** a continuación, se puede llamar con un *fRequest* de ODBC_INSTALL_COMPLETE y el *cbPathOutMax* argumento establecido en el valor en el *búfer pcbPathOut,* más el carácter de terminación null.  
  
 Si decide no utilizar el modelo de dos fases para **SQLInstallDriverEx**, debe establecer *cbPathOutMax*, que define el tamaño del almacenamiento para la ruta de acceso del directorio de destino, en el valor _MAX_PATH, tal como se define en Stdlib.h, para evitar el truncamiento.  
  
 Cuando *fRequest* se ODBC_INSTALL_COMPLETE, **SQLInstallDriverEx** no permite que *lpszPathOut* sea NULL (o *cbPathOutMax* sea 0). Si *fRequest* es ODBC_INSTALL_COMPLETE, FALSE se devuelve cuando el número de bytes disponibles para devolver es mayor o igual que *cbPathOutMax*, con el resultado de que se produce el truncamiento.  
  
 Después de **SQLInstallDriverEx** se ha llamado y el programa de instalación de la aplicación ha copiado el archivo de controlador (si es necesario), el archivo DLL de instalación del controlador debe llamar a **SQLConfigDriver** para establecer la configuración del controlador.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Instalación del Administrador de controladores|[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|
