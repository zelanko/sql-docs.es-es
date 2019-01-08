---
title: Función SQLDataSources | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDataSources
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDataSources
helpviewer_keywords:
- SQLDataSources function [ODBC]
ms.assetid: 3f63b1b4-e70e-44cd-96c6-6878d50d0117
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b7b04dc2554b820fc6ac8344457754aae984d4b8
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/11/2018
ms.locfileid: "53213114"
---
# <a name="sqldatasources-function"></a>Función SQLDataSources
**Conformidad**  
 Versión de introducción: Cumplimiento de estándares 1.0 de ODBC: 92 ISO  
  
 **Resumen**  
 **SQLDataSources** devuelve información acerca de un origen de datos. Esta función se implementa solo por el Administrador de controladores.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SQLRETURN SQLDataSources(  
     SQLHENV          EnvironmentHandle,  
     SQLUSMALLINT     Direction,  
     SQLCHAR *        ServerName,  
     SQLSMALLINT      BufferLength1,  
     SQLSMALLINT *    NameLength1Ptr,  
     SQLCHAR *        Description,  
     SQLSMALLINT      BufferLength2,  
     SQLSMALLINT *    NameLength2Ptr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *EnvironmentHandle*  
 [Entrada] Identificador de entorno.  
  
 *Dirección*  
 [Entrada] Determina qué origen de datos del Administrador de controladores devuelve información acerca de. Puede ser:  
  
 SQL_FETCH_NEXT (para capturar el siguiente nombre de origen de datos en la lista), SQL_FETCH_FIRST (para capturar desde el principio de la lista), SQL_FETCH_FIRST_USER (para el DSN de usuario de la primera captura) o SQL_FETCH_FIRST_SYSTEM (para capturar el primer sistema DSN).  
  
 Cuando *dirección* está establecido en SQL_FETCH_FIRST, las llamadas subsiguientes a **SQLDataSources** con *dirección* establecido en SQL_FETCH_NEXT devolver los DSN de usuario y del sistema. Cuando *dirección* está establecido en SQL_FETCH_FIRST_USER, todas las llamadas subsiguientes a **SQLDataSources** con *dirección* establecido en SQL_FETCH_NEXT devolver sólo los DSN de usuario. Cuando *dirección* está establecido en SQL_FETCH_FIRST_SYSTEM, todas las llamadas subsiguientes a **SQLDataSources** con *dirección* establecido en SQL_FETCH_NEXT devolver sólo DSN del sistema.  
  
 *ServerName*  
 [Salida] Puntero a un búfer en el que se va a devolver el nombre del origen de datos.  
  
 Si *ServerName* es NULL, *NameLength1Ptr* devolverá el número total de caracteres (excepto el carácter de terminación null para los datos de caracteres) disponibles para devolver en el búfer señalado por *ServerName*.  
  
 *BufferLength1*  
 [Entrada] Longitud de la **ServerName* búfer en caracteres; no es necesario que puede tener más de SQL_MAX_DSN_LENGTH y el carácter de terminación null.  
  
 *NameLength1Ptr*  
 [Salida] Puntero a un búfer en el que se va a devolver el número total de caracteres (excepto el carácter de terminación null) disponibles para devolver en \* *ServerName*. Si el número de caracteres disponibles para devolver es mayor o igual a *BufferLength1*, el nombre del origen de datos en \* *ServerName* se trunca a *BufferLength1* menos la longitud de un carácter de terminación null.  
  
 *Descripción*  
 [Salida] Puntero a un búfer en el que se va a devolver la descripción del controlador asociado con el origen de datos. Por ejemplo, dBASE o SQL Server.  
  
 Si *descripción* es NULL, *NameLength2Ptr* devolverá el número total de caracteres (excepto el carácter de terminación null para los datos de caracteres) disponibles para devolver en el búfer señalado por *Descripción*.  
  
 *BufferLength2*  
 [Entrada] Longitud en caracteres de la **descripción* búfer.  
  
 *NameLength2Ptr*  
 [Salida] Puntero a un búfer en el que se va a devolver el número total de caracteres (excepto el carácter de terminación null) disponibles para devolver en \* *descripción*. Si el número de caracteres disponibles para devolver es mayor o igual a *BufferLength2*, la descripción del controlador en \* *descripción* se trunca a *BufferLength2*  menos la longitud de un carácter de terminación null.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLDataSources** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType*de SQL_HANDLE_ENV y un *controlar* de *EnvironmentHandle*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLDataSources** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|(DM) mensaje informativo del Administrador de controladores específicos. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01004|Datos de cadena derecha truncados|(DM) el búfer \* *ServerName* no era lo suficientemente grande como para devolver el nombre de origen de datos completo. Por lo tanto, el nombre se ha truncado. Se devuelve la longitud del nombre del origen de datos completa en \* *NameLength1Ptr*. (La función devuelve SQL_SUCCESS_WITH_INFO).<br /><br /> (DM) el búfer \* *descripción* no era lo suficientemente grande como para devolver la descripción completa del controlador. Por lo tanto, la descripción se ha truncado. Se devuelve la longitud de la descripción del origen de datos sin truncar en **NameLength2Ptr*. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|HY000|Error general|(DM) a un error para que se ha producido ningún SQLSTATE específico para el que no se definió ningún SQLSTATE específicos de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El Administrador de controladores (DM) no pudo asignar memoria que es necesario para admitir la ejecución o la finalización de la función.|  
|HY010|Error de secuencia de función|(DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llamó para el *StatementHandle* y devuelven SQL_PARAM_DATA_ ESTÁ DISPONIBLE. Esta función se invoca antes de que se recuperan los datos para todos los parámetros transmitidos.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos de memoria subyacente no se podrían tener acceso, posiblemente debido a memoria insuficiente.|  
|HY090|Longitud de búfer o cadena no válida|(DM) el valor especificado para el argumento *BufferLength1* era menor que 0.<br /><br /> (DM) el valor especificado para el argumento *BufferLength2* era menor que 0.|  
|HY103|Código de recuperación no válido|(DM) el valor especificado para el argumento *dirección* no es igual a SQL_FETCH_FIRST, SQL_FETCH_FIRST_USER, SQL_FETCH_FIRST_SYSTEM o SQL_FETCH_NEXT.|  
|HY117|Conexión está suspendida debido al estado de transacción desconocido. Solo se desconecte y se permiten funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
  
## <a name="comments"></a>Comentarios  
 Dado que **SQLDataSources** se implementa en el Administrador de controladores, se admite para todos los controladores independientemente del cumplimiento de estándares de un controlador determinado.  
  
 Una aplicación puede llamar a **SQLDataSources** varias veces para recuperar todos los nombres de origen de datos. El Administrador de controladores recupera esta información de la información del sistema. Cuando no hay ningún nombre de origen de datos más, el Administrador de controladores devuelve SQL_NO_DATA. Si **SQLDataSources** se llama con SQL_FETCH_NEXT inmediatamente después de que devuelva SQL_NO_DATA, devolverá el primer nombre de origen de datos. Para obtener información acerca de cómo una aplicación usa la información devuelta por **SQLDataSources**, consulte [elegir un origen de datos o controlador](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md).  
  
 Si se pasa SQL_FETCH_NEXT a **SQLDataSources** la primera vez que se llama, devolverá el primer nombre de origen de datos.  
  
 El controlador determina cómo se asignan los nombres de origen de datos a orígenes de datos real.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Detectar y enumerar los valores necesarios para conectarse a un origen de datos|[Función SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|Conectar a un origen de datos|[Función SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|Conectarse a un origen de datos mediante un cuadro de diálogo o la cadena de conexión|[Función SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|Devuelve la descripción de los controladores y atributos|[Función SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
