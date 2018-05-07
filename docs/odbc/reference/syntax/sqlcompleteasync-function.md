---
title: Función SQLCompleteAsync | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- SQLCompleteAsync
helpviewer_keywords:
- SQLCompleteAsync function [ODBC]
ms.assetid: 1b97c46a-d2e5-4540-8239-9d975e5321c6
caps.latest.revision: 4
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0d3b851fd61209df8a721264e50e5cf1f298da87
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqlcompleteasync-function"></a>SQLCompleteAsync (función)
**Conformidad**  
 Versión incluyen: 3.8 de ODBC  
  
 Cumplimiento de normas: ninguno  
  
 **Resumen**  
 **SQLCompleteAsync** puede utilizarse para determinar cuándo se completan usando cualquier notificación o sondeo-procesamiento basado en una función asincrónica. Para obtener más información acerca de las operaciones asincrónicas, vea [ejecución asincrónica](../../../odbc/reference/develop-app/asynchronous-execution.md).  
  
 **SQLCompleteAsync** solo se implementa en el Administrador de controladores ODBC.  
  
 En el modo de notificación según el procesamiento asincrónico, **SQLCompleteAsync** debe llamarse una vez que el Administrador de controladores genera el objeto de evento utilizado para la notificación. **SQLCompleteAsync** asincrónico se complete el procesamiento y la función asincrónica generará un código de retorno.  
  
 En el modo de procesamiento asincrónico de sondeo basado, **SQLCompleteAsync** es una alternativa a llamar a la función asincrónica original, sin necesidad de especificar los argumentos en la llamada de función asincrónica original. **SQLCompleteAsync** puede usarse sin importar si está habilitada la biblioteca de cursores ODBC.  
  
## <a name="syntax"></a>Sintaxis  
  
```vb  
  
SQLRETURN SQLCompleteAsync(  
      SQLSMALLINT HandleType,  
      SQLHANDLE   Handle,  
      RETCODE *   AsyncRetCodePtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *HandleType*  
 [Entrada] El tipo del identificador en el que se va a completar asincrónico de procesamiento. Los valores válidos son SQL_HANDLE_DBC o SQL_HANDLE_STMT.  
  
 *Handle*  
 [Entrada] Procesando el identificador en el que se va a completar asincrónica. Si *controlar* no es un identificador válido del tipo especificado por *HandleType*, **SQLCompleteAsync** devuelva SQL_INVALID_HANDLE.  
  
 Si *controlar* no es un identificador válido del tipo especificado por *HandleType*, **SQLCompleteAsync** devuelva SQL_INVALID_HANDLE.  
  
 *AsyncRetCodePtr*  
 [Salida] Puntero a un búfer que contendrá el código de retorno de la API asincrónica. Si *AsyncRetCodePtr* es NULL, **SQLCompleteAsync** devuelve SQL_ERROR.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_ERROR, SQL_NO_DATA o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Si **SQLCompleteAsync** devuelve SQL_SUCCESS, una aplicación debe obtener el código de retorno de la función asincrónica desde el búfer señalado por *AsyncRetCodePtr*. El valor de SQLSTATE asociado, si existe, se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_STMT y un identificador de instrucción o un *HandleType* de SQL_ HANDLE_DBC y un identificador de conexión. Los registros de diagnóstico están asociados a la función asincrónica, no se **SQLCompleteAsync** (función).  
  
 **SQLCompleteAsync** devuelve un código que no es SQL_SUCCESS para indicar que **SQLCompleteAsync** no se llama correctamente. **SQLCompleteAsync** no registrará cualquier registro de diagnóstico en este caso. Posibles códigos devueltos son:  
  
-   SQL_INVALID_HANDLE: El identificador indicado por *HandleType* y *controlar* no es un identificador válido.  
  
-   SQL_ERROR: *AsyncRetCodePtr* es NULL o no está habilitado el procesamiento asincrónico en el identificador.  
  
-   SQL_NO_DATA: En el modo de notificación, una operación asincrónica no está en curso o el Administrador de controladores no ha notificado a la aplicación. En el modo de sondeo, una operación asincrónica no está en curso.  
  
## <a name="comments"></a>Comentarios  
 En el modo de procesamiento asincrónico de sondeo basado, *AsyncRetCodePtr* podría ser SQL_STILL_EXECUTING cuando **SQLCompleteAsync** devuelve SQL_SUCCESS. Aplicación debe mantener sondeo hasta *AsyncRetCodePtr* no es SQL_STILL_EXECUTING. En el modo de notificación según el procesamiento asincrónico, *AsyncRetCodePtr* nunca será SQL_STILL_EXECUTING.  
  
## <a name="see-also"></a>Vea también  
 [Ejecución asincrónica (método de sondeo)](../../../odbc/reference/develop-app/asynchronous-execution-polling-method.md)
