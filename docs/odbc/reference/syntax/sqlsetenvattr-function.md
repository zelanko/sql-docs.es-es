---
title: Función SQLSetEnvAttr ( SQLSetEnvAttr ) Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetEnvAttr
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLSetEnvAttr
helpviewer_keywords:
- SQLSetEnvAttr function [ODBC]
ms.assetid: 0343241c-4b15-4d4b-aa2b-2e8ab5215cd2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 640b1e6947d67b92e2b7f8e623597e1d99d4a877
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299545"
---
# <a name="sqlsetenvattr-function"></a>Función SQLSetEnvAttr
**Conformidad**  
 Versión introducida: Cumplimiento de normas ODBC 3.0: ISO 92  
  
 **Resumen**  
 **SQLSetEnvAttr** establece atributos que rigen aspectos de los entornos.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
SQLRETURN SQLSetEnvAttr(  
     SQLHENV      EnvironmentHandle,  
     SQLINTEGER   Attribute,  
     SQLPOINTER   ValuePtr,  
     SQLINTEGER   StringLength);  
```  
  
## <a name="arguments"></a>Argumentos  
 *EnvironmentHandle*  
 [Entrada] Mango de entorno.  
  
 *Atributo*  
 [Entrada] Atributo a establecer, que aparece en "Comentarios."  
  
 *ValuePtr*  
 [Entrada] Puntero al valor que se va a asociar a *Attribute*. Dependiendo del valor de *Attribute*, *ValuePtr* será un valor entero de 32 bits o apuntará a una cadena de caracteres terminada en null.  
  
 *StringLength*  
 [Entrada] Si *ValuePtr* apunta a una cadena de caracteres o un búfer binario, este argumento debe ser la longitud de **ValuePtr*. Para los datos de cadena de caracteres, este argumento debe contener el número de bytes de la cadena.  
  
 Si *ValuePtr* es un entero, *StringLength* se omite.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLSetEnvAttr** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_ENV y un *control* de *EnvironmentHandle*. En la tabla siguiente se enumeran los valores SQLSTATE normalmente devueltos por **SQLSetEnvAttr** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario. Si un controlador no admite un atributo de entorno, el error solo se puede devolver durante el tiempo de conexión.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo específico del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01S02|Valor de opción cambiado|El controlador no admitió el valor especificado en *ValuePtr* y sustituyó un valor similar. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|HY000|Error general|Se ha producido un error para el que no se ha definido sqlSTATE específico y para el que no se ha definido sqlSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el * \*messageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función.|  
|HY009|Uso no válido de puntero nulo|El atributo Attribute argumento identificó un atributo de entorno que requería un valor de cadena y el *ValuePtr* argumento era un puntero nulo.|  
|HY010|Error de secuencia de funciones|(DM) Se ha asignado un identificador de conexión en *EnvironmentHandle*.<br /><br /> (DM) **SQL_ATTR_ODBC_VERSION** no se ha establecido con **SQLSetEnvAttr** y *Attribute* no es igual a **SQL_ATTR_ODBC_VERSION**. No es necesario establecer **SQL_ATTR_ODBC_VERSION** explícitamente si utiliza **SQLAllocHandleStd**.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de poca memoria.|  
|HY024|Valor de atributo no válido|Dado el valor *Attribute* especificado, se especificó un valor no válido en *ValuePtr*.|  
|HY090|Cadena no válida o longitud de búfer|El *StringLength* argumento era menor que 0 pero no era SQL_NTS.|  
|HY092|Identificador de atributo/opción no válido|(DM) el valor especificado para el argumento *Attribute* no era válido para la versión de ODBC admitida por el controlador.|  
|HY117|La conexión se suspende debido al estado de transacción desconocido. Solo se permiten funciones de desconexión y de solo lectura.|(DM) Para obtener más información sobre el estado suspendido, vea [SqlEndTran (función).](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|HYC00|Característica opcional no implementada|El valor especificado para el argumento *Attribute* era un atributo de entorno ODBC válido para la versión de ODBC admitida por el controlador, pero no lo admitía el controlador.<br /><br /> (DM) el *atributo* argumento era SQL_ATTR_OUTPUT_NTS y *ValuePtr* se SQL_FALSE.|  
  
## <a name="comments"></a>Comentarios  
 Una aplicación puede llamar a **SQLSetEnvAttr** solo si no se asigna ningún identificador de conexión en el entorno. Todos los atributos de entorno establecidos correctamente por la aplicación para el entorno persisten hasta **sqlFreeHandle** se llama en el entorno. Se puede asignar más de un identificador de entorno simultáneamente en ODBC *3.x*.  
  
 El formato de la información establecida a través *de ValuePtr* depende del *atributo*especificado . **SQLSetEnvAttr** aceptará información de atributo en uno de los dos formatos diferentes: una cadena de caracteres terminada en null o un valor entero de 32 bits. El formato de cada uno se indica en la descripción del atributo.  
  
 No hay atributos de entorno específicos del controlador.  
  
 Los atributos de conexión no se pueden establecer mediante una llamada a **SQLSetEnvAttr**. Al intentar hacerlo, se devolverá SQLSTATE HY092 (identificador de atributo/opción no válido).  
  
|*Atributo*|*Contenido valuePtr*|  
|-----------------|-------------------------|  
|SQL_ATTR_CONNECTION_POOLING (ODBC 3.8)|Un valor SQLUINTEGER de 32 bits que habilita o deshabilita la agrupación de conexiones en el nivel de entorno. Se utilizan los siguientes valores:<br /><br /> SQL_CP_OFF: la agrupación de conexiones está desactivada. Este es el valor predeterminado.<br /><br /> SQL_CP_ONE_PER_DRIVER: se admite un único grupo de conexiones para cada controlador. Cada conexión de un grupo está asociada a un controlador.<br /><br /> SQL_CP_ONE_PER_HENV: se admite un único grupo de conexiones para cada entorno. Cada conexión de un grupo está asociada a un entorno.<br /><br /> SQL_CP_DRIVER_AWARE: Utilice la característica de reconocimiento de la agrupación de conexiones del controlador, si está disponible. Si el controlador no admite el reconocimiento del grupo de conexiones, se omite SQL_CP_DRIVER_AWARE y se usa SQL_CP_ONE_PER_HENV. Para obtener más información, consulte Agrupación de [conexiones compatible con controladores](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md). En un entorno donde algunos controladores admiten y algunos controladores no admiten el reconocimiento del grupo de conexiones, SQL_CP_DRIVER_AWARE puede habilitar la característica de reconocimiento de la agrupación de conexiones en los controladores compatibles, pero equivale a establecer SQL_CP_ONE_PER_HENV en aquellos controladores que no admiten la característica de reconocimiento de grupo de conexiones.<br /><br /> La agrupación de conexiones se habilita mediante una llamada a **SQLSetEnvAttr** para establecer el atributo SQL_ATTR_CONNECTION_POOLING en SQL_CP_ONE_PER_DRIVER o SQL_CP_ONE_PER_HENV. Esta llamada debe realizarse antes de que la aplicación asigne el entorno compartido para el que se va a habilitar la agrupación de conexiones. El identificador de entorno en la llamada a **SQLSetEnvAttr** se establece en null, lo que hace que SQL_ATTR_CONNECTION_POOLING un atributo de nivel de proceso. Una vez habilitada la agrupación de conexiones, la aplicación asigna un entorno compartido implícito llamando a **SQLAllocHandle** con el argumento *InputHandle* establecido en SQL_HANDLE_ENV.<br /><br /> Una vez habilitada la agrupación de conexiones y seleccionado un entorno compartido para una aplicación, no se puede restablecer SQL_ATTR_CONNECTION_POOLING para ese entorno, porque **SQLSetEnvAttr** se llama con un identificador de entorno nulo al establecer este atributo. Si este atributo se establece mientras la agrupación de conexiones ya está habilitada en un entorno compartido, el atributo solo afecta a los entornos compartidos que se asignan posteriormente.<br /><br /> También es posible habilitar la agrupación de conexiones en un entorno. Tenga en cuenta lo siguiente acerca de la agrupación de conexiones de entorno:<br /><br /> - Habilitar la agrupación de conexiones en un identificador NULL es un atributo de nivel de proceso. Los entornos asignados posteriormente serán un entorno compartido y heredarán la configuración de agrupación de conexiones de nivel de proceso.<br />- Una vez asignado un entorno, una aplicación todavía puede cambiar la configuración del grupo de conexiones.<br />- Si la agrupación de conexiones de entorno está habilitada y el controlador de la conexión utiliza la agrupación de controladores, la agrupación de entornos tiene preferencia.<br /><br /> SQL_ATTR_CONNECTION_POOLING se implementa dentro del Administrador de controladores. Un controlador no necesita implementar SQL_ATTR_CONNECTION_POOLING. Las aplicaciones ODBC 2.0 y 3.0 pueden establecer este atributo de entorno.<br /><br /> Para obtener más información, consulte este artículo sobre la [agrupación de conexiones ODBC](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md).|  
|SQL_ATTR_CP_MATCH (ODBC 3.0)|Un valor SQLUINTEGER de 32 bits que determina cómo se elige una conexión de un grupo de conexiones. Cuando **sqlConnect** o **SQLDriverConnect** se llama, el Administrador de controladores determina qué conexión se reutiliza desde el grupo. El Administrador de controladores intenta hacer coincidir las opciones de conexión de la llamada y los atributos de conexión establecidos por la aplicación con las palabras clave y los atributos de conexión de las conexiones del grupo. El valor de este atributo determina el nivel de precisión de los criterios de coincidencia.<br /><br /> Los siguientes valores se utilizan para establecer el valor de este atributo:<br /><br /> SQL_CP_STRICT_MATCH: solo se reutilizan las conexiones que coinciden exactamente con las opciones de conexión de la llamada y los atributos de conexión establecidos por la aplicación. Este es el valor predeterminado.<br /><br /> SQL_CP_RELAXED_MATCH: se pueden utilizar conexiones con palabras clave de cadena de conexión coincidentes. Las palabras clave deben coincidir, pero no todos los atributos de conexión deben coincidir.<br /><br /> Para obtener más información acerca de cómo el Administrador de controladores realiza la coincidencia al conectarse a una conexión agrupada, vea [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md). Para obtener más información acerca de la agrupación de conexiones, vea Agrupación de [conexiones ODBC](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md).|  
|SQL_ATTR_ODBC_VERSION (ODBC 3.0)|Entero de 32 bits que determina si cierta funcionalidad muestra el comportamiento ODBC *2.x* o ODBC *3.x.* Los siguientes valores se utilizan para establecer el valor de este atributo:<br /><br /> SQL_OV_ODBC3_80: el Administrador de controladores y el controlador muestran el siguiente comportamiento de ODBC 3.8:<br /><br /> - El controlador devuelve y espera códigos ODBC *3.x* para la fecha, hora y marca de tiempo.<br />- El controlador devuelve códigos SQLSTATE ODBC *3.x* cuando se llama a **SQLError**, **SQLGetDiagField**o **SQLGetDiagRec** .<br />- El *CatalogName* argumento en una llamada a **SQLTables** acepta un patrón de búsqueda.<br />- El Administrador de controladores admite la extensibilidad del tipo de datos C. Para obtener más información acerca de la extensibilidad de tipos de datos de C, vea Tipos de [datos de C en ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).<br /><br /> Para obtener más información, vea [Novedades de ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md).<br /><br /> SQL_OV_ODBC3: el Administrador de controladores y el controlador muestran el siguiente comportamiento odbc *3.x:*<br /><br /> - El controlador devuelve y espera códigos ODBC *3.x* para la fecha, hora y marca de tiempo.<br />- El controlador devuelve códigos SQLSTATE ODBC *3.x* cuando se llama a **SQLError**, **SQLGetDiagField**o **SQLGetDiagRec** .<br />- El *CatalogName* argumento en una llamada a **SQLTables** acepta un patrón de búsqueda.<br />- El Administrador de controladores no admite la extensibilidad del tipo de datos C.<br /><br /> SQL_OV_ODBC2: el Administrador de controladores y el controlador muestran el siguiente comportamiento ODBC *2.x.* Esto es especialmente útil para una aplicación ODBC *2.x* que trabaja con un controlador ODBC *3.x.*<br /><br /> - El controlador devuelve y espera códigos ODBC *2.x* para la fecha, hora y marca de tiempo.<br />- El controlador devuelve códigos SQLSTATE ODBC *2.x* cuando se llama a **SQLError**, **SQLGetDiagField**o **SQLGetDiagRec** .<br />- El *CatalogName* argumento en una llamada a **SQLTables** no acepta un patrón de búsqueda.<br />- El Administrador de controladores no admite la extensibilidad del tipo de datos C.<br /><br /> Una aplicación debe establecer este atributo de entorno antes de llamar a cualquier función que tenga un argumento SQLHENV, o la llamada devolverá SQLSTATE HY010 (error de secuencia de funciones). Es específico del conductor si existe un comportamiento adicional para estas marcas ambientales.<br /><br /> - Para obtener más información, consulte [Declarar la versión ODBC](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md) de la aplicación y los [cambios](../../../odbc/reference/develop-app/behavioral-changes.md)de comportamiento .|  
|SQL_ATTR_OUTPUT_NTS (ODBC 3.0)|Entero de 32 bits que determina cómo el controlador devuelve datos de cadena. Si SQL_TRUE, el controlador devuelve datos de cadena terminados en null. Si SQL_FALSE, el controlador no devuelve datos de cadena terminados en null.<br /><br /> El valor predeterminado de este atributo es SQL_TRUE. Una llamada a **SQLSetEnvAttr** para establecerlo en SQL_TRUE devuelve SQL_SUCCESS. Una llamada a **SQLSetEnvAttr** para establecerlo en SQL_FALSE devuelve SQL_ERROR y SQLSTATE HYC00 (característica opcional no implementada).|  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Asignación de un asa|[Función SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Devolver la configuración de un atributo de entorno|[Función SQLGetEnvAttr](../../../odbc/reference/syntax/sqlgetenvattr-function.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Novedades de ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
