---
title: Función SQLDrivers | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDrivers
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDrivers
helpviewer_keywords:
- SQLDrivers function [ODBC]
ms.assetid: 6b5b7514-e9cb-4cfd-8b7a-ab51dfab9efa
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 181d3aea0b2c756abc0dc603348cc9cfd728ac4f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65538157"
---
# <a name="sqldrivers-function"></a>Función SQLDrivers
**Conformidad**  
 Versión de introducción: Cumplimiento de estándares 2.0 de ODBC: ODBC  
  
 **Resumen**  
 **SQLDrivers** muestra descripciones del controlador y palabras clave del atributo de controlador. Esta función se implementa solo por el Administrador de controladores.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
SQLRETURN SQLDrivers(  
     SQLHENV         EnvironmentHandle,  
     SQLUSMALLINT    Direction,  
     SQLCHAR *       DriverDescription,  
     SQLSMALLINT     BufferLength1,  
     SQLSMALLINT *   DescriptionLengthPtr,  
     SQLCHAR *       DriverAttributes,  
     SQLSMALLINT     BufferLength2,  
     SQLSMALLINT *   AttributesLengthPtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *EnvironmentHandle*  
 [Entrada] Identificador de entorno.  
  
 *Dirección*  
 [Entrada] Determina si el Administrador de controladores recupera la descripción del controlador siguiente en la lista (SQL_FETCH_NEXT) o si la búsqueda se inicia desde el principio de la lista (SQL_FETCH_FIRST).  
  
 *DriverDescription*  
 [Salida] Puntero a un búfer en el que se va a devolver la descripción del controlador.  
  
 Si *DriverDescription* es NULL, *DescriptionLengthPtr* devolverá el número total de caracteres (excepto el carácter de terminación null para los datos de caracteres) disponibles para devolver en el búfer señalado por *DriverDescription*.  
  
 *BufferLength1*  
 [Entrada] Longitud de la **DriverDescription* búfer en caracteres.  
  
 *DescriptionLengthPtr*  
 [Salida] Puntero a un búfer en el que se va a devolver el número total de caracteres (excepto el carácter de terminación null) disponibles para devolver en \* *DriverDescription*. Si el número de caracteres disponibles para devolver es mayor o igual a *BufferLength1*, la descripción del controlador en \* *DriverDescription* se trunca a  *BufferLength1* menos la longitud de un carácter de terminación null.  
  
 *DriverAttributes*  
 [Salida] Puntero a un búfer en el que se va a devolver la lista de pares de valor de atributo de controlador (vea "Comentarios").  
  
 Si *DriverAttributes* es NULL, *AttributesLengthPtr* devolverá el número total de bytes (excluido el carácter de terminación null para los datos de caracteres) disponibles para devolver en el búfer apunta a *DriverAttributes*.  
  
 *BufferLength2*  
 [Entrada] Longitud de la \* *DriverAttributes* búfer en caracteres. Si el  *\*DriverDescription* valor es una cadena Unicode (al llamar a **SQLDriversW**), el *BufferLength* argumento debe ser un número par.  
  
 *AttributesLengthPtr*  
 [Salida] Puntero a un búfer en el que se va a devolver el número total de bytes (sin incluir los bytes de terminación null) disponibles para devolver en \* *DriverAttributes*. Si el número de bytes disponible para devolver es mayor o igual a *BufferLength2*, la lista de pares de valor de atributo en \* *DriverAttributes* se trunca a  *BufferLength2* menos la longitud del carácter de terminación null.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLDrivers** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_ENV y un *controlar* de *EnvironmentHandle*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLDrivers** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|(DM) mensaje informativo del Administrador de controladores específicos. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01004|Datos de cadena derecha truncados|(DM) el búfer \* *DriverDescription* no era lo suficientemente grande como para devolver la descripción completa del controlador. Por lo tanto, la descripción se ha truncado. Se devuelve la longitud de la descripción completa de controlador en \* *DescriptionLengthPtr*. (La función devuelve SQL_SUCCESS_WITH_INFO).<br /><br /> (DM) el búfer \* *DriverAttributes* no era lo suficientemente grande como para devolver una lista completa de pares de valor de atributo. Por lo tanto, la lista se trunca. Se devuelve la longitud de la lista de pares de valor de atributo sin truncar en **AttributesLengthPtr*. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|HY000|Error general|Se produjo un error para que se ha producido ningún SQLSTATE específico y para los que se ha definido ningún SQLSTATE específicos de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El Administrador de controladores (DM) no pudo asignar memoria que es necesario para admitir la ejecución o la finalización de la función.|  
|HY010|Error de secuencia de función|(DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llamó para el *StatementHandle* y devuelven SQL_PARAM_DATA_ ESTÁ DISPONIBLE. Esta función se invoca antes de que se recuperan los datos para todos los parámetros transmitidos.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos de memoria subyacente no se podrían tener acceso, posiblemente debido a memoria insuficiente.|  
|HY090|Longitud de búfer o cadena no válida|(DM) el valor especificado para el argumento *BufferLength1* era menor que 0.<br /><br /> (DM) el valor especificado para el argumento *BufferLength2* era menor que 0 o igual a 1.|  
|HY103|Código de recuperación no válido|(DM) el valor especificado para el argumento *dirección* no es igual a SQL_FETCH_FIRST o SQL_FETCH_NEXT.|  
|HY117|Conexión está suspendida debido al estado de transacción desconocido. Solo se desconecte y se permiten funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
  
## <a name="comments"></a>Comentarios  
 **SQLDrivers** devuelve la descripción del controlador en el \* *DriverDescription* búfer. Devuelve información adicional sobre el controlador en el \* *DriverAttributes* búfer como una lista de pares palabra clave-valor. Todas las palabras clave mostrado en la información del sistema de controladores se devolverá para todos los controladores, excepto para **CreateDSN**, que se usa para solicitar la creación de orígenes de datos y, por tanto, es opcional. Cada par se termina con un byte nulo y la lista completa se termina con un byte nulo (es decir, dos bytes nulos marcan el final de la lista). Por ejemplo, un controlador basado en archivos con la sintaxis de C podría devolver la siguiente lista de atributos ("\0" representa un carácter nulo):  
  
```  
FileUsage=1\0FileExtns=*.dbf\0\0  
```  
  
 Si \* *DriverAttributes* es no suficientemente grande para contener toda la lista, la lista se trunca, **SQLDrivers** devuelve SQLSTATE 01004 (datos truncados) y la longitud de la lista (excluyendo la byte final de una terminación null) se devuelve en **AttributesLengthPtr*.  
  
 Palabras clave del atributo de controlador se agregan desde la información del sistema cuando el controlador está instalado. Para obtener más información, consulte [instalación de componentes de ODBC](../../../odbc/reference/install/installing-odbc-components.md).  
  
 Una aplicación puede llamar a **SQLDrivers** varias veces para recuperar todas las descripciones del controlador. El Administrador de controladores recupera esta información de la información del sistema. Cuando no hay ningún más descripciones de controlador, **SQLDrivers** devuelve SQL_NO_DATA. Si **SQLDrivers** se llama con SQL_FETCH_NEXT inmediatamente después de que devuelva SQL_NO_DATA, devuelve la primera descripción del controlador. Para obtener información acerca de cómo una aplicación usa la información devuelta por **SQLDrivers**, consulte [elegir un origen de datos o controlador](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md).  
  
 Si se pasa SQL_FETCH_NEXT a **SQLDrivers** la primera vez que se llama, **SQLDrivers** devuelve el primer nombre de origen de datos.  
  
 Dado que **SQLDrivers** se implementa en el Administrador de controladores, se admite para todos los controladores independientemente del cumplimiento de estándares de un controlador determinado.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Detectar y enumerar los valores necesarios para conectarse a un origen de datos|[Función SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|Conectar a un origen de datos|[Función SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|Devolver nombres de origen de datos|[Función SQLDataSources](../../../odbc/reference/syntax/sqldatasources-function.md)|  
|Conectarse a un origen de datos mediante un cuadro de diálogo o la cadena de conexión|[Función SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
