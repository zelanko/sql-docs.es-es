---
title: "Función SQLInstallDriverEx | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLInstallDriverEx
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLInstallDriverEx
helpviewer_keywords: SQLInstallDriverEx function [ODBC]
ms.assetid: 1dd74544-f4e9-46e1-9b5f-c11d84fdab4c
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4179bf04131f256c5a37cb01c079035a569a07af
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="sqlinstalldriverex-function"></a>SQLInstallDriverEx (función)
**Conformidad**  
 Versión introdujo: ODBC 3.0  
  
 **Resumen**  
 **SQLInstallDriverEx** agrega información sobre el controlador a la entrada de Odbcinst.ini en la información del sistema e incrementa el controlador *UsageCount* en 1. Sin embargo, si una versión de los controladores ya existe pero la *UsageCount* valor para el controlador no existe, la nueva *UsageCount* valor está establecido en 2.  
  
 Esta función no copia los archivos. Es responsabilidad del programa que realiza la llamada para copiar los archivos del controlador en el directorio de destino correctamente.  
  
 La funcionalidad de **SQLInstallDriverEx** también puede tener acceso mediante [ODBCCONF. EXE](../../../odbc/odbcconf-exe.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
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
 [Entrada] Descripción del controlador (el nombre del DBMS asociado) presentada a los usuarios en lugar del nombre de controlador físico. El *lpszDriver* argumento debe contener una lista de pares de palabra clave y valor que describe el controlador doble terminada en null. Para obtener más información sobre los pares palabra clave-valor, vea [controlador especificación subclaves](../../../odbc/reference/install/driver-specification-subkeys.md). Para obtener más información acerca de la cadena terminada en null por partida doble, consulte [ConfigDSN función](../../../odbc/reference/syntax/configdsn-function.md).  
  
 *lpszPathIn*  
 [Entrada] Ruta de acceso completa del directorio de destino de la instalación, o un puntero nulo. Si *lpszPathIn* es un puntero nulo, los controladores se instalarán en el directorio del sistema.  
  
 *lpszPathOut*  
 [Salida] Ruta de acceso del directorio de destino donde se debe instalar el controlador. Si el controlador no se ha instalado previamente, *lpszPathOut* debe ser el mismo que *lpszPathIn*. Si el controlador se instaló previamente, *lpszPathOut* es la ruta de acceso de la instalación anterior.  
  
 *cbPathOutMax*  
 [Entrada] Longitud de *lpszPathOut*.  
  
 *pcbPathOut*  
 [Salida] Número total de bytes (sin incluir el carácter de terminación null) disponible para devolver en *lpszPathOut*. Si el número de bytes disponible para devolver es mayor o igual que *cbPathOutMax*, la ruta de acceso de salida en *lpszPathOut* se trunca a *cbPathOutMax* menos el carácter de terminación NULL. El *pcbPathOut* argumento puede ser un puntero nulo.  
  
 *fRequest*  
 [Entrada] Tipo de solicitud. El *fRequest* argumento debe contener uno de los siguientes valores:  
  
 ODBC_INSTALL_INQUIRY: Realizar consultas sobre donde se puede instalar un controlador.  
  
 ODBC_INSTALL_COMPLETE: Completar la solicitud de instalación.  
  
 *lpdwUsageCount*  
 [Salida] El contador de uso del controlador después de llamar a esta función.  
  
 Las aplicaciones no deben establecer el recuento de uso. ODBC mantendrá este número.  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si se realiza correctamente, FALSE si se produce un error.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLInstallDriverEx** devuelve FALSE, un asociado  *\*pfErrorCode* valor puede obtenerse mediante una llamada a **SQLInstallerError**. La siguiente tabla se recogen los  *\*pfErrorCode* valores que pueden ser devueltos por **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Error del instalador general|Se produjo un error para que no se produjo ningún error de instalación concreto.|  
|ODBC_ERROR_INVALID_BUFF_LEN|Longitud de búfer no válido|El *lpszPathOut* argumento no era lo suficientemente grande como para contener la ruta de acceso de salida. El búfer contiene la ruta de acceso truncado.<br /><br /> El *cbPathOutMax* argumento era 0, y *fRequest* era ODBC_INSTALL_COMPLETE.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitud no válido|El *fRequest* argumento no es uno de los siguientes:<br /><br /> ODBC_INSTALL_INQUIRY ODBC_INSTALL_COMPLETE|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|Pares palabra clave-valor no válidas|El *lpszDriver* argumento contiene un error de sintaxis.|  
|ODBC_ERROR_INVALID_PATH|Ruta de acceso de instalación no válida|El *lpszPathIn* argumento contiene una ruta de acceso no válido.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|No se pudo cargar la biblioteca de instalación de controlador o traductor|No se pudo cargar la biblioteca de instalación de controladores.|  
|ODBC_ERROR_INVALID_PARAM_SEQUENCE|Secuencia de parámetros no válidos|El *lpszDriver* argumento no contiene una lista de pares de palabra clave y valor.|  
|ODBC_ERROR_USAGE_UPDATE_FAILED|No se pudo incrementar o disminuir el recuento de uso de componente|El instalador no pudo incrementar el contador de uso del controlador.|  
  
## <a name="comments"></a>Comentarios  
 El *lpszDriver* argumento es una lista de atributos en forma de pares de palabra clave y valor. Cada par se termina con un byte null, y toda la lista se termina con un byte nulo. (Es decir, dos bytes nulos marcan el final de la lista.) El formato de esta lista es como sigue:  
  
 *controlador desc*  **\\** 0Driver**=***nombre del controlador de archivo DLL*  **\\** 0 [el programa de instalación**=***nombre del programa de instalación de archivo DLL***\\**0]  
  
 [*controlador-attr-palabraclave1***=***value1***\\**0] [*controlador-attr-palabraclave2*   **=**  *value2***\\**0]...  **\\** 0  
  
 donde \0 es un byte nulo y *controlador-attr-keywordn* es cualquier palabra clave de atributo de controlador. Las palabras clave deben aparecer en el orden especificado. Por ejemplo, imagine que un controlador de archivos de texto con formato tiene controlador independiente y el programa de instalación de archivos DLL y puede utilizar archivos con las extensiones .txt y .csv. El *lpszDriver* argumento para este controlador podría ser el siguiente:  
  
```  
Text\0Driver=TEXT.DLL\0Setup=TXTSETUP.DLL\0FileUsage=1\0  
FileExtns=*.txt,*.csv\0\0  
```  
  
 Suponga que un controlador de SQL Server no tiene un archivo DLL de configuración independiente y no tiene las palabras clave de atributo de controlador. El *lpszDriver* argumento para este controlador podría ser el siguiente:  
  
```  
SQL Server\0Driver=SQLSRVR.DLL\0\0  
```  
  
 Después de **SQLInstallDriverEx** recupera información sobre el controlador de la *lpszDriver* argumento, agrega la descripción del controlador a la sección [ODBC Drivers] de la entrada de Odbcinst.ini en el sistema información. A continuación, crea una sección con la descripción del controlador y agrega las rutas de acceso completas de la DLL del controlador y el archivo DLL de configuración. Por último, devuelve la ruta de acceso del directorio de destino de la instalación, pero no copia los archivos de controlador a él. El programa de llamada realmente debe copiar los archivos del controlador en el directorio de destino.  
  
 **SQLInstallDriverEx** incrementa en 1 el recuento de uso de componente con el controlador instalado. Si ya existe una versión del controlador, pero el contador de uso de componente para el controlador no existe, el nuevo valor de recuento de uso del componente se establece en 2.  
  
 El programa de instalación de la aplicación es responsable de la copia físicamente el archivo del controlador y el mantenimiento el contador de uso de archivo. Si el archivo del controlador no se ha instalado previamente, el programa de instalación de la aplicación debe copiar el archivo en el *lpszPathIn* ruta de acceso y crear el contador de uso de archivo. Si el archivo se ha instalado previamente, el programa de instalación simplemente incrementa el recuento de uso de archivo y devuelve la ruta de acceso de la instalación anterior en el *lpszPathOut* argumento.  
  
> [!NOTE]  
>  Para obtener más información sobre recuentos de uso de componentes y los recuentos de uso de archivo, consulte [recuento de uso](../../../odbc/reference/install/usage-counting.md).  
  
 Si la aplicación se instaló anteriormente una versión anterior del archivo del controlador, el controlador se debe desinstalar y, a continuación, reinstalar, por lo que el contador de uso del componente de controlador es válido. **SQLConfigDriver** (con un *referien* de ODBC_REMOVE_DRIVER) debe llamarse en primer lugar y, a continuación, **SQLRemoveDriver** debe llamarse para disminuir el recuento de uso del componente. **SQLInstallDriverEx** , a continuación, se debe llamar para reinstalar el controlador, incrementar el contador de uso del componente. El programa de instalación de la aplicación debe reemplazar el archivo antiguo con el nuevo archivo. El contador de uso de archivo seguirá siendo el mismo, y cualquier otra aplicación que utiliza el archivo de la versión anterior ahora usará la versión más reciente.  
  
> [!NOTE]  
>  Si el controlador se instaló previamente y **SQLInstallDriverEx** se llama para instalar el controlador en un directorio diferente, la función devuelve TRUE, pero *lpszPathOut* incluirá el directorio donde ya se ha instalado el controlador. No se incluyen el directorio especificado en el *lpszDriver* argumento.  
  
 La longitud de la ruta de acceso en *lpszPathOut* en **SQLInstallDriverEx** permite para un proceso de instalación en dos fases, por lo que una aplicación puede determinar qué *cbPathOutMax* debe ser al llamar a **SQLInstallDriverEx** con una *fRequest* del modo ODBC_INSTALL_INQUIRY. Esto devolverá el número total de bytes disponible en la *pcbPathOut* búfer. **SQLInstallDriverEx** , a continuación, se puede llamar con un *fRequest* de ODBC_INSTALL_COMPLETE y *cbPathOutMax* establecido en el valor de la *pcbPathOut*búfer más el carácter de terminación null.  
  
 Si decide no utilizar el modelo en dos fases para **SQLInstallDriverEx**, debe establecer *cbPathOutMax*, que define el tamaño del almacenamiento para la ruta de acceso del directorio de destino, que el valor _MAX_PATH, como se definen en Stdlib.h, para evitar el truncamiento.  
  
 Cuando *referien* es ODBC_INSTALL_COMPLETE, **SQLInstallDriverEx** no permite *lpszPathOut* null (o *cbPathOutMax* como 0). Si *referien* es ODBC_INSTALL_COMPLETE, se devuelve FALSE cuando el número de bytes disponible para devolver es mayor o igual que *cbPathOutMax*, con lo que el truncamiento se produce.  
  
 Después de **SQLInstallDriverEx** se ha llamado y el programa de instalación de la aplicación ha copiado el archivo del controlador (si es necesario), el programa de instalación de controlador debe llamar DLL **SQLConfigDriver** para establecer la configuración de la controlador.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Instalación del Administrador de controladores|[SQLInstallDriverManager](../../../odbc/reference/syntax/sqlinstalldrivermanager-function.md)|
