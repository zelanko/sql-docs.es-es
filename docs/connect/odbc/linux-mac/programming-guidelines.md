---
title: "Instrucciones de programación (controlador ODBC para SQL Server) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/11/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: fd8952f28f389fa5f1b8f82072998676c5a4196e
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2018
---
# <a name="programming-guidelines"></a>Instrucciones de programación

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Las características de programación de la [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] en Mac OS y Linux se basan en el controlador ODBC en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Native Client ([SQL Server Native Client (ODBC)](http://go.microsoft.com/fwlink/?LinkID=134151)). [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]Native Client se basa en el controlador ODBC en Windows Data Access Components ([referencia del programador de ODBC](http://go.microsoft.com/fwlink/?LinkID=45250)).  

Puede usar una aplicación ODBC Multiple Active Result Sets (MARS) y otros [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] características específicas mediante la inclusión de `/usr/local/include/msodbcsql.h` después de incluir los encabezados de unixODBC (`sql.h`, `sqlext.h`, `sqltypes.h`, y `sqlucode.h`). A continuación, utilice los mismos nombres simbólicos para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]-elementos específicos que se usan en las aplicaciones ODBC de Windows.

## <a name="available-features"></a>Características disponibles  
Las siguientes secciones de la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] documentación Native Client para ODBC ([SQL Server Native Client (ODBC)](http://go.microsoft.com/fwlink/?LinkID=134151)) son válidos cuando se utiliza el controlador ODBC en Mac OS y Linux:  

-   [Comunicar con SQL Server (ODBC)](http://msdn.microsoft.com/library/ms131692.aspx)  
-   [Compatibilidad de tiempo de espera de conexión y consulta](http://msdn.microsoft.com/library/ms130822.aspx)  
-   [Cursores](http://msdn.microsoft.com/library/ms130794(SQL.110).aspx)  
-   [Fecha y hora mejoras (ODBC)](http://msdn.microsoft.com/library/bb677319.aspx)  
-   [Ejecutar consultas (ODBC)](http://msdn.microsoft.com/library/ms131677.aspx)  
-   [Controlar errores y mensajes](http://msdn.microsoft.com/library/ms131289.aspx)  
-   [Autenticación Kerberos](http://msdn.microsoft.com/library/cc280459.aspx)  
-   [Tipos CLR grandes definidos por el usuario (ODBC)](http://msdn.microsoft.com/library/bb677316.aspx)  
-   [Realizar transacciones (ODBC) (excepto las transacciones distribuidas)](http://msdn.microsoft.com/library/ms131706.aspx)  
-   [Procesar resultados (ODBC)](http://msdn.microsoft.com/library/ms130812.aspx)  
-   [Ejecutar procedimientos almacenados](http://msdn.microsoft.com/library/ms131440.aspx)
-   [Compatibilidad con columnas dispersas (ODBC)](http://msdn.microsoft.com/library/cc280357.aspx)
-   [Cifrado SSL](http://msdn.microsoft.com/library/ms131691.aspx)
-   [Parámetros con valores de tabla](https://docs.microsoft.com/en-us/sql/relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc)
-   [UTF-8 y UTF-16 para datos y comandos de API](http://msdn.microsoft.com/library/ff878241.aspx)
-   [Utilizar funciones de catálogo](http://msdn.microsoft.com/library/ms131490.aspx)  

## <a name="unsupported-features"></a>Características no admitidas

Las siguientes características no se han comprobado para que funcione correctamente en esta versión del controlador ODBC en Mac OS y Linux:

-   Conexión de clúster de conmutación por error
-   [Resolución IP de red transparente](https://docs.microsoft.com/en-us/sql/connect/odbc/linux/using-transparent-network-ip-resolution) (antes del controlador ODBC 17)
-   [Seguimiento de controlador avanzado](https://blogs.msdn.microsoft.com/mattn/2012/05/15/enabling-advanced-driver-tracing-for-the-sql-native-client-odbc-drivers/)

Las siguientes características no están disponibles en esta versión del controlador ODBC en Mac OS y Linux: 

-   Las transacciones distribuidas (no se admite el atributo SQL_ATTR_ENLIST_IN_DTC)  
-   Creación de reflejo de base de datos  
-   FILESTREAM  
-   Generación de perfiles de rendimiento del controlador ODBC, se describe en [SQLSetConnectAttr](http://go.microsoft.com/fwlink/?LinkId=234099)y los siguientes atributos de conexión relacionados con el rendimiento:  
    -   SQL_COPT_SS_PERF_DATA  
    -   SQL_COPT_SS_PERF_DATA_LOG  
    -   SQL_COPT_SS_PERF_DATA_LOG_NOW  
    -   SQL_COPT_SS_PERF_QUERY  
    -   SQL_COPT_SS_PERF_QUERY_INTERVAL  
    -   SQL_COPT_SS_PERF_QUERY_LOG  
-   SQLBrowseConnect  
-   Tipos de intervalo de C como SQL_C_INTERVAL_YEAR_TO_MONTH (documentados en [identificadores de tipo de datos y los descriptores de](http://msdn.microsoft.com/library/ms716351(VS.85).aspx))
-   El valor SQL_CUR_USE_ODBC del atributo SQL_ATTR_ODBC_CURSORS de la función SQLSetConnectAttr.

## <a name="character-set-support"></a>Compatibilidad de conjunto de caracteres

Para ODBC Driver 13 y 13.1, los datos SQLCHAR deben ser UTF-8. No hay otras codificaciones se admiten.

Para 17 del controlador ODBC se admiten datos SQLCHAR de uno de las conjuntos/codificaciones de caracteres siguientes:

|Nombre|Description|
|-|-|
|UTF-8|Unicode|
|CP437|MS-DOS Latín EE. UU.|
|CP850|MS-DOS Latín 1|
|CP874|Alfabeto latino/tailandés|
|CP932|Japonés, Shift-JIS|
|CP936|Chino simplificado GBK|
|CP949|Coreano, EUC-KR|
|CP950|Chino tradicional Big5|
|CP1251|Cirílico|
|CP1253|Greek|
|CP1256|Árabe|
|CP1257|Báltico|
|CP1258|Vietnamita|
|ISO-8859-1 / CP1252|Latín-1|
|ISO-8859-2 / CP1250|Latín-2|
|ISO-8859-3|Latín-3|
|ISO-8859-4|Latín-4|
|ISO-8859-5|Alfabeto latino/cirílico|
|ISO-8859-6|Alfabeto latino/árabe|
|ISO-8859-7|Alfabeto latino/griego|
|ISO-8859-8 / CP1255|Hebreo|
|ISO-8859-9 / CP1254|Turco|
|ISO-8859-13|Latin-7|
|ISO-8859-15|Latín 9|

Tras la conexión, el controlador detecta la configuración regional actual del proceso que se carga en. Si utiliza una de las codificaciones anteriores, el controlador utiliza esa codificación para los datos SQLCHAR (caracteres estrechos); en caso contrario, el valor predeterminado es UTF-8. Dado que todos los procesos de inicio en la configuración regional "C" de forma predeterminada (y, por tanto, hacer que el controlador predeterminado UTF-8), si una aplicación necesita utilizar una de las codificaciones anteriores, debe utilizar el **setlocale** función para establecer la configuración regional correctamente antes problema de conexión. especificar la configuración regional deseada explícitamente, o mediante una cadena vacía como `setlocale(LC_ALL, "")` para usar la configuración regional del entorno.

Por lo tanto, en un entorno típico de Linux o Mac que la codificación es UTF-8, los usuarios de la actualización de 17 del controlador ODBC de 13 ó 13.1 no advertirán las diferencias. Sin embargo, las aplicaciones que utilizan una codificación no UTF-8 en la lista anterior a través de `setlocale()` que deba usar esa codificación de datos hacia/desde el controlador en lugar de UTF-8.

Los datos de SQLWCHAR deben tener la codificación UTF-16LE (Little Endian).

Al enlazar parámetros de entrada con SQLBindParameter, si un carácter estrecho SQL tipo como SQL_VARCHAR se especifica, el controlador convierte los datos proporcionados desde el cliente de codificación con el valor predeterminado (normalmente página de códigos 1252) [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] codificación. Para los parámetros de salida, el controlador convierte de la codificación especificada en la información de intercalación asociada con los datos para el cliente de codificación. Sin embargo, es posible pérdida de datos---caracteres en la codificación de origen no se puede representar en la codificación de destino, se convertirá en un signo de interrogación ('? ').

Para evitar esta pérdida de datos al enlazar parámetros de entrada, especificar un tipo de carácter Unicode SQL, como SQL_NVARCHAR. En este caso, el controlador convierte desde el cliente de codificación a UTF-16, que puede representar todos los caracteres Unicode. Además, la columna de destino o el parámetro en el servidor debe ser también un tipo de Unicode (**nchar**, **nvarchar**, **ntext**) o uno con una intercalación/codificación, que puede representar todos los caracteres del origen de datos original. Para evitar la pérdida de datos con parámetros de salida, especifique un tipo de Unicode SQL y una Unicode C escriba (SQL_C_WCHAR), haciendo que el controlador devolver los datos como UTF-16; o una estrecha C escriba y asegúrese de que el cliente de codificación puede representar todos los caracteres del origen de datos (Esto siempre es posible con UTF-8.)

Para obtener más información acerca de intercalaciones y codificaciones, vea [Collation and Unicode Support](../../../relational-databases/collations/collation-and-unicode-support.md).

Hay algunas diferencias de conversión de codificación entre Windows y varias versiones de la biblioteca iconv de Linux y macOS. Datos de texto en la página de códigos 1255 (hebreo) tienen un punto de código (0xCA) que tiene un comportamiento diferente tras la conversión a Unicode. En Windows, este carácter se convierte en el punto de código UTF-16 de 0x05BA. En Mac OS y Linux con las versiones de libiconv anteriores a 1.15, convierte en 0x00CA. En Linux con iconv bibliotecas que son compatibles con la revisión de 2003 de Big5/CP950 (denominado `BIG5-2003`), no se convertirán correctamente caracteres agregados con esa revisión.

En ODBC Driver 13 y 13.1, cuando los caracteres multibyte UTF-8 o UTF-16 suplentes se dividen en búferes de SQLPutData, se producen daños en los datos. Los búferes se utilizan para transmitir datos de SQLPutData sin codificaciones de caracteres parciales. Se ha quitado esta limitación con 17 del controlador ODBC.

## <a name="additional-notes"></a>Notas adicionales  

1.  Puede realizar una conexión de administrador dedicada (DAC) con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] autenticación y **host, puerto**. Un miembro de la función Sysadmin debe detectar primero el puerto DAC. Vea [conexión de diagnóstico para administradores de base de datos](https://docs.microsoft.com/en-us/sql/database-engine/configure-windows/diagnostic-connection-for-database-administrators#dac-port) para descubrir cómo. Por ejemplo, si el puerto DAC fuera 33000, podría conectarse a él con `sqlcmd` como se indica a continuación:  

    ```
    sqlcmd –U <user> -P <pwd> -S <host>,33000
    ```

    > [!NOTE]  
    > Las conexiones DAC deben utilizar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] autenticación.  
    
2.  El Administrador de controladores unixODBC devuelve el mensaje "Identificador de opción o atributo no válido" en todos los atributos de instrucción cuando se transmiten a través de SQLSetConnectAttr. En Windows, cuando SQLSetConnectAttr recibe un valor de atributo de instrucción hace que el controlador tiene que establecer ese valor en todas las instrucciones activas que pertenecen al identificador de conexión.  

## <a name="see-also"></a>Vea también  
[Preguntas más frecuentes](../../../connect/odbc/linux-mac/frequently-asked-questions-faq-for-odbc-linux.md)

[Problemas conocidos en esta versión del controlador](../../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)

[Notas de la versión](../../../connect/odbc/linux-mac/release-notes.md)
