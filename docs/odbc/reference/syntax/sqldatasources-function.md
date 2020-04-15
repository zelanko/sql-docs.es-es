---
title: Función SQLDataSources (SQLDataSources) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b56a6c25e54897e67beaf39d3b7797ac45391d7b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301185"
---
# <a name="sqldatasources-function"></a>Función SQLDataSources
**Conformidad**  
 Versión introducida: Cumplimiento de normas ODBC 1.0: ISO 92  
  
 **Resumen**  
 **SQLDataSources** devuelve información sobre un origen de datos. Esta función solo la implementa el Administrador de controladores.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
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
 [Entrada] Mango de entorno.  
  
 *Dirección*  
 [Entrada] Determina sobre qué origen de datos devuelve información el Administrador de controladores. Puede ser:  
  
 SQL_FETCH_NEXT (para obtener el siguiente nombre de origen de datos en la lista), SQL_FETCH_FIRST (para obtener desde el principio de la lista), SQL_FETCH_FIRST_USER (para obtener el primer DSN de usuario) o SQL_FETCH_FIRST_SYSTEM (para obtener el primer DSN del sistema).  
  
 Cuando *Direction* se establece en SQL_FETCH_FIRST, las llamadas posteriores a **SQLDataSources** con *Direction* establecido en SQL_FETCH_NEXT devolver los DSN de usuario y del sistema. Cuando *Direction* se establece en SQL_FETCH_FIRST_USER, todas las llamadas posteriores a **SQLDataSources** con *Direction* establecido en SQL_FETCH_NEXT devolver solo los DSN de usuario. Cuando *Direction* se establece en SQL_FETCH_FIRST_SYSTEM, todas las llamadas posteriores a **SQLDataSources** con *Direction* establecido en SQL_FETCH_NEXT devolver solo los DSN del sistema.  
  
 *nombreDeServidor*  
 [Salida] Puntero a un búfer en el que se va a devolver el nombre del origen de datos.  
  
 Si *ServerName* es NULL, *NameLength1Ptr* seguirá devolviendo el número total de caracteres (excluyendo el carácter de terminación nula para los datos de caracteres) disponibles para devolver en el búfer al que apunta *ServerName*.  
  
 *BufferLength1*  
 [Entrada] Longitud del búfer **ServerName,* en caracteres; esto no necesita ser más largo que SQL_MAX_DSN_LENGTH más el carácter de terminación nula.  
  
 *NameLength1Ptr*  
 [Salida] Puntero a un búfer en el que se va a devolver el número \*total de caracteres (excluyendo el carácter de terminación nula) disponibles para devolver en *ServerName*. Si el número de caracteres disponibles para devolver es mayor o \*igual que *BufferLength1*, el nombre del origen de datos en *ServerName* se trunca a *BufferLength1* menos la longitud de un carácter de terminación nula.  
  
 *Descripción*  
 [Salida] Puntero a un búfer en el que se va a devolver la descripción del controlador asociado al origen de datos. Por ejemplo, dBASE o SQL Server.  
  
 Si *Description* es NULL, *NameLength2Ptr* seguirá devolviendo el número total de caracteres (excluyendo el carácter de terminación nula para los datos de caracteres) disponibles para devolver en el búfer al que apunta *Description*.  
  
 *BufferLength2*  
 [Entrada] Longitud en caracteres del búfer **Description.*  
  
 *NameLength2Ptr*  
 [Salida] Puntero a un búfer en el que se va a devolver el número \*total de caracteres (excluyendo el carácter de terminación nula) disponibles para devolver en *Descripción*. Si el número de caracteres disponibles para devolver es mayor \*o igual que *BufferLength2*, la descripción del controlador en *Description* se trunca en *BufferLength2* menos la longitud de un carácter de terminación nula.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLDataSources** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_ENV y un *control* de *EnvironmentHandle*. En la tabla siguiente se enumeran los valores SQLSTATE normalmente devueltos por **SQLDataSources** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|(DM) Mensaje informativo específico del Administrador de controladores. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01004|Datos de cadena truncados a la derecha|(DM) El \*búfer *ServerName* no era lo suficientemente grande como para devolver el nombre completo del origen de datos. Por lo tanto, el nombre se truncó. La longitud del nombre completo del \*origen de datos se devuelve en *NameLength1Ptr*. (La función devuelve SQL_SUCCESS_WITH_INFO.)<br /><br /> (DM) La \* *descripción* del búfer no era lo suficientemente grande como para devolver la descripción completa del controlador. Por lo tanto, la descripción se truncó. La longitud de la descripción del origen de datos no truncado se devuelve en **NameLength2Ptr*. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|HY000|Error general|(DM) Se ha producido un error para el que no se ha definido SQLSTATE específico y para el que no se ha definido sqlSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el * \*messageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|(DM) El Administrador de controladores no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función.|  
|HY010|Error de secuencia de funciones|(DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** se llamó para el *StatementHandle* y devuelto SQL_PARAM_DATA_AVAILABLE. Se llamó a esta función antes de recuperar los datos para todos los parámetros transmitidos.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de poca memoria.|  
|HY090|Cadena no válida o longitud de búfer|(DM) el valor especificado para el argumento *BufferLength1* era menor que 0.<br /><br /> (DM) el valor especificado para el argumento *BufferLength2* era menor que 0.|  
|HY103|Código de recuperación no válido|(DM) el valor especificado para el argumento *Direction* no era igual a SQL_FETCH_FIRST, SQL_FETCH_FIRST_USER, SQL_FETCH_FIRST_SYSTEM o SQL_FETCH_NEXT.|  
|HY117|La conexión se suspende debido al estado de transacción desconocido. Solo se permiten funciones de desconexión y de solo lectura.|(DM) Para obtener más información sobre el estado suspendido, vea [SqlEndTran (función).](../../../odbc/reference/syntax/sqlendtran-function.md)|  
  
## <a name="comments"></a>Comentarios  
 Dado que **SQLDataSources** se implementa en el Administrador de controladores, se admite para todos los controladores, independientemente del cumplimiento de los estándares de un controlador determinado.  
  
 Una aplicación puede llamar a **SQLDataSources** varias veces para recuperar todos los nombres de origen de datos. El Administrador de controladores recupera esta información de la información del sistema. Cuando no hay más nombres de origen de datos, el Administrador de controladores devuelve SQL_NO_DATA. Si **SQLDataSources** se llama con SQL_FETCH_NEXT inmediatamente después de que devuelve SQL_NO_DATA, devolverá el primer nombre de origen de datos. Para obtener información sobre cómo una aplicación utiliza la información devuelta por **SQLDataSources**, vea Elegir un origen de [datos o controlador](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md).  
  
 Si SQL_FETCH_NEXT se pasa a **SQLDataSources** la primera vez que se llama, devolverá el primer nombre de origen de datos.  
  
 El controlador determina cómo se asignan los nombres de origen de datos a orígenes de datos reales.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Descubrir y enumerar los valores necesarios para conectarse a un origen de datos|[Función SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|Conectar a un origen de datos|[Función SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|Conexión a un origen de datos mediante una cadena de conexión o un cuadro de diálogo|[Función SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
|Devolver las descripciones y atributos del controlador|[Función SQLDrivers](../../../odbc/reference/syntax/sqldrivers-function.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
