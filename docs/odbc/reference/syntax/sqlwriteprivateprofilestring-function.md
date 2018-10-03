---
title: Función SQLWritePrivateProfileString | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: aeff68aaa4e4901820054a9bf3079efc7d74cebc
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47818853"
---
# <a name="sqlwriteprivateprofilestring-function"></a>Función SQLWritePrivateProfileString
**Conformidad**  
 Versión introdujo: ODBC 2.0  
  
 **Resumen**  
 **SQLWritePrivateProfileString** escribe un nombre de valor y los datos en la subclave Odbc.ini la información del sistema.  
  
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
 [Entrada] Apunta a una cadena terminada en null que contiene el nombre de la sección a la que se copiará la cadena. Si la sección no existe, se crea. El nombre de la sección es independiente del caso; la cadena puede ser cualquier combinación de mayúsculas y minúsculas.  
  
 *lpszEntry*  
 [Entrada] Apunta a una cadena terminada en null que contiene el nombre de la clave que se va a asociar con una cadena. Si la clave no existe en la sección especificada, se crea. Si este argumento es NULL, la sección toda, incluidas todas las entradas en la sección, se elimina.  
  
 *lpszString*  
 [Entrada] Apunta a una cadena terminada en null se escriban en el archivo. Si este argumento es NULL, la clave apunta a la *lpszEntry* argumento se elimina.  
  
 *lpszFilename*  
 [Salida] Apunta a una cadena terminada en null que se asigna nombre al archivo de inicialización.  
  
## <a name="returns"></a>Devuelve  
 La función devuelve TRUE si es correcto, FALSE si se produce un error.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLWritePrivateProfileString** devuelve FALSE, un asociado  *\*pfErrorCode* valor puede obtenerse mediante una llamada a **SQLInstallerError**. La siguiente tabla se enumeran los  *\*pfErrorCode* valores que pueden devolver **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Descripción|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Error del instalador general|Se produjo un error para que se ha producido ningún error de instalación concreto.|  
|ODBC_ERROR_REQUEST_FAILED|Error en la solicitud|No se pudo escribir la información del sistema solicitado.|  
|ODBC_ERROR_OUT_OF_MEM|No hay memoria suficiente|El programa de instalación no pudo realizar la función debido a la falta de memoria.|  
  
## <a name="comments"></a>Comentarios  
 **SQLWritePrivateProfileString** se proporciona como una manera sencilla para controladores de puerto y las DLL de instalación de controladores de Microsoft® Windows® para Microsoft Windows o Windows 2000. Las llamadas a **WritePrivateProfileString** que escribir una cadena de perfil en el archivo Odbc.ini debe reemplazarse por las llamadas a **SQLWritePrivateProfileString**. **SQLWritePrivateProfileString** llama a las funciones de la API de Win32® para agregar el nombre del valor especificado y los datos a la subclave Odbc.ini la información del sistema.  
  
 Un modo de configuración indica que la entrada del archivo Odbc.ini enumerar valores DSN es la información del sistema. Si el DSN es un DSN de usuario (la variable de estado es USERDSN_ONLY), la función escribe en la entrada del archivo Odbc.ini en HKEY_CURRENT_USER. Si el DSN es un DSN de sistema (SYSTEMDSN_ONLY), la función escribe en la entrada del archivo Odbc.ini en HKEY_LOCAL_MACHINE. Si la variable de estado es BOTHDSN, se ha intentado HKEY_CURRENT_USER y, si se produce un error, se usa HKEY_LOCAL_MACHINE.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Obtener un valor de la información del sistema|[SQLGetPrivateProfileString](../../../odbc/reference/syntax/sqlgetprivateprofilestring-function.md)|
