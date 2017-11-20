---
title: "Función SQLConfigDataSource | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLConfigDataSource
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLConfigDataSource
helpviewer_keywords:
- SQLConfigDataSource function [ODBC]
ms.assetid: f8d6e342-c010-434e-b1cd-f5371fb50a14
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1d1fddaf67cfbdb8f8c8df7e66b86a681ca2e23d
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlconfigdatasource-function"></a>SQLConfigDataSource Function
**Conformidad**  
 Versión introdujo: ODBC 1.0  
  
 **Resumen**  
 **SQLConfigDataSource** agrega, modifica o elimina los orígenes de datos.  
  
 La funcionalidad de **SQLConfigDataSource** también puede tener acceso mediante [ODBCCONF. EXE](../../../odbc/odbcconf-exe.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
BOOL SQLConfigDataSource(  
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
  
 ODBC_ADD_DSN: Agregar un nuevo origen de datos de usuario.  
  
 ODBC_CONFIG_DSN: Configurar (modificar) un origen de datos de usuario existente.  
  
 ODBC_REMOVE_DSN: Quitar un origen de datos de usuario existente.  
  
 ODBC_ADD_SYS_DSN: Agregar un nuevo origen de datos de sistema.  
  
 ODBC_CONFIG_SYS_DSN: Modificar un origen de datos del sistema existente.  
  
 ODBC_REMOVE_SYS_DSN: Quitar un origen de datos del sistema existente.  
  
 ODBC_REMOVE_DEFAULT_DSN: Quitar la sección de especificación de origen de datos predeterminada de la información del sistema. (También quita la sección predeterminada de la especificación de controlador de la entrada de Odbcinst.ini en la información del sistema. Esto *referien* realiza la misma función que las regiones **SQLRemoveDefaultDataSource** función.) Cuando se especifica esta opción, todos los otros parámetros en la llamada a **SQLConfigDataSource** deben ser valores NULL; si no son NULL, se omitirá.  
  
 *lpszDriver*  
 [Entrada] Descripción del controlador (el nombre del DBMS asociado) presentada a los usuarios en lugar del nombre de controlador físico.  
  
 *lpszAttributes*  
 [Entrada] Una lista doblemente terminada en null de atributos en forma de pares de palabra clave y valor. Para obtener más información, consulte [ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md).  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si se realiza correctamente, FALSE si se produce un error. Si no existe ninguna entrada en la información del sistema cuando se llama a esta función, la función devuelve FALSE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLConfigDataSource** devuelve FALSE, un asociado  *\*pfErrorCode* valor puede obtenerse mediante una llamada a **SQLInstallerError**. La siguiente tabla se recogen los  *\*pfErrorCode* valores que pueden ser devueltos por **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Error del instalador general|Se produjo un error para que no se produjo ningún error de instalación concreto.|  
|ODBC_ERROR_INVALID_HWND|Identificador de ventana no válido|El *hwndParent* argumento era nulo o no válido.|  
|ODBC_ERROR_INVALID_REQUEST_TYPE|Tipo de solicitud no válido|El *fRequest* argumento no es uno de los siguientes:<br /><br /> ODBC_ADD_DSN ODBC_CONFIG_DSN ODBC_REMOVE_DSN ODBC_ADD_SYS_DSN ODBC_CONFIG_SYS_DSN ODBC_REMOVE_SYS_DSN ODBC_REMOVE_DEFAULT_DSN|  
|ODBC_ERROR_INVALID_NAME|Nombre de traductor o controlador no válido|El *lpszDriver* argumento no era válido. No se encontró en el registro.|  
|ODBC_ERROR_INVALID_KEYWORD_VALUE|Pares palabra clave-valor no válidas|El *lpszAttributes* argumento contiene un error de sintaxis.|  
|ODBC_ERROR_REQUEST_FAILED|*Solicitar* error|El programa de instalación no pudo realizar la operación solicitada por el *fRequest* argumento. La llamada a **ConfigDSN** error.|  
|ODBC_ERROR_LOAD_LIBRARY_FAILED|No se pudo cargar la biblioteca de instalación de controlador o traductor|No se pudo cargar la biblioteca de instalación de controladores.|  
|ODBC_ERROR_OUT_OF_MEM|No hay memoria suficiente|El programa de instalación no pudo realizar la función debido a la falta de memoria.|  
  
## <a name="comments"></a>Comentarios  
 **SQLConfigDataSource** utiliza el valor de *lpszDriver* para leer la ruta de acceso completa de la configuración del archivo DLL para el controlador de la información del sistema. Carga el archivo DLL y las llamadas **ConfigDSN** con los mismos argumentos que se pasaron a él.  
  
 **SQLConfigDataSource** devuelve FALSE si no puede encontrar o cargar el archivo DLL de configuración o si el usuario cancela el cuadro de diálogo. De lo contrario, devuelve el estado que recibió del **ConfigDSN**.  
  
 **SQLConfigDataSource** asigna el DSN de sistema *referien*s para el DSN de usuario *fRequest*s (ODBC_ADD_SYS_DSN a ODBC_ADD_DSN, ODBC_CONFIG_SYS_DSN ODBC_CONFIG_DSN y ODBC_REMOVE_SYS _DSN a ODBC_REMOVE_DSN). Para distinguir los DSN de sistema y de usuario **SQLConfigDataSource** establece el instalador en el modo de configuración según la tabla siguiente. Antes de devolver, **SQLConfigDataSource** restablece el modo de configuración a BOTHDSN. **ConfigDSN** (implementada por controladores) debe llamar a **SQLWriteDSNToIni** y **SQLWritePrivateProfileString** para admitir un DSN de sistema. Para obtener más información, consulte [ConfigDSN función](../../../odbc/reference/syntax/configdsn-function.md).  
  
|*fRequest*|Modo de configuración|  
|----------------|------------------------|  
|ODBC_ADD_DSN|USERDSN_ONLY|  
|ODBC_CONFIG_DSN|USERDSN_ONLY|  
|ODBC_REMOVE_DSN|USERDSN_ONLY|  
|ODBC_ADD_SYS_DSN|SYSTEMDSN_ONLY|  
|ODBC_CONFIG_SYS_DSN|SYSTEMDSN_ONLY|  
|ODBC_REMOVE_SYS_DSN|SYSTEMDSN_ONLY|  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Agregar, modificar o quitar un origen de datos|[ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md) (en la configuración del archivo DLL)|  
|Quitar un nombre de origen de datos de la información del sistema|[SQLRemoveDSNFromIni](../../../odbc/reference/syntax/sqlremovedsnfromini-function.md)|  
|Agregar un nombre de origen de datos a la información del sistema|[SQLWriteDSNToIni](../../../odbc/reference/syntax/sqlwritedsntoini-function.md)|

