---
title: Función SQLGetDiagRec ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 39069526e254903509ddfef00b7bd4844f3d9e10
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285385"
---
# <a name="sqlgetdiagrec-function"></a>Función SQLGetDiagRec
**Conformidad**  
 Versión introducida: Cumplimiento de normas ODBC 3.0: ISO 92  
  
 **Resumen**  
 **SQLGetDiagRec** devuelve los valores actuales de varios campos de un registro de diagnóstico que contiene información de error, advertencia y estado. A diferencia de **SQLGetDiagField**, que devuelve un campo de diagnóstico por llamada, **SQLGetDiagRec** devuelve varios campos de uso común de un registro de diagnóstico, incluido SQLSTATE, el código de error nativo y el texto del mensaje de diagnóstico.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
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
 [Entrada] Identificador de tipo de identificador que describe el tipo de identificador para el que se requieren diagnósticos. Debe ser una de las siguientes:  
  
-   SQL_HANDLE_DBC  
  
-   SQL_HANDLE_DBC_INFO_TOKEN  
  
-   SQL_HANDLE_DESC  
  
-   SQL_HANDLE_ENV  
  
-   SQL_HANDLE_STMT  
  
 SQL_HANDLE_DBC_INFO_TOKEN identificador solo lo utilizan el Administrador de controladores y el controlador. Las aplicaciones no deben usar este tipo de identificador. Para obtener más información acerca de SQL_HANDLE_DBC_INFO_TOKEN, vea Desarrollar el reconocimiento de grupos [de conexiones en un controlador ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md).  
  
 *Handle*  
 [Entrada] Identificador de la estructura de datos de diagnóstico, del tipo indicado por *HandleType*. Si *HandleType* es SQL_HANDLE_ENV, *Handle* puede ser un identificador de entorno compartido o no compartido.  
  
 *RecNumber*  
 [Entrada] Indica el registro de estado del que la aplicación solicita información. Los registros de estado se numeran desde 1.  
  
 *Sqlstate*  
 [Salida] Puntero a un búfer en el que se va a devolver un código SQLSTATE de cinco caracteres (y terminaNDO NULL) para el registro de diagnóstico *RecNumber*. Los dos primeros caracteres indican la clase; los tres siguientes indican la subclase. Esta información se encuentra en el campo de diagnóstico SQL_DIAG_SQLSTATE. Para obtener más información, vea [SQLSTATEs](../../../odbc/reference/develop-app/sqlstates.md).  
  
 *NativeErrorPtr*  
 [Salida] Puntero a un búfer en el que se va a devolver el código de error nativo, específico del origen de datos. Esta información se encuentra en el campo de diagnóstico SQL_DIAG_NATIVE.  
  
 *MessageText*  
 [Salida] Puntero a un búfer en el que se va a devolver la cadena de texto del mensaje de diagnóstico. Esta información se encuentra en el campo de diagnóstico SQL_DIAG_MESSAGE_TEXT. Para conocer el formato de la cadena, vea [Mensajes de diagnóstico](../../../odbc/reference/develop-app/diagnostic-messages.md).  
  
 Si *MessageText* es NULL, *TextLengthPtr* seguirá devolviendo el número total de caracteres (excluyendo el carácter de terminación nula para los datos de caracteres) disponibles para devolver en el búfer al que apunta *MessageText*.  
  
 *BufferLength*  
 [Entrada] Longitud del búfer **MessageText* en caracteres. No hay una longitud máxima del texto del mensaje de diagnóstico.  
  
 *TextLengthPtr*  
 [Salida] Puntero a un búfer en el que se va a devolver el número total de caracteres (excluyendo el número de caracteres necesarios para el carácter de terminación nula) disponibles para devolver en * \*MessageText*. Si el número de caracteres disponibles para devolver es mayor que *BufferLength*, el texto del mensaje de diagnóstico en * \*MessageText* se trunca a *BufferLength* menos la longitud de un carácter de terminación nula.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 **SQLGetDiagRec** no publica registros de diagnóstico por sí mismo. Utiliza los siguientes valores devueltos para informar del resultado de su propia ejecución:  
  
-   SQL_SUCCESS: la función devolvió correctamente la información de diagnóstico.  
  
-   SQL_SUCCESS_WITH_INFO: \*el búfer *MessageText* era demasiado pequeño para contener el mensaje de diagnóstico solicitado. No se generaron registros de diagnóstico. Para determinar que se ha producido un truncamiento, la aplicación debe comparar *BufferLength* con el número real de bytes disponibles, que se escribe en **StringLengthPtr*.  
  
