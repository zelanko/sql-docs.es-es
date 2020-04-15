---
title: Función SQLCompleteAsync ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
f1_keywords:
- SQLCompleteAsync
helpviewer_keywords:
- SQLCompleteAsync function [ODBC]
ms.assetid: 1b97c46a-d2e5-4540-8239-9d975e5321c6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4e09d61ef516e846798dd3af2d07dafa78af4605
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299660"
---
# <a name="sqlcompleteasync-function"></a>Función SQLCompleteAsync
**Conformidad**  
 Versión introducida: ODBC 3.8  
  
 Cumplimiento de normas: Ninguno  
  
 **Resumen**  
 **SQLCompleteAsync** se puede usar para determinar cuándo se completa una función asincrónica mediante el procesamiento basado en notificaciones o sondeos. Para obtener más información acerca de las operaciones asincrónicas, vea [Ejecución asincrónica](../../../odbc/reference/develop-app/asynchronous-execution.md).  
  
 **SQLCompleteAsync** solo se implementa en el Administrador de controladores ODBC.  
  
 En el modo de procesamiento asincrónico basado en notificaciones, **sqlCompleteAsync** debe llamarse después de que el Administrador de controladores genera el objeto de evento utilizado para la notificación. **SQLCompleteAsync** completa el procesamiento asincrónico y la función asincrónica generará un código de retorno.  
  
 En el modo de procesamiento asincrónico basado en sondeos, **SQLCompleteAsync** es una alternativa a llamar a la función asincrónica original, sin necesidad de especificar los argumentos en la llamada de función asincrónica original. **SQLCompleteAsync** se puede usar independientemente de si la biblioteca de cursores ODBC está habilitada.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
SQLRETURN SQLCompleteAsync(  
      SQLSMALLINT HandleType,  
      SQLHANDLE   Handle,  
      RETCODE *   AsyncRetCodePtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *HandleType*  
 [Entrada] El tipo del identificador en el que se completa el procesamiento asincrónico. Los valores válidos son SQL_HANDLE_DBC o SQL_HANDLE_STMT.  
  
 *Handle*  
 [Entrada] Identificador en el que se completa el procesamiento asincrónico. Si *Handle* no es un identificador válido del tipo especificado por *HandleType*, **SQLCompleteAsync** devuelve SQL_INVALID_HANDLE.  
  
 Si *Handle* no es un identificador válido del tipo especificado por *HandleType*, **SQLCompleteAsync** devuelve SQL_INVALID_HANDLE.  
  
 *AsyncRetCodePtr*  
 [Salida] Puntero a un búfer que contendrá el código de retorno de la API asincrónica. Si *AsyncRetCodePtr* es NULL, **SQLCompleteAsync** devuelve SQL_ERROR.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_ERROR, SQL_NO_DATA o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Si **SQLCompleteAsync** devuelve SQL_SUCCESS, una aplicación debe obtener el código de retorno de la función asincrónica desde el búfer al que apunta *AsyncRetCodePtr*. El SQLSTATE asociado, si existe, se puede obtener llamando a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_STMT y un identificador de instrucción o un *HandleType* de SQL_HANDLE_DBC y un identificador de conexión. Esos registros de diagnóstico están asociados a la función asincrónica, no a esta función **SQLCompleteAsync.**  
  
 **SQLCompleteAsync** devuelve un código distinto de SQL_SUCCESS para indicar que **SQLCompleteAsync** no se llama correctamente. **SQLCompleteAsync** no registrará ningún registro de diagnóstico en este caso. Los posibles códigos de retorno son:  
  
-   SQL_INVALID_HANDLE: el identificador indicado por *HandleType* y *Handle* no es un identificador válido.  
  
-   SQL_ERROR: *AsyncRetCodePtr* es NULL o el procesamiento asincrónico no está habilitado en el identificador.  
  
-   SQL_NO_DATA: en el modo de notificación, una operación asincrónica no está en curso o el Administrador de controladores no ha notificado a la aplicación. En el modo de sondeo, una operación asincrónica no está en curso.  
  
## <a name="comments"></a>Comentarios  
 En el modo de procesamiento asincrónico basado en sondeos, *AsyncRetCodePtr* podría SQL_STILL_EXECUTING cuando **SQLCompleteAsync** devuelve SQL_SUCCESS. La aplicación debe seguir sondeando hasta que *AsyncRetCodePtr* no se SQL_STILL_EXECUTING. En el modo de procesamiento asincrónico basado en notificaciones, *AsyncRetCodePtr* nunca se SQL_STILL_EXECUTING.  
  
## <a name="see-also"></a>Consulte también  
 [Ejecución asincrónica (método de sondeo)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
