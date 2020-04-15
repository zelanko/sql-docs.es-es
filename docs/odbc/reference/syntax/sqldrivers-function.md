---
title: Función SQLDrivers (SQLDrivers) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2496e7cd5f2abe0831c72484bed374d7aa1513ce
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302766"
---
# <a name="sqldrivers-function"></a>Función SQLDrivers
**Conformidad**  
 Versión introducida: Cumplimiento de estándares ODBC 2.0: ODBC  
  
 **Resumen**  
 **SQLDrivers** enumera las descripciones del controlador y las palabras clave de atributo de controlador. Esta función solo la implementa el Administrador de controladores.  
  
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
 [Entrada] Mango de entorno.  
  
 *Dirección*  
 [Entrada] Determina si el Administrador de controladores recupera la siguiente descripción del controlador en la lista (SQL_FETCH_NEXT) o si la búsqueda comienza desde el principio de la lista (SQL_FETCH_FIRST).  
  
 *DriverDescription*  
 [Salida] Puntero a un búfer en el que se va a devolver la descripción del controlador.  
  
 Si *DriverDescription* es NULL, *DescriptionLengthPtr* seguirá devolviendo el número total de caracteres (excluyendo el carácter de terminación nula para los datos de caracteres) disponibles para devolver en el búfer señalado por *DriverDescription*.  
  
 *BufferLength1*  
 [Entrada] Longitud del búfer **DriverDescription,* en caracteres.  
  
 *DescripciónLengthPtr*  
 [Salida] Puntero a un búfer en el que se va a devolver el número \*total de caracteres (excluyendo el carácter de terminación nula) disponibles para devolver en *DriverDescription*. Si el número de caracteres disponibles para devolver es mayor \*o igual que *BufferLength1*, la descripción del controlador en *DriverDescription* se trunca en *BufferLength1* menos la longitud de un carácter de terminación nula.  
  
 *DriverAttributes*  
 [Salida] Puntero a un búfer en el que se va a devolver la lista de pares de valores de atributo de controlador (consulte "Comentarios").  
  
 Si *DriverAttributes* es NULL, *AttributesLengthPtr* seguirá devolviendo el número total de bytes (excluyendo el carácter de terminación nula para los datos de caracteres) disponibles para devolver en el búfer señalado por *DriverAttributes*.  
  
 *BufferLength2*  
 [Entrada] Longitud del \*búfer *DriverAttributes,* en caracteres. Si * \** el valor DriverDescription es una cadena Unicode (al llamar a **SQLDriversW**), el argumento *BufferLength* debe ser un número par.  
  
 *AttributesLengthPtr*  
 [Salida] Puntero a un búfer en el que se va a devolver el número \*total de bytes (excluyendo el byte de terminación nula) disponiblepara devolver en *DriverAttributes*. Si el número de bytes disponibles para devolver es mayor o igual \*que *BufferLength2*, la lista de pares de valores de atributo en *DriverAttributes* se trunca en *BufferLength2* menos la longitud del carácter de terminación nula.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLDrivers** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_ENV y un *control* de *EnvironmentHandle*. En la tabla siguiente se enumeran los valores SQLSTATE normalmente devueltos por **SQLDrivers** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|(DM) Mensaje informativo específico del Administrador de controladores. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01004|Datos de cadena truncados a la derecha|(DM) El \*búfer *DriverDescription* no era lo suficientemente grande como para devolver la descripción completa del controlador. Por lo tanto, la descripción se truncó. La longitud de la descripción \*completa del controlador se devuelve en *DescriptionLengthPtr*. (La función devuelve SQL_SUCCESS_WITH_INFO.)<br /><br /> (DM) el \*búfer *DriverAttributes* no era lo suficientemente grande como para devolver la lista completa de pares de valores de atributo. Por lo tanto, la lista se truncó. La longitud de la lista no truncada de pares de valores de atributo se devuelve en **AttributesLengthPtr*. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|HY000|Error general|Se ha producido un error para el que no se ha definido sqlSTATE específico y para el que no se ha definido sqlSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el * \*messageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|(DM) El Administrador de controladores no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función.|  
