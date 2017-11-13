---
title: "Función SQLGetPrivateProfileString | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLGetPrivateProfileString
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetPrivateProfileString
helpviewer_keywords:
- SQLGetPrivateProfileString function [ODBC]
ms.assetid: b72ca065-4d67-48df-baac-e18379a8320a
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 49c1939845ed63f295054afab629389f3e1bbcaf
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetprivateprofilestring-function"></a>SQLGetPrivateProfileString (función)
**Conformidad**  
 Versión introdujo: ODBC 2.0  
  
 **Resumen**  
 **SQLGetPrivateProfileString** Obtiene una lista de nombres de valores o datos que se corresponde con el valor de la información del sistema.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
int SQLGetPrivateProfileString(  
     LPCSTR   lpszSection,  
     LPCSTR   lpszEntry,  
     LPCSTR   lpszDefault,  
     LPCSTR   RetBuffer,  
     INT      cbRetBuffer,  
     LPCSTR   lpszFilename);  
```  
  
## <a name="arguments"></a>Argumentos  
 *lpszSection*  
 [Entrada] Apunta a una cadena terminada en null que especifica la sección que contiene el nombre de clave. Si este argumento es NULL, la función copia todos los nombres de sección en el archivo en el búfer proporcionado.  
  
 *lpszEntry*  
 [Entrada] Apunta a la cadena terminada en null que contiene el nombre de clave cuya cadena asociada se van a recuperar. Si este argumento es NULL, todos los nombres de clave en la sección especificada por el *lpszSection* argumento se copia en el búfer especificado por el *RetBuffer* argumento.  
  
 *lpszDefault*  
 [Entrada] Apunta a una cadena terminada en null que especifica el valor predeterminado de la clave especificada si la clave no se encuentra en el archivo de inicialización. Este argumento no puede ser NULL.  
  
 *RetBuffer*  
 [Salida] Señala al búfer que recibe la cadena recuperada.  
  
 *cbRetBuffer*  
 [Entrada] Especifica el tamaño, en caracteres, del búfer que señala el *RetBuffer* argumento.  
  
 *lpszFilename*  
 [Entrada] Apunta a una cadena terminada en null que da nombre al archivo de inicialización. Si este argumento no contiene una ruta de acceso completa al archivo, se busca en el directorio predeterminado.  
  
## <a name="returns"></a>Devuelve  
 **SQLGetPrivateProfileString** devuelve un valor entero que indica el número de caracteres leídos.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando una llamada a **SQLGetPrivateProfileString** se produce un error, un asociado  *\*pfErrorCode* valor puede obtenerse mediante una llamada a **SQLInstallerError**. La siguiente tabla se recogen los  *\*pfErrorCode* valores que pueden ser devueltos por **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Description|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Error del instalador general|Se produjo un error para que no se produjo ningún error de instalación concreto.|  
|ODBC_ERROR_OUT_OF_MEM|No hay memoria suficiente|El programa de instalación no pudo realizar la función debido a la falta de memoria.|  
  
## <a name="comments"></a>Comentarios  
 **SQLGetPrivateProfileString** se proporciona como una manera sencilla para los controladores de puerto y las DLL de instalación de controladores de Microsoft® Windows® para Microsoft Windows/Windows 2000. Las llamadas a **GetPrivateProfileString** que recuperar una cadena de perfil del archivo Odbc.ini debe reemplazarse por llamadas a **SQLGetPrivateProfileString**. **SQLGetPrivateProfileString** llama a funciones de la API de Win32® para recuperar los nombres de valores o datos que se corresponde con el valor de la subclave Odbc.ini de la información del sistema solicitados.  
  
 El modo de configuración (tal como lo establece **SQLSetConfigMode**) indica que la entrada de Odbc.ini enumerar valores DSN en la información del sistema. Si el DSN es un DSN de usuario (el modo de configuración es USERDSN_ONLY), la función lee de la entrada Odbc.ini en HKEY_CURRENT_USER. Si el DSN es un DSN de sistema (SYSTEMDSN_ONLY), la función lee de la entrada Odbc.ini en HKEY_LOCAL_MACHINE. Si el modo de configuración es BOTHDSN, se prueba con HKEY_CURRENT_USER, y si se produce un error, se utiliza HKEY_LOCAL_MACHINE.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Si escribe un valor a la información del sistema|[SQLWritePrivateProfileString](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|

