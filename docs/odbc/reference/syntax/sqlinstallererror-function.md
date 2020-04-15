---
title: Función SQLInstallerError (SQLInstallerError) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLInstallerError
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLInstallerError
helpviewer_keywords:
- SQLInstallerError [ODBC]
ms.assetid: e6474b79-4d55-458f-81ce-abfafe357f83
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e749237cf87c5054b8273f38531d9336d316e040
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302106"
---
# <a name="sqlinstallererror-function"></a>Función SQLInstallerError
**Conformidad**  
 Versión introducida: ODBC 3.0  
  
 **Resumen**  
 **SQLInstallerError** devuelve información de error o estado para las funciones del instalador ODBC.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
RETCODE SQLInstallerError(  
     WORD      iError,  
     DWORD *   pfErrorCode,  
     LPSTR     lpszErrorMsg,  
     WORD      cbErrorMsgMax,  
     WORD *    pcbErrorMsg);  
```  
  
## <a name="arguments"></a>Argumentos  
 *iError*  
 [Entrada] Número de registro de error. Los números válidos son del 1 al 8.  
  
 *pfErrorCode*  
 [Salida] Código de error del instalador. (Para obtener más información, consulte "Comentarios.")  
  
 *lpszErrorMsg*  
 [Salida] Puntero al almacenamiento para el texto del mensaje de error.  
  
 *cbErrorMsgMax*  
 [Entrada] Longitud máxima del búfer *szErrorMsg.* Debe ser menor o igual que SQL_MAX_MESSAGE_LENGTH menos el carácter de terminación nula.  
  
 *cbErrorMsgMax*  
 [Entrada] Longitud máxima del búfer *szErrorMsg.* Debe ser menor o igual que SQL_MAX_MESSAGE_LENGTH menos el carácter de terminación nula.  
  
 *pcbErrorMsg*  
 [Salida] Puntero al número total de bytes (excluyendo el carácter de terminación nula) disponibles para devolver en *lpszErrorMsg*. Si el número de bytes disponibles para devolver es mayor o igual que *cbErrorMsgMax*, el texto del mensaje de error en *lpszErrorMsg* se trunca en *cbErrorMsgMax* menos los bytes de carácter de terminación nula. El argumento *pcbErrorMsg* puede ser un puntero nulo.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA o SQL_ERROR.  
  
## <a name="diagnostics"></a>Diagnóstico  
 **SQLInstallerError** no publica valores de error por sí mismo. **SQLInstallerError** devuelve SQL_NO_DATA cuando no puede recuperar ninguna información de error (en cuyo caso *pfErrorCode* es indefinido). Si **SQLInstallerError** no puede tener acceso a los valores de error por cualquier motivo que normalmente devolvería SQL_ERROR, **SQLInstallerError** devuelve SQL_ERROR pero no registra ningún valor de error. Si no conoce la longitud de la cadena de advertencia (*lpszErrorMsg*), puede establecer *lpszErrorMsg* en NULL y llamar a **SQLInstallerError**. **SQLInstallerError** devolverá la longitud de la cadena de advertencia en *cbErrorMsgMax*. Si el búfer del mensaje de error es demasiado corto, **SQLInstallerError** devuelve SQL_SUCCESS_WITH_INFO y devuelve el valor *pfErrorCode* correcto para **SQLInstallerError**.  
  
 Para determinar si se ha producido un truncamiento en el mensaje de error, una aplicación puede comparar el valor del argumento *cbErrorMsgMax* con la longitud real del texto del mensaje escrito en el argumento *pcbErrorMsg.* Si se produce el truncamiento, se debe asignar la longitud de búfer correcta para *lpszErrorMsg* y **SQLInstallerError** debe llamarse de nuevo con el registro *iError* correspondiente.  
  
## <a name="comments"></a>Comentarios  
 Una aplicación llama a **SQLInstallerError** cuando una llamada anterior a la función del instalador ODBC devuelve FALSE. Las funciones de configuración del instalador y del controlador o del traductor ODBC publican cero o más errores solo cuando se produce un error en la función (devuelve FALSE); por lo tanto, una aplicación llama a **SQLInstallerError** solo después de que se produce un error en una función de instalador ODBC.  
  
 La cola de errores del instalador ODBC se vacía cada vez que se llama a una nueva función del instalador. Por lo tanto, una aplicación no puede esperar recuperar errores para funciones que no sean de la última llamada de función del instalador.  
  
 Para recuperar varios errores para una llamada de función, una aplicación llama a **SQLInstallerError** varias veces.  
  
 Cuando no hay información adicional, **SQLInstallerError** devuelve SQL_NO_DATA, el argumento *pfErrorCode* es indefinido, el argumento *pcbErrorMsg* es igual a 0 y el argumento *lpszErrorMsg* contiene un único carácter de terminación nula (a menos que el argumento *cbErrorMsgMax* sea igual a 0).
