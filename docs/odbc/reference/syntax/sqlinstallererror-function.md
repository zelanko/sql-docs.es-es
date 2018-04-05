---
title: Función SQLInstallerError | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
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
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c3cdc3ae1e4efe4292077851a4f457bae4af17bd
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="sqlinstallererror-function"></a>SQLInstallerError (función)
**Conformidad**  
 Versión introdujo: ODBC 3.0  
  
 **Resumen**  
 **SQLInstallerError** devuelve información de estado o de error para las funciones del instalador ODBC.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
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
 [Salida] Puntero al número total de bytes (sin incluir el carácter de terminación null) disponible para devolver en *lpszErrorMsg*. Si el número de bytes disponible para devolver es mayor o igual que *cbErrorMsgMax*, el texto del mensaje de error en *lpszErrorMsg* se trunca a *cbErrorMsgMax* menos el bytes de carácter de terminación NULL. El *pcbErrorMsg* argumento puede ser un puntero nulo.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA o SQL_ERROR.  
  
## <a name="diagnostics"></a>Diagnósticos  
 **SQLInstallerError** no publica valores de error para sí mismo. **SQLInstallerError** devuelve SQL_NO_DATA cuando no puede recuperar cualquier información de error (en cuyo caso *pfErrorCode* no está definido). Si **SQLInstallerError** no se puede obtener acceso a los valores de error por algún motivo que normalmente devuelve SQL_ERROR, **SQLInstallerError** devuelve SQL_ERROR pero no envía los valores de error. Si no conoce la longitud de la cadena de advertencia (*lpszErrorMsg*), puede establecer *lpszErrorMsg* a NULL y llame al método **SQLInstallerError**. **SQLInstallerError** le devuelve a continuación, la longitud de la cadena de advertencia en *cbErrorMsgMax*. Si el búfer del mensaje de error es demasiado corto, **SQLInstallerError** devuelve SQL_SUCCESS_WITH_INFO y devuelve el valor correcto *pfErrorCode* valor **SQLInstallerError**.  
  
 Para determinar si se produjo un truncamiento en el mensaje de error, una aplicación puede comparar el valor de la *cbErrorMsgMax* argumento pasado a la longitud real del texto del mensaje que escribe en el *pcbErrorMsg* argumento pasado. Si se produce el truncamiento, se debe asignar la longitud de búfer correcto para *lpszErrorMsg* y **SQLInstallerError** debería llamar de nuevo con la correspondiente *iError*registro.  
  
## <a name="comments"></a>Comentarios  
 Una aplicación llama **SQLInstallerError** cuando una llamada anterior a la función de instalador ODBC devuelve FALSE. Funciones de configuración de instalador y traductor o controlador ODBC registrar cero o más errores sólo cuando se produce un error en la función (devuelve FALSE); por lo tanto, una aplicación llama **SQLInstallerError** solo después de que se produce un error en una función de instalador ODBC.  
  
 La cola de errores de instalador ODBC se vacía cada vez que se invoque una función nueva del instalador. Por lo tanto, no se puede esperar una aplicación recuperar errores de funciones distinto de la última llamada de función de instalador.  
  
 Para recuperar varios errores para una llamada de función, una aplicación llama **SQLInstallerError** varias veces.  
  
 Cuando no hay ninguna información adicional, **SQLInstallerError** devuelve SQL_NO_DATA, la *pfErrorCode* argumento está definido, el *pcbErrorMsg* argumento es igual a 0, y el *lpszErrorMsg* argumento contiene un único carácter de terminación null (a menos que la *cbErrorMsgMax* argumento es igual a 0).
