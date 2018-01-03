---
title: "Función SQLSetEnvAttr | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLSetEnvAttr
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLSetEnvAttr
helpviewer_keywords: SQLSetEnvAttr function [ODBC]
ms.assetid: 0343241c-4b15-4d4b-aa2b-2e8ab5215cd2
caps.latest.revision: "38"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c8a70e7d7de19f4f69a79db56742938ca0d61344
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="sqlsetenvattr-function"></a>Función SQLSetEnvAttr
**Conformidad**  
 Versión introdujo: ODBC 3.0 normativas: ISO 92  
  
 **Resumen**  
 **SQLSetEnvAttr** establece atributos que controlan aspectos de los entornos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SQLRETURN SQLSetEnvAttr(  
     SQLHENV      EnvironmentHandle,  
     SQLINTEGER   Attribute,  
     SQLPOINTER   ValuePtr,  
     SQLINTEGER   StringLength);  
```  
  
## <a name="arguments"></a>Argumentos  
 *EnvironmentHandle*  
 [Entrada] Identificador de entorno.  
  
 *Atributo*  
 [Entrada] Atributo que se establecerá, aparecen en "Comentarios".  
  
 *ValuePtr*  
 [Entrada] Puntero a la capacidad de asociarse *atributo*. Dependiendo del valor de *atributo*, *ValuePtr* se ser un valor entero de 32 bits o señalar a una cadena de caracteres terminada en null.  
  
 *StringLength*  
 [Entrada] Si *ValuePtr* apunta a una cadena de caracteres o un búfer binario, este argumento debe ser la longitud de **ValuePtr*. Para los datos de cadena de caracteres, este argumento debe contener el número de bytes en la cadena.  
  
 Si *ValuePtr* es un entero, *StringLength* se omite.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLSetEnvAttr** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_ HANDLE_ENV y un *controlar* de *EnvironmentHandle*. En la tabla siguiente se enumera los valores SQLSTATE suelen ser devueltos por **SQLSetEnvAttr** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario. Si un controlador no es compatible con un atributo de entorno, se puede devolver el error solo durante el tiempo de conexión.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo de específicas del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01S02 DE SQLSTATE|Ha cambiado el valor de opción|El controlador no admitía el valor especificado en *ValuePtr* y sustituir un valor similar. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|HY000|Error general|Se produjo un error para que no hubo ninguna SQLSTATE específico y para el que se ha definido ningún SQLSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY009|Uso no válido del puntero null|El argumento de atributo identifica un atributo de entorno que requería un valor de cadena, y el *ValuePtr* argumento era un puntero nulo.|  
|HY010|Error de secuencia de función|(DM) se ha asignado un identificador de conexión en *EnvironmentHandle*.<br /><br /> (DM) **SQL_ATTR_ODBC_VERSION** no se estableció con **SQLSetEnvAttr** y *atributo* no es igual a **SQL_ATTR_ODBC_VERSION**. No es necesario establecer **SQL_ATTR_ODBC_VERSION** explícitamente si utilizas **SQLAllocHandleStd**.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos subyacentes de la memoria no se pudieron tener acceso, posiblemente debido a condiciones de memoria insuficiente.|  
|HY024|Valor de atributo no válido|Dada la especificado *atributo* valor, que se especificó un valor no válido en *ValuePtr*.|  
|HY090|Longitud de búfer o cadena no válida|El *StringLength* argumento era menor que 0 pero no SQL_NTS.|  
|HY092|Identificador de opción o atributo no válido|(DM) el valor especificado para el argumento *atributo* no era válido para la versión de ODBC compatible con el controlador.|  
|HY117|Se suspende la conexión debido al estado de transacción desconocido. Solo se desconecte y se permiten las funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Característica opcional no implementada|El valor especificado para el argumento *atributo* era un atributo válido de entorno de ODBC para el controlador es compatible con la versión de ODBC, pero no era compatible con el controlador.<br /><br /> (DM) la *atributo* argumento era SQL_ATTR_OUTPUT_NTS, y *ValuePtr* era SQL_FALSE.|  
  
## <a name="comments"></a>Comentarios  
 Una aplicación puede llamar a **SQLSetEnvAttr** solo si no hay ningún identificador de conexión se asigna en el entorno. Todos los atributos de entorno definidos correctamente para la aplicación para el entorno se conservan hasta que **SQLFreeHandle** se llama en el entorno. Se puede asignar más de un identificador de entorno al mismo tiempo en ODBC 3*.x*.  
  
 Establece el formato de información a través de *ValuePtr* depende especificado *atributo*. **SQLSetEnvAttr** aceptará información de atributos en uno de dos formatos diferentes: una cadena de caracteres terminada en null o un valor entero de 32 bits. El formato de cada uno se indica en la descripción del atributo.  
  
 No hay ningún atributo de entorno específicas del controlador.  
  
 No se puede establecer atributos de conexión mediante una llamada a **SQLSetEnvAttr**. Intenta hacer esto devolverá SQLSTATE HY092 (identificador de atributo u opción no válido).  
  
|*Atributo*|*ValuePtr* contenido|  
|-----------------|-------------------------|  
|SQL_ATTR_CONNECTION_POOLING (ODBC 3.8)|Un valor SQLUINTEGER de 32 bits que habilita o deshabilita la agrupación de conexiones en el nivel de entorno. Se utilizan los siguientes valores:<br /><br /> SQL_CP_OFF = conexión de agrupación se ha desactivado. Ésta es la opción predeterminada.<br /><br /> SQL_CP_ONE_PER_DRIVER = un solo se admite la agrupación de conexiones para cada controlador. Todas las conexiones en un grupo está asociada a un controlador.<br /><br /> SQL_CP_ONE_PER_HENV = un solo se admite la agrupación de conexiones para cada entorno. Todas las conexiones en un grupo está asociada a un entorno.<br /><br /> SQL_CP_DRIVER_AWARE = utilizar la característica de reconocimiento de la agrupación de conexiones del controlador, si está disponible. Si el controlador no es compatible con el conocimiento de la agrupación de conexiones, SQL_CP_DRIVER_AWARE se omite y se utiliza SQL_CP_ONE_PER_HENV. Para obtener más información, consulte [agrupación de conexiones dependientes del controlador](../../../odbc/reference/develop-app/driver-aware-connection-pooling.md). En un entorno donde algunos controladores admiten y algunos controladores no son compatibles con el conocimiento de la agrupación de conexiones, SQL_CP_DRIVER_AWARE puede habilitar la característica de reconocimiento de agrupación de conexiones en aquellas que admiten controladores, pero es equivalente a establecer para SQL_CP_ONE_PER_HENV en los controladores que no admiten la característica de reconocimiento de la agrupación de conexiones.<br /><br /> Agrupación de conexiones está habilitada mediante una llamada a **SQLSetEnvAttr** para establecer el atributo SQL_ATTR_CONNECTION_POOLING en SQL_CP_ONE_PER_DRIVER o SQL_CP_ONE_PER_HENV. Esta llamada se debe realizar antes de que la aplicación asigna el entorno compartido para qué conexión agrupación es esté habilitado. El identificador de entorno en la llamada a **SQLSetEnvAttr** se establece en null, lo que hace SQL_ATTR_CONNECTION_POOLING un atributo de nivel de proceso. Después de habilita la agrupación de conexiones, la aplicación, a continuación, asigna un entorno compartido implícito mediante una llamada a **SQLAllocHandle** con el *InputHandle* establecido en SQL_HANDLE_ENV.<br /><br /> Después de que se ha habilitado la agrupación de conexiones y un entorno compartido se ha seleccionado para una aplicación, no se puede restablecer SQL_ATTR_CONNECTION_POOLING para ese entorno, porque **SQLSetEnvAttr** se llama con un entorno de null identificador al establecer este atributo. Si este atributo se establece cuando la agrupación de conexiones ya está habilitada en un entorno compartido, el atributo afecta a solo los entornos compartidos que se asignan posteriormente.<br /><br /> También es posible habilitar la agrupación de conexiones en un entorno. Tenga en cuenta lo siguiente acerca de la agrupación de conexiones de entorno:<br /><br /> -Habilitar un identificador nulo de agrupación de conexiones es un atributo de nivel de proceso. Entornos posteriormente asignados serán un entorno compartido y heredarán la configuración de la agrupación de conexiones de nivel de proceso.<br />-Después de haber asignado un entorno, una aplicación puede cambiar su configuración de la agrupación de conexiones.<br />-Si está habilitada la agrupación de conexiones de entorno y controlador de la conexión utiliza la agrupación de controlador, la agrupación de entorno tiene preferencia.<br /><br /> SQL_ATTR_CONNECTION_POOLING se implementa en el Administrador de controladores. Un controlador no necesita implementar SQL_ATTR_CONNECTION_POOLING. ODBC 2.0 y 3.0 aplicaciones pueden establecer este atributo del entorno.<br /><br /> Para obtener más información, consulte [agrupación de conexiones ODBC](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md).|  
|SQL_ATTR_CP_MATCH (ODBC 3.0)|Un valor SQLUINTEGER de 32 bits que determina cómo se elige una conexión de un grupo de conexiones. Cuando **SQLConnect** o **SQLDriverConnect** es llama, el Administrador de controladores determina qué conexión se vuelve a utilizar desde el grupo. El Administrador de controladores intenta hacer coincidir las opciones de conexión de la llamada y los atributos de conexión establecidos por la aplicación a las palabras clave y los atributos de conexión de las conexiones en el grupo. El valor de este atributo determina el nivel de precisión de los criterios de coincidencia.<br /><br /> Los siguientes valores se utilizan para establecer el valor de este atributo:<br /><br /> SQL_CP_STRICT_MATCH = sólo las conexiones que coincidan exactamente con las opciones de conexión en la llamada y la conexión se reutilizan atributos establecidos por la aplicación. Ésta es la opción predeterminada.<br /><br /> SQL_CP_RELAXED_MATCH = conexiones con la coincidencia de cadena de conexión se pueden usar palabras clave. Debe coincidir con palabras clave, pero no todos los atributos de conexión deben coincidir.<br /><br /> Para obtener más información acerca de cómo el Administrador de controladores realiza la búsqueda de coincidencias en conectarse a una conexión agrupada, consulte [SQLConnect](../../../odbc/reference/syntax/sqlconnect-function.md). Para obtener más información acerca de la agrupación de conexiones, vea [agrupación de conexiones ODBC](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md).|  
|SQL_ATTR_ODBC_VERSION (ODBC 3.0)|Un entero de 32 bits que determina si ciertas funciones exhibe ODBC 2*.x* comportamiento u ODBC 3*.x* comportamiento. Los siguientes valores se utilizan para establecer el valor de este atributo:<br /><br /> SQL_OV_ODBC3_80 = el Administrador de controladores y el comportamiento del documento la siguiente ODBC 3.8 de controlador:<br /><br /> -El controlador devuelve y espera que ODBC 3. *x* códigos de fecha, hora y marca de tiempo.<br />-El controlador devuelve ODBC 3. *x* códigos SQLSTATE cuando **SQLError**, **SQLGetDiagField**, o **SQLGetDiagRec** se llama.<br />-El *CatalogName* argumento en una llamada a **SQLTables** acepta un patrón de búsqueda.<br />-El Administrador de controladores admite C extensibilidad del tipo de datos. Para obtener más información acerca de la extensibilidad del tipo de datos de C, vea [tipos de datos C en ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).<br /><br /> Para obtener más información, consulte [What's New en ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md).<br /><br /> SQL_OV_ODBC3 = el Administrador de controladores y exposición de controlador el 3 de ODBC siguiente*.x* comportamiento:<br /><br /> -El controlador devuelve y espera que ODBC 3*.x* códigos de fecha, hora y marca de tiempo.<br />-El controlador devuelve ODBC 3*.x* códigos SQLSTATE cuando **SQLError**, **SQLGetDiagField**, o **SQLGetDiagRec** se llama.<br />-El *CatalogName* argumento en una llamada a **SQLTables** acepta un patrón de búsqueda.<br />-El Administrador de controladores no es compatible con la extensibilidad del tipo de datos C.<br /><br /> SQL_OV_ODBC2 = el Administrador de controladores y presenten las siguientes 2 de ODBC de controlador*.x* comportamiento. Esto es especialmente útil para una API ODBC 2*.x* aplicación trabajar con una aplicación ODBC 3*.x* controlador.<br /><br /> -El controlador devuelve y espera ODBC 2*.x* códigos de fecha, hora y marca de tiempo.<br />-El controlador devuelve 2 de ODBC*.x* códigos SQLSTATE cuando **SQLError**, **SQLGetDiagField**, o **SQLGetDiagRec** se llama.<br />-El *CatalogName* argumento en una llamada a **SQLTables** no acepta un patrón de búsqueda.<br />-El Administrador de controladores no es compatible con la extensibilidad del tipo de datos C.<br /><br /> Una aplicación debe establecer este atributo entorno antes de llamar a cualquier función que tiene un argumento SQLHENV o la llamada devolverá SQLSTATE HY010 (error de secuencia de función). Es si existe un comportamiento adicional para estos indicadores medioambientales específicos del controlador.<br /><br /> -Para obtener más información, consulte [declarar ODBC versión la aplicación](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md) y [cambios de comportamiento](../../../odbc/reference/develop-app/behavioral-changes.md).|  
|SQL_ATTR_OUTPUT_NTS (ODBC 3.0)|Un entero de 32 bits que determina cómo el controlador devuelve datos de cadena. Si es SQL_TRUE, el controlador devuelve datos de la cadena terminada en null. Si SQL_FALSE, el controlador no devuelve datos de la cadena terminada en null.<br /><br /> El valor predeterminado de este atributo es SQL_TRUE. Una llamada a **SQLSetEnvAttr** establecerlo en SQL_TRUE devuelve SQL_SUCCESS. Una llamada a **SQLSetEnvAttr** establecerlo en los devuelve SQL_FALSE SQL_ERROR y SQLSTATE HYC00 (característica opcional no implementada).|  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Asignar un identificador|[Función SQLAllocHandle](../../../odbc/reference/syntax/sqlallochandle-function.md)|  
|Devolver el valor de un atributo de entorno|[Función SQLGetEnvAttr](../../../odbc/reference/syntax/sqlgetenvattr-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Novedades de ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md)
