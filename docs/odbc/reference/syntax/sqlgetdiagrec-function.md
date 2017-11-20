---
title: "Función SQLGetDiagRec | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLGetDiagRec
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetDiagRec
helpviewer_keywords:
- SQLGetDiagRec function [ODBC]
ms.assetid: ebdbac93-3d68-438f-8416-ef1f08e04269
caps.latest.revision: 26
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 591664f329f4c7feeb24fff52b809dba567d0b80
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetdiagrec-function"></a>SQLGetDiagRec, función
**Conformidad**  
 Versión introdujo: ODBC 3.0 normativas: ISO 92  
  
 **Resumen**  
 **SQLGetDiagRec** devuelve los valores actuales de varios campos de un registro de diagnóstico que contiene el error, advertencia e información de estado. A diferencia de **SQLGetDiagField**, que devuelve un campo de diagnóstico por llamada, **SQLGetDiagRec** devuelve varios campos de un registro de diagnóstico, incluidos los valores de SQLSTATE, el código de error nativo más usan y el texto del mensaje de diagnóstico.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SQLRETURN SQLGetDiagRec(  
     SQLSMALLINT     HandleType,  
     SQLHANDLE       Handle,  
     SQLSMALLINT     RecNumber,  
     SQLCHAR *       SQLState,  
     SQLINTEGER *    NativeErrorPtr,  
     SQLCHAR *       MessageText,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   TextLengthPtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *HandleType*  
 [Entrada] Un identificador de tipo de identificador que describe el tipo de identificador para el que se requieren los diagnósticos. Debe ser una de las siguientes:  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 Identificador SQL_HANDLE_DBC_INFO_TOKEN se utiliza únicamente por el Administrador de controladores y el controlador. Las aplicaciones no deben usar este tipo de identificador. Para obtener más información sobre SQL_HANDLE_DBC_INFO_TOKEN, consulte [desarrollar conocimiento de la agrupación de conexiones en un controlador ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).  
  
 *Handle*  
 [Entrada] Un identificador para la estructura de datos de diagnóstico, del tipo indicado por *HandleType*. Si *HandleType* es SQL_HANDLE_ENV, *controlar* puede ser compartida o un identificador de entorno no compartido.  
  
 *RecNumber*  
 [Entrada] Indica que el registro de estado desde el que la aplicación busca información. Registros de estado se numeran del 1.  
  
 *SQLState*  
 [Salida] Puntero a un búfer en el que se va a devolver un código SQLSTATE de cinco caracteres (y el carácter nulo final) para el registro de diagnóstico *RecNumber*. Los dos primeros caracteres indican la clase; los tres siguientes indican la subclase. Esta información se encuentra en el campo de diagnóstico de SQL_DIAG_SQLSTATE. Para obtener más información, consulte [SQLSTATEs](../../../odbc/reference/develop-app/sqlstates.md).  
  
 *NativeErrorPtr*  
 [Salida] Puntero a un búfer en el que se va a devolver el código de error nativo específico del origen de datos. Esta información se encuentra en el campo de diagnóstico de SQL_DIAG_NATIVE.  
  
 *MessageText*  
 [Salida] Puntero a un búfer en el que se va a devolver la cadena de texto de mensaje de diagnóstico. Esta información se encuentra en el campo de diagnóstico de SQL_DIAG_MESSAGE_TEXT. Para el formato de la cadena, vea [mensajes de diagnóstico](../../../odbc/reference/develop-app/diagnostic-messages.md).  
  
 Si *MessageText* es NULL, *TextLengthPtr* devolverá el número total de caracteres (excepto el carácter de terminación null para los datos de carácter) disponible para devolver en el búfer señalado por *MessageText*.  
  
 *BufferLength*  
 [Entrada] Longitud de la **MessageText* búfer en caracteres. No hay ninguna longitud máxima del texto del mensaje de diagnóstico.  
  
 *TextLengthPtr*  
 [Salida] Puntero a un búfer en el que se va a devolver el número total de caracteres (excepto el número de caracteres necesarios para el carácter de terminación null) disponible para devolver en  *\*MessageText*. Si es mayor que el número de caracteres disponibles para devolver *BufferLength*, el texto del mensaje de diagnóstico en  *\*MessageText* se trunca a *BufferLength* menos la longitud de un carácter de terminación null.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 **SQLGetDiagRec** no registra los registros de diagnóstico para sí mismo. Utiliza los siguientes valores devueltos para indicar el resultado de su propio ejecución:  
  
-   SQL_SUCCESS: La función devolvió información de diagnóstico.  
  
-   SQL_SUCCESS_WITH_INFO: El \* *MessageText* búfer es demasiado pequeño para contener el mensaje de diagnóstico solicitado. No se genera ningún registro de diagnóstico. Para determinar que se produjo un truncamiento, la aplicación debe comparar *BufferLength* en el número real de bytes disponibles, que se escribe en **StringLengthPtr*.  
  
-   SQL_INVALID_HANDLE: El identificador indicado por *HandleType* y *controlar* no es un identificador válido.  
  
-   SQL_ERROR: Producido uno de los siguientes:  
  
    -   *RecNumber* era negativo o 0.  
  
    -   *BufferLength* era menor que cero.  
  
    -   Cuando se utiliza la notificación asincrónica, no finalizó la operación asincrónica en el identificador.  
  
-   SQL_NO_DATA: *RecNumber* era mayor que el número de registros de diagnóstico que existían en el identificador especificado en *controlar.* La función también devuelve SQL_NO_DATA para los valores positivos *RecNumber* si no hay ningún registro de diagnóstico para *controlar*.  
  
## <a name="comments"></a>Comentarios  
 Una aplicación suele llamar **SQLGetDiagRec** cuando una llamada anterior a una función ODBC ha devuelto SQL_ERROR o SQL_SUCCESS_WITH_INFO. Sin embargo, como una función de ODBC puede registrar cada vez que se llama de cero o más registros de diagnóstico, una aplicación puede llamar a **SQLGetDiagRec** después de cualquier llamada a la función ODBC. Una aplicación puede llamar a **SQLGetDiagRec** varias veces para devolver algunos o todos los registros de la estructura de datos de diagnóstico. ODBC no impone ningún límite para el número de registros de diagnóstico que se pueden almacenar en cualquier momento.  
  
 **SQLGetDiagRec** no se puede usar para devolver los campos del encabezado de la estructura de datos de diagnóstico. (El *RecNumber* argumento debe ser mayor que 0.) La aplicación debe llamar a **SQLGetDiagField** para este propósito.  
  
 **SQLGetDiagRec** recupera sólo la información de diagnóstico más recientemente asociada al identificador especificado en el *controlar* argumento. Si la aplicación llama a otra función ODBC, excepto **SQLGetDiagRec**, **SQLGetDiagField**, o **SQLError**, cualquier información de diagnóstico de las llamadas anteriores en el identificador de la misma se pierde.  
  
 Una aplicación puede buscar todos los registros de diagnóstico mediante un bucle, incrementar *RecNumber*, siempre y cuando **SQLGetDiagRec** devuelve SQL_SUCCESS. Las llamadas a **SQLGetDiagRec** son destructivos a los campos de encabezado y el registro. La aplicación puede llamar a **SQLGetDiagRec** nuevo en un momento posterior para recuperar un campo de un registro siempre y como ninguna otra función, excepto **SQLGetDiagRec**, **SQLGetDiagField**, o **SQLError**, se ha llamado en el ínterin. La aplicación también puede recuperar un recuento del número total de registros de diagnóstico disponibles mediante una llamada a **SQLGetDiagField** para recuperar el valor del campo SQL_DIAG_NUMBER y, a continuación, llamando **SQLGetDiagRec**ese número veces.  
  
 Para obtener una descripción de los campos de la estructura de datos de diagnóstico, vea [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md). Para obtener más información, consulte [utilizando SQLGetDiagRec y SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md) y [implementar SQLGetDiagRec y SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md).  
  
 Llamar a una API que no sea el que se está ejecutando de forma asincrónica generará HY010 "Error en la secuencia de función". Sin embargo, no se puede recuperar el registro de error antes de que finalice la operación asincrónica.  
  
## <a name="handletype-argument"></a>Argumento HandleType  
 Cada tipo de identificador puede tener información de diagnóstico asociada con él. El *HandleType* argumento indica el tipo de identificador de la *controlar* argumento.  
  
 Algunos campos de encabezado y el registro no se puede devolver para el entorno, conexión, instrucción y descriptor de identificadores. Los identificadores para los que un campo no es aplicable se indican en las secciones "Campos de encabezado" y "Campos de registro" de [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md).  
  
 Una llamada a **SQLGetDiagRec** devolverá SQL_INVALID_HANDLE si *HandleType* es SQL_HANDLE_SENV, que indica un identificador de entorno compartido. Sin embargo, si *HandleType* es SQL_HANDLE_ENV, *controlar* puede ser compartida o un identificador de entorno no compartido.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Obtención de un campo de un registro de diagnóstico o un campo del encabezado del diagnóstico|[SQLGetDiagField, función](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Programa de ejemplo de ODBC](../../../odbc/reference/sample-odbc-program.md)

