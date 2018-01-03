---
title: "Función ConfigDSN | Documentos de Microsoft"
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
apiname: ConfigDSN
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: ConfigDSN
helpviewer_keywords: ConfigDSN [ODBC]
ms.assetid: 01ced74e-c575-4a25-83f5-bd7d918123f8
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b82eb128f125415d3dbdb24ffc616dbeccc5e938
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="configdsn-function"></a>ConfigDSN (función)
**Conformidad**  
 Versión introdujo: ODBC 1.0  
  
 **Resumen**  
 **ConfigDSN** agrega, modifica o elimina los orígenes de datos de la información del sistema. Puede solicitar al usuario información de conexión. Puede estar en la DLL del controlador o un archivo DLL de configuración independiente.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
BOOL ConfigDSN(  
     HWND     hwndParent,  
     WORD     fRequest,  
     LPCSTR   lpszDriver,  
     LPCSTR   lpszAttributes);  
```  
  
## <a name="arguments"></a>Argumentos  
 *hwndParent*  
 [Entrada] Identificador de la ventana primaria. La función no mostrará los cuadros de diálogo si el identificador no es null.  
  
 *fRequest*  
 [Entrada] Tipo de solicitud. El *fRequest* argumento debe contener uno de los siguientes valores:  
  
 ODBC_ADD_DSN: Agregar un nuevo origen de datos.  
  
 ODBC_CONFIG_DSN: Configurar (modificar) un origen de datos existente.  
  
 ODBC_REMOVE_DSN: Quitar un origen de datos existente.  
  
 *lpszDriver*  
 [Entrada] Descripción del controlador (el nombre del DBMS asociado) presentada a los usuarios en lugar del nombre de controlador físico.  
  
 *lpszAttributes*  
 [Entrada] Una lista doblemente terminada en null de atributos en forma de pares de palabra clave y valor. Para obtener más información, vea "Comentarios".  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si se realiza correctamente, FALSE si se produce un error.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **ConfigDSN** devuelve FALSE, un asociado  *\*pfErrorCode* valor se registra en el búfer de error del instalador mediante una llamada a **SQLPostInstallerError** y se puede obtener mediante una llamada a **SQLInstallerError**. La siguiente tabla se recogen los  *\*pfErrorCode* valores que pueden ser devueltos por **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_INVALID_HWND|Identificador de ventana no válido|El *hwndParent* argumento no era válido.|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|Pares palabra clave-valor no válidas|El *lpszAttributes* argumento contiene un error de sintaxis.|  
|ODBC_ERROR_INVALID_NAME|Nombre de traductor o controlador no válido|El *lpszDriver* argumento no era válido. No se encontró en el registro.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitud no válido|El *fRequest* argumento no es uno de los siguientes:<br /><br /> ODBC_ADD_DSN ODBC_CONFIG_DSN ODBC_REMOVE_DSN|  
|ODBC_ERROR_REQUEST_FAILED|*Solicitar* error|No se pudo realizar la operación solicitada por el *fRequest* argumento.|  
|ODBC_ERROR_DRIVER_SPECIFIC|Error específico del controlador o del traductor|Un error específico del controlador para el que no hay ningún error de instalador ODBC definido. El *SzError* argumento en una llamada a la **SQLPostInstallerError** función debe contener el mensaje de error específico del controlador.|  
  
## <a name="comments"></a>Comentarios  
 **ConfigDSN** recibe información de conexión desde el archivo DLL de instalador como una lista de atributos en forma de pares de palabra clave y valor. Cada par se termina con un byte null, y toda la lista se termina con un byte nulo. (Es decir, dos bytes nulos marcan el final de la lista.) No se permiten espacios alrededor del signo igual en el par de palabra clave y valor. **ConfigDSN** puede aceptar palabras clave que no es palabras clave válidas para **SQLBrowseConnect** y **SQLDriverConnect**. **ConfigDSN** no necesariamente no admite todas las palabras clave que son palabras clave válidas para **SQLBrowseConnect** y **SQLDriverConnect**. (**ConfigDSN** no acepta el **controlador** (palabra clave).) Las palabras clave utilizadas por la **ConfigDSN** función debe admitir todas las opciones necesarias para volver a crear el origen de datos mediante la característica de configuración automática del instalador. Cuando los usos de la **ConfigDSN** son los mismos valores y los valores de cadena de conexión, se deben usar las mismas palabras clave.  
  
 ¿Como en **SQLBrowseConnect** y **SQLDriverConnect**, las palabras clave y sus valores no deben contener el **[] {} (),? \*=! @** caracteres y el valor de la **DSN** palabra clave no puede contener solo espacios en blanco. Debido a la gramática del registro, los nombres de origen de datos y palabras clave no pueden contener la barra diagonal inversa (\\) caracteres.  
  
 **ConfigDSN** debe llamar a **SQLValidDSN** para comprobar la longitud del nombre del origen de datos y para comprobar que no hay caracteres no válidos se incluyen en el nombre. Si el nombre de origen de datos es mayor que SQL_MAX_DSN_LENGTH o incluye caracteres no válidos, **SQLValidDSN** devuelve un error y **ConfigDSN** devuelve un error. La longitud del nombre del origen de datos también se comprueba por **SQLWriteDSNToIni**.  
  
 Por ejemplo, para configurar un origen de datos que requiere un Id. de usuario, una contraseña y un nombre de base de datos, una aplicación de instalación podría pasar los siguientes pares de palabra clave y valor:  
  
```  
DSN=Personnel Data\0UID=Smith\0PWD=Sesame\0DATABASE=Personnel\0\0  
```  
  
 Para obtener más información acerca de estas palabras clave, consulte [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) y la documentación de cada controlador.  
  
 Para mostrar un cuadro de diálogo *hwndParent* no debe ser null.  
  
## <a name="adding-a-data-source"></a>Agregar un origen de datos  
 Si se pasa un nombre de origen de datos a **ConfigDSN** en *lpszAttributes*, **ConfigDSN** comprueba que el nombre es válido. Si el nombre de origen de datos coincide con un nombre de origen de datos existente y *hwndParent* es null, **ConfigDSN** sobrescribe el nombre existente. Si coincide con un nombre existente y *hwndParent* no es null, **ConfigDSN** pide al usuario que sobrescriba el nombre existente.  
  
 Si *lpszAttributes* contiene suficiente información para conectarse a un origen de datos, **ConfigDSN** puede agregar origen de datos o mostrar un cuadro de diálogo con el que el usuario puede cambiar la información de conexión. Si *lpszAttributes* no contiene suficiente información para conectarse a un origen de datos, **ConfigDSN** debe determinar la información necesaria; si *hwndParent* no es null, muestra un cuadro de diálogo para recuperar la información del usuario.  
  
 Si **ConfigDSN** muestra un cuadro de diálogo, debe mostrar ninguna información de conexión que se pasa en *lpszAttributes*. En concreto, si se ha pasado un nombre de origen de datos, **ConfigDSN** muestra ese nombre, pero no permite al usuario cambiarlo. **ConfigDSN** puede proporcionar valores predeterminados para la información de conexión no pasado en *lpszAttributes*.  
  
 Si **ConfigDSN** no se puede obtener la información de conexión completa para un origen de datos, devuelve FALSE.  
  
 Si **ConfigDSN** puede obtener información de conexión completa para un origen de datos, llama a **SQLWriteDSNToIni** en el archivo DLL para agregar la nueva especificación de origen de datos en el archivo Odbc.ini (o registro) del programa de instalación. **SQLWriteDSNToIni** agrega el nombre de origen de datos a la sección [orígenes de datos ODBC], la sección de especificación del origen de datos se crea y agrega el **controlador** palabra clave con la descripción del controlador como su valor. **ConfigDSN** llamadas **SQLWritePrivateProfileString** en el archivo DLL para agregar los valores que se utiliza el controlador y palabras clave adicionales del programa de instalación.  
  
## <a name="modifying-a-data-source"></a>Modificar un origen de datos  
 Para modificar un origen de datos, se debe pasar un nombre de origen de datos a **ConfigDSN** en *lpszAttributes*. **ConfigDSN** comprueba que el nombre de origen de datos está en el archivo Odbc.ini (o registro).  
  
 Si *hwndParent* es null, **ConfigDSN** utiliza la información de *lpszAttributes* para modificar la información en el archivo Odbc.ini (o registro). Si *hwndParent* no es null, **ConfigDSN** muestra un cuadro de diálogo con la información de *lpszAttributes*; para obtener información que no está en *lpszAttributes* , usa información de la información del sistema. El usuario puede modificar la información antes de **ConfigDSN** almacena la información del sistema.  
  
 Si se ha cambiado el nombre de origen de datos, **ConfigDSN** llama primero **SQLRemoveDSNFromIni** en el instalador de especificación del archivo Odbc.ini (o registro) del origen de archivo DLL para quitar los datos existentes. A continuación, sigue los pasos descritos en la sección anterior para agregar la nueva especificación de origen de datos. Si no se ha cambiado el nombre de origen de datos, **ConfigDSN** llamadas **SQLWritePrivateProfileString** en el instalador de DLL para realizar otros cambios. **ConfigDSN** no se puede eliminar ni cambiar el valor de la **controlador** palabra clave.  
  
## <a name="deleting-a-data-source"></a>Eliminar un origen de datos  
 Para eliminar un origen de datos, se debe pasar un nombre de origen de datos a **ConfigDSN** en *lpszAttributes*. **ConfigDSN** comprueba que el nombre de origen de datos está en el archivo Odbc.ini (o registro). A continuación, se llama **SQLRemoveDSNFromIni** en el archivo DLL para quitar el origen de datos del instalador.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Agregar, modificar o quitar un origen de datos|[SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md)|  
|Obtener un valor desde el archivo Odbc.ini o el registro|[SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|  
|Quitando el origen de datos predeterminada|[SQLRemoveDefaultDataSource](../../../odbc/reference/syntax/sqlremovedefaultdatasource-function.md)|  
|Quitar un nombre de origen de datos de Odbc.ini (o registro)|[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|  
|Agregar un nombre de origen de datos a Odbc.ini (o registro)|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|  
|Si escribe un valor en el registro o el archivo Odbc.ini|[SQLWritePrivateProfileString](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|
