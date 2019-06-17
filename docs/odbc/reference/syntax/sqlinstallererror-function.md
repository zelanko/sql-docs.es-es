---
title: Función SQLInstallerError | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a0ae475ba4dc290f57eadf94d1e45e8a203a7ce5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65536596"
---
# <a name="sqlinstallererror-function"></a>Función SQLInstallerError
**Conformidad**  
 Versión de introducción: ODBC 3.0  
  
 **Resumen**  
 **SQLInstallerError** devuelve información de estado o de error para las funciones del instalador ODBC.  
  
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
 [Entrada] Número de registro de error. Números válidos son de 1 a 8.  
  
 *pfErrorCode*  
 [Salida] Código de error del instalador. (Para obtener más información, vea "Comentarios".)  
  
 *lpszErrorMsg*  
 [Salida] Puntero al almacenamiento para el texto del mensaje de error.  
  
 *cbErrorMsgMax*  
 [Entrada] Longitud máxima de la *szErrorMsg* búfer. Debe ser menor o igual que SQL_MAX_MESSAGE_LENGTH menos el carácter de terminación null.  
  
 *cbErrorMsgMax*  
 [Entrada] Longitud máxima de la *szErrorMsg* búfer. Debe ser menor o igual que SQL_MAX_MESSAGE_LENGTH menos el carácter de terminación null.  
  
 *pcbErrorMsg*  
 [Salida] Puntero al número total de bytes (excluido el carácter de terminación null) disponibles para devolver en *lpszErrorMsg*. Si el número de bytes disponible para devolver es mayor o igual a *cbErrorMsgMax*, el texto del mensaje de error en *lpszErrorMsg* se trunca a *cbErrorMsgMax* menos el bytes de caracteres de terminación NULL. El *pcbErrorMsg* argumento puede ser un puntero nulo.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA o SQL_ERROR.  
  
## <a name="diagnostics"></a>Diagnósticos  
 **SQLInstallerError** no registra los valores de error para sí mismo. **SQLInstallerError** devuelve SQL_NO_DATA cuando no puede recuperar cualquier información de error (en cuyo caso *pfErrorCode* no está definido). Si **SQLInstallerError** no se puede obtener acceso a los valores de error por algún motivo que normalmente devolvería SQL_ERROR, **SQLInstallerError** devuelve SQL_ERROR, pero no envía los valores de error. Si no conoce la longitud de la cadena de advertencia (*lpszErrorMsg*), puede establecer *lpszErrorMsg* en NULL y llamada **SQLInstallerError**. **SQLInstallerError** le retorno, a continuación, la longitud de la cadena de advertencia en *cbErrorMsgMax*. Si el búfer del mensaje de error es demasiado corto, **SQLInstallerError** devuelve SQL_SUCCESS_WITH_INFO y devuelve el valor correcto *pfErrorCode* valor **SQLInstallerError**.  
  
 Para determinar si se produjo un truncamiento en el mensaje de error, una aplicación puede comparar el valor de la *cbErrorMsgMax* argumento a la longitud real del texto del mensaje que escribe en el *pcbErrorMsg* argumento. Si se produce un truncamiento, se debe asignar la longitud del búfer correcto para *lpszErrorMsg* y **SQLInstallerError** se debe llamar de nuevo con el correspondiente *iError*registro.  
  
## <a name="comments"></a>Comentarios  
 Una aplicación llama a **SQLInstallerError** cuando una llamada anterior a la función del instalador ODBC devuelve FALSE. Funciones de configuración de instalador y el traductor o controlador ODBC registrar errores de cero o más solo cuando se produce un error en la función (devuelve FALSE); por lo tanto, una aplicación llama a **SQLInstallerError** solo después de que se produce un error en una función de instalador ODBC.  
  
 La cola de errores del instalador ODBC se vacía cada vez que se llama a una nueva función de instalador. Por lo tanto, no se puede esperar una aplicación recuperar errores para las funciones que no sea de la última llamada de función del instalador.  
  
 Para recuperar varios errores para una llamada de función, una aplicación llama a **SQLInstallerError** varias veces.  
  
 Cuando no hay ninguna información adicional, **SQLInstallerError** devuelve SQL_NO_DATA, la *pfErrorCode* argumento está definido, el *pcbErrorMsg* argumento es igual a 0, y el *lpszErrorMsg* argumento contiene un único carácter de terminación null (a menos que el *cbErrorMsgMax* argumento es igual a 0).