|HY010|Error de secuencia de funciones|(DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** se llamó para el *StatementHandle* y devuelto SQL_PARAM_DATA_AVAILABLE. Se llamó a esta función antes de recuperar los datos para todos los parámetros transmitidos.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de poca memoria.|  
|HY090|Cadena no válida o longitud de búfer|(DM) el valor especificado para el argumento *BufferLength1* era menor que 0.<br /><br /> (DM) el valor especificado para el argumento *BufferLength2* era menor que 0 o igual que 1.|  
|HY103|Código de recuperación no válido|(DM) El valor especificado para el argumento *Direction* no era igual a SQL_FETCH_FIRST o SQL_FETCH_NEXT.|  
|HY117|La conexión se suspende debido al estado de transacción desconocido. Solo se permiten funciones de desconexión y de solo lectura.|(DM) Para obtener más información sobre el estado suspendido, vea [SqlEndTran (función).](../../../odbc/reference/syntax/sqlendtran-function.md)|  
  
## <a name="comments"></a>Comentarios  
 **SQLDrivers** devuelve la descripción del controlador en el \*búfer *DriverDescription.* Devuelve información adicional sobre el \*controlador en el búfer *DriverAttributes* como una lista de pares palabra clave-valor. Todas las palabras clave enumeradas en la información del sistema para los controladores se devolverán para todos los controladores, excepto **CreateDSN**, que se utiliza para solicitar la creación de orígenes de datos y, por lo tanto, es opcional. Cada par se termina con un byte nulo y la lista completa se termina con un byte nulo (es decir, dos bytes nulos marcan el final de la lista). Por ejemplo, un controlador basado en archivos que usa la sintaxis de C podría devolver la siguiente lista de atributos (en lo que se representa un carácter nulo):  
  
```  
FileUsage=1\0FileExtns=*.dbf\0\0  
```  
  
 Si \* *DriverAttributes* no es lo suficientemente grande como para contener toda la lista, la lista se trunca, **SQLDrivers** devuelve SQLSTATE 01004 (datos truncados) y la longitud de la lista (excluyendo el byte de terminación nula final) se devuelve en **AttributesLengthPtr*.  
  
 Las palabras clave de atributo de controlador se agregan desde la información del sistema cuando se instala el controlador. Para obtener más información, consulte [Instalación de componentes ODBC](../../../odbc/reference/install/installing-odbc-components.md).  
  
 Una aplicación puede llamar a **SQLDrivers** varias veces para recuperar todas las descripciones de controladores. El Administrador de controladores recupera esta información de la información del sistema. Cuando no hay más descripciones de controladores, **SQLDrivers** devuelve SQL_NO_DATA. Si **SQLDrivers** se llama con SQL_FETCH_NEXT inmediatamente después de que devuelve SQL_NO_DATA, devuelve la primera descripción del controlador. Para obtener información sobre cómo una aplicación utiliza la información devuelta por **SQLDrivers**, vea Elegir un origen de [datos o controlador](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md).  
  
 Si SQL_FETCH_NEXT se pasa a **SQLDrivers** la primera vez que se llama, **SQLDrivers** devuelve el primer nombre de origen de datos.  
  
 Dado que **SQLDrivers** se implementa en el Administrador de controladores, se admite para todos los controladores independientemente del cumplimiento de los estándares de un controlador determinado.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Descubrir y enumerar los valores necesarios para conectarse a un origen de datos|[Función SQLBrowseConnect](../../../odbc/reference/syntax/sqlbrowseconnect-function.md)|  
|Conectar a un origen de datos|[Función SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md)|  
|Devolución de nombres de orígenes de datos|[Función SQLDataSources](../../../odbc/reference/syntax/sqldatasources-function.md)|  
|Conexión a un origen de datos mediante una cadena de conexión o un cuadro de diálogo|[Función SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
