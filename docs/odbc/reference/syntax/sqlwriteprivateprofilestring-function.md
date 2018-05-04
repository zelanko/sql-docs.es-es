---
title: Función SQLWritePrivateProfileString | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
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
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b7691d59d701ed11f1a76715a4d85680890aa7a3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqlwriteprivateprofilestring-function"></a>SQLWritePrivateProfileString (función)
**Conformidad**  
 Versión introdujo: ODBC 2.0  
  
 **Resumen**  
 **SQLWritePrivateProfileString** escribe un nombre de valor y los datos en la subclave Odbc.ini de la información del sistema.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
BOOL SQLWritePrivateProfileString(  
     LPCSTR     lpszSection,  
     LPCSTR     lpszEntry,  
     LPCSTR     lpszString,  
     LPCSTR     lpszFilename);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszSection*  
 [Entrada] Apunta a una cadena terminada en null que contiene el nombre de la sección en la que se copiará la cadena. Si la sección no existe, se crea. El nombre de la sección es independiente del caso; la cadena puede ser cualquier combinación de letras mayúsculas y minúsculas.  
  
 *lpszEntry*  
 [Entrada] Apunta a una cadena terminada en null que contiene el nombre de la clave se asocia con una cadena. Si la clave no existe en la sección especificada, se crea. Si este argumento es NULL, se elimina toda la sección, incluidas todas las entradas en la sección.  
  
 *lpszString*  
 [Entrada] Apunta a una cadena terminada en null se escriban en el archivo. Si este argumento es NULL, la clave que señala el *lpszEntry* argumento se elimina.  
  
 *lpszFilename*  
 [Salida] Apunta a una cadena terminada en null que da nombre al archivo de inicialización.  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si se realiza correctamente, FALSE si se produce un error.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLWritePrivateProfileString** devuelve FALSE, un asociado  *\*pfErrorCode* valor puede obtenerse mediante una llamada a **SQLInstallerError**. La siguiente tabla se recogen los  *\*pfErrorCode* valores que pueden ser devueltos por **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Error del instalador general|Se produjo un error para que no se produjo ningún error de instalación concreto.|  
|ODBC_ERROR_REQUEST_FAILED|Error en la solicitud|No se pudo escribir la información del sistema solicitado.|  
|ODBC_ERROR_OUT_OF_MEM|No hay memoria suficiente|El programa de instalación no pudo realizar la función debido a la falta de memoria.|  
  
## <a name="comments"></a>Comentarios  
 **SQLWritePrivateProfileString** se proporciona como una manera sencilla para los controladores de puerto y las DLL de instalación de controladores de Microsoft® Windows® para Microsoft Windows/Windows 2000. Las llamadas a **WritePrivateProfileString** que escribir una cadena de perfil en el archivo Odbc.ini debe reemplazarse por llamadas a **SQLWritePrivateProfileString**. **SQLWritePrivateProfileString** llama a funciones de la API de Win32® para agregar el nombre de valor especificado y los datos a la subclave Odbc.ini de la información del sistema.  
  
 Un modo de configuración indica que la entrada de Odbc.ini enumerar valores DSN tiene la información del sistema. Si el DSN es un DSN de usuario (la variable de estado es USERDSN_ONLY), la función se escribe en la entrada Odbc.ini en HKEY_CURRENT_USER. Si el DSN es un DSN de sistema (SYSTEMDSN_ONLY), la función se escribe en la entrada Odbc.ini en HKEY_LOCAL_MACHINE. Si la variable de estado es BOTHDSN, se prueba con HKEY_CURRENT_USER, y si se produce un error, se utiliza HKEY_LOCAL_MACHINE.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Obtener un valor de la información del sistema|[SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|
