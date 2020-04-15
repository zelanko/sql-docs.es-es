---
title: SQLWritePrivateProfileString (Función) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLWritePrivateProfileString
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLWritePrivateProfileString
helpviewer_keywords:
- SQLWritePrivateProfileString [ODBC]
ms.assetid: 526f36a4-92ed-4874-9725-82d27c0b86f9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b0de5ad074fb2b760420686feddff58b26887112
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286888"
---
# <a name="sqlwriteprivateprofilestring-function"></a>Función SQLWritePrivateProfileString
**Conformidad**  
 Versión introducida: ODBC 2.0  
  
 **Resumen**  
 **SQLWritePrivateProfileString** escribe un nombre de valor y datos en la subclave Odbc.ini de la información del sistema.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
BOOL SQLWritePrivateProfileString(  
     LPCSTR     lpszSection,  
     LPCSTR     lpszEntry,  
     LPCSTR     lpszString,  
     LPCSTR     lpszFilename);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszSection*  
 [Entrada] Apunta a una cadena terminada en null que contiene el nombre de la sección en la que se copiará la cadena. Si la sección no existe, se crea. El nombre de la sección es independiente de mayúsculas y minúsculas; la cadena puede ser cualquier combinación de letras mayúsculas y minúsculas.  
  
 *lpszEntry*  
 [Entrada] Apunta a una cadena terminada en null que contiene el nombre de la clave que se va a asociar a una cadena. Si la clave no existe en la sección especificada, se crea. Si este argumento es NULL, se elimina toda la sección, incluidas todas las entradas de la sección.  
  
 *lpszString*  
 [Entrada] Apunta a una cadena terminada en null que se va a escribir en el archivo. Si este argumento es NULL, se elimina la clave a la que apunta el argumento *lpszEntry.*  
  
 *lpszFilename*  
 [Salida] Apunta a una cadena terminada en null que nombra el archivo de inicialización.  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si se realiza correctamente, FALSE si se produce un error.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLWritePrivateProfileString** devuelve FALSE, se puede obtener un valor * \*pfErrorCode* asociado llamando a **SQLInstallerError**. En la tabla * \** siguiente se enumeran los valores pfErrorCode que puede devolver **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Descripción|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Error general del instalador|Se ha producido un error para el que no se ha producido ningún error específico del instalador.|  
|ODBC_ERROR_REQUEST_FAILED|Error en la solicitud|No se pudo escribir la información solicitada del sistema.|  
|ODBC_ERROR_OUT_OF_MEM|No hay memoria suficiente|El instalador no pudo realizar la función debido a la falta de memoria.|  
  
## <a name="comments"></a>Comentarios  
 **SQLWritePrivateProfileString** se proporciona como una forma sencilla de portar controladores y archivos DLL de instalación de controladores de Microsoft® Windows® a Microsoft Windows NT®/Windows 2000. Las llamadas a **WritePrivateProfileString** que escriben una cadena de perfil en el archivo Odbc.ini deben reemplazarse con llamadas a **SQLWritePrivateProfileString**. **SQLWritePrivateProfileString** llama a funciones en la API Win32® para agregar el nombre de valor especificado y los datos a la subclave Odbc.ini de la información del sistema.  
  
 Un modo de configuración indica dónde se encuentra la entrada Odbc.ini que enumera los valores DSN en la información del sistema. Si el DSN es un DSN de usuario (la variable de estado se USERDSN_ONLY), la función escribe en la entrada Odbc.ini de HKEY_CURRENT_USER. Si el DSN es un DSN del sistema (SYSTEMDSN_ONLY), la función escribe en la entrada Odbc.ini en HKEY_LOCAL_MACHINE. Si la variable de estado es BOTHDSN, se intenta HKEY_CURRENT_USER y, si se produce un error, se utiliza HKEY_LOCAL_MACHINE.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Obtener un valor de la información del sistema|[SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|
