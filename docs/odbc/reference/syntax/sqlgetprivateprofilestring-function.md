---
title: Función SQLGetPrivateProfileString | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 17ac06d65d519be86ec077e6c6d39896c7f5ad46
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65537338"
---
# <a name="sqlgetprivateprofilestring-function"></a>Función SQLGetPrivateProfileString
**Conformidad**  
 Versión de introducción: ODBC 2.0  
  
 **Resumen**  
 **SQLGetPrivateProfileString** Obtiene una lista de nombres de valores o datos que corresponde a un valor de la información del sistema.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
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
 [Entrada] Apunta a la cadena terminada en null que contiene el nombre de clave cuya cadena asociado se van a recuperar. Si este argumento es NULL, todas las claves de nombres en la sección especificada por el *lpszSection* argumento se copian en el búfer especificado por el *RetBuffer* argumento.  
  
 *lpszDefault*  
 [Entrada] Apunta a una cadena terminada en null que especifica el valor predeterminado de la clave especificada si la clave no se encuentra en el archivo de inicialización. Este argumento no puede ser NULL.  
  
 *RetBuffer*  
 [Salida] Apunta al búfer que recibe la cadena recuperada.  
  
 *cbRetBuffer*  
 [Entrada] Especifica el tamaño, en caracteres, del búfer señalado por el *RetBuffer* argumento.  
  
 *lpszFilename*  
 [Entrada] Apunta a una cadena terminada en null que se asigna nombre al archivo de inicialización. Si este argumento no contiene una ruta de acceso completa al archivo, se busca en el directorio predeterminado.  
  
## <a name="returns"></a>Devuelve  
 **SQLGetPrivateProfileString** devuelve un valor entero que indica el número de caracteres leídos.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando una llamada a **SQLGetPrivateProfileString** produce un error, un asociado  *\*pfErrorCode* valor puede obtenerse mediante una llamada a **SQLInstallerError**. La siguiente tabla se enumeran los  *\*pfErrorCode* valores que pueden devolver **SQLInstallerError** y se explica cada uno de ellos en el contexto de esta función.  
  
|*\*pfErrorCode*|Error|Descripción|  
|---------------------|-----------|-----------------|  
|ODBC_ERROR_GENERAL_ERR|Error del instalador general|Se produjo un error para que se ha producido ningún error de instalación concreto.|  
|ODBC_ERROR_OUT_OF_MEM|No hay memoria suficiente|El programa de instalación no pudo realizar la función debido a la falta de memoria.|  
  
## <a name="comments"></a>Comentarios  
 **SQLGetPrivateProfileString** se proporciona como una manera sencilla para controladores de puerto y las DLL de instalación de controladores de Microsoft® Windows® para Microsoft Windows o Windows 2000. Las llamadas a **GetPrivateProfileString** que recuperar una cadena de perfil del archivo Odbc.ini debe reemplazarse por las llamadas a **SQLGetPrivateProfileString**. **SQLGetPrivateProfileString** llama a las funciones de la API de Win32® para recuperar los nombres de valores o datos que corresponde a un valor de la subclave Odbc.ini la información del sistema solicitados.  
  
 El modo de configuración (como lo establece **SQLSetConfigMode**) indica que la entrada del archivo Odbc.ini enumerar valores DSN es en la información del sistema. Si el DSN es un DSN de usuario (el modo de configuración es USERDSN_ONLY), la función lee la entrada del archivo Odbc.ini en HKEY_CURRENT_USER. Si el DSN es un DSN de sistema (SYSTEMDSN_ONLY), la función lee la entrada del archivo Odbc.ini en HKEY_LOCAL_MACHINE. Si el modo de configuración es BOTHDSN, se ha intentado HKEY_CURRENT_USER y, si se produce un error, se usa HKEY_LOCAL_MACHINE.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Escribir un valor en la información del sistema|[SQLWritePrivateProfileString](../../../odbc/reference/syntax/sqlwriteprivateprofilestring-function.md)|