-   SQL_INVALID_HANDLE: el identificador indicado por *HandleType* y *Handle* no era un identificador válido.  
  
-   SQL_ERROR: Se ha producido una de las siguientes situaciones:  
  
    -   *RecNumber* fue negativo o 0.  
  
    -   *BufferLength* era menor que cero.  
  
    -   Cuando se usa la notificación asincrónica, la operación asincrónica en el identificador no se completó.  
  
-   SQL_NO_DATA: *RecNumber* era mayor que el número de registros de diagnóstico que existían para el identificador especificado en *Handle.* La función también devuelve SQL_NO_DATA para cualquier *RecNumber* positivo si no hay registros de diagnóstico para *Handle*.  
  
## <a name="comments"></a>Comentarios  
 Normalmente, una aplicación llama a **SQLGetDiagRec** cuando una llamada anterior a una función ODBC ha devuelto SQL_ERROR o SQL_SUCCESS_WITH_INFO. Sin embargo, dado que cualquier función ODBC puede publicar cero o más registros de diagnóstico cada vez que se llama, una aplicación puede llamar a **SQLGetDiagRec** después de cualquier llamada a la función ODBC. Una aplicación puede llamar a **SQLGetDiagRec** varias veces para devolver algunos o todos los registros de la estructura de datos de diagnóstico. ODBC no impone ningún límite al número de registros de diagnóstico que se pueden almacenar a la vez.  
  
 **SQLGetDiagRec** no se puede usar para devolver campos desde el encabezado de la estructura de datos de diagnóstico. (El *argumento RecNumber* debe ser mayor que 0.) La aplicación debe llamar a **SQLGetDiagField** para este propósito.  
  
 **SQLGetDiagRec** recupera solo la información de diagnóstico asociada más recientemente con el identificador especificado en el *Handle* argumento. Si la aplicación llama a otra función ODBC, excepto **SQLGetDiagRec**, **SQLGetDiagField**o **SQLError**, se pierde cualquier información de diagnóstico de las llamadas anteriores en el mismo identificador.  
  
 Una aplicación puede examinar todos los registros de diagnóstico mediante bucle, incrementando *RecNumber*, siempre y cuando **SQLGetDiagRec** devuelve SQL_SUCCESS. Las llamadas a **SQLGetDiagRec** no son destructivas para los campos de encabezado y registro. La aplicación puede llamar a **SQLGetDiagRec** de nuevo en un momento posterior para recuperar un campo de un registro siempre que no se haya llamado a ninguna otra función, excepto **SQLGetDiagRec**, **SQLGetDiagField**o **SQLError**, en el intermedio. La aplicación también puede recuperar un recuento del número total de registros de diagnóstico disponibles mediante una llamada a **SQLGetDiagField** para recuperar el valor del campo SQL_DIAG_NUMBER y, a continuación, llamar a **SQLGetDiagRec** muchas veces.  
  
 Para obtener una descripción de los campos de la estructura de datos de diagnóstico, vea [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md). Para obtener más información, vea Uso de [SQLGetDiagRec y SQLGetDiagField](../../../odbc/reference/develop-app/using-sqlgetdiagrec-and-sqlgetdiagfield.md) e [Implementación de SQLGetDiagRec y SQLGetDiagField](../../../odbc/reference/develop-app/implementing-sqlgetdiagrec-and-sqlgetdiagfield.md).  
  
 Llamar a una API distinta de la que se ejecuta de forma asincrónica generará HY010 "Error de secuencia de funciones". Sin embargo, el registro de error no se puede recuperar antes de que se complete la operación asincrónica.  
  
## <a name="handletype-argument"></a>Argumento HandleType  
 Cada tipo de identificador puede tener información de diagnóstico asociada. El *HandleType* argumento denota el tipo de identificador de la *Handle* argumento.  
  
 Algunos campos de encabezado y registro no se pueden devolver para los identificadores de entorno, conexión, instrucción y descriptor. Los identificadores para los que un campo no es aplicable se indican en las secciones "Campos de encabezado" y "Campos de registro" de [SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md).  
  
 Una llamada a **SQLGetDiagRec** devolverá SQL_INVALID_HANDLE si *HandleType* es SQL_HANDLE_SENV, lo que denota un identificador de entorno compartido. Sin embargo, si *HandleType* es SQL_HANDLE_ENV, *Handle* puede ser un identificador de entorno compartido o no compartido.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Obtención de un campo de un registro de diagnóstico o un campo de la cabecera de diagnóstico|[Función SQLGetDiagField](../../../odbc/reference/syntax/sqlgetdiagfield-function.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Programa de ejemplo de ODBC](../../../odbc/reference/sample-odbc-program.md)
