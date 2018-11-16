---
title: Instrucciones de programación (controlador ODBC para SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 01/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2edaeee9d073cb0c12a509bd23e3db9edf4b3894
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 11/13/2018
ms.locfileid: "51602190"
---
# <a name="programming-guidelines"></a>Instrucciones de programación

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Las características de programación de [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 11 for [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en macOS y Linux se basan en ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ([SQL Server Native Client (ODBC)](https://go.microsoft.com/fwlink/?LinkID=134151)). [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client se basa en ODBC de los Componentes de Windows Data Access ([Referencia del programador de ODBC](https://go.microsoft.com/fwlink/?LinkID=45250)).  

Puede usar una aplicación ODBC Multiple Active Result Sets (MARS) y otros [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] características específicas mediante la inclusión de `/usr/local/include/msodbcsql.h` después de incluir los encabezados de unixODBC (`sql.h`, `sqlext.h`, `sqltypes.h`, y `sqlucode.h`). Luego use los mismos nombres simbólicos para los elementos específicos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que usaría en las aplicaciones de ODBC para Windows.

## <a name="available-features"></a>Características disponibles  
Las siguientes secciones de la documentación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client para ODBC ([SQL Server Native Client (ODBC)](https://go.microsoft.com/fwlink/?LinkID=134151)) son válidas cuando se usa el controlador ODBC en macOS y Linux:  

-   [Comunicar con SQL Server (ODBC)](https://msdn.microsoft.com/library/ms131692.aspx)  
-   [Compatibilidad con el tiempo de espera de la conexión y consulta](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)  
-   [Cursores](../../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)  
-   [Mejoras en los tipos de datos de fecha y hora (ODBC)](https://msdn.microsoft.com/library/bb677319.aspx)  
-   [Ejecutar consultas (ODBC)](https://msdn.microsoft.com/library/ms131677.aspx)  
-   [Controlar errores y mensajes](../../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
-   [Autenticación Kerberos](../../../relational-databases/native-client/features/service-principal-name-spn-support-in-client-connections.md)  
-   [Tipos CLR grandes definidos por el usuario (ODBC)](https://msdn.microsoft.com/library/bb677316.aspx)  
-   [Realización de transacciones (ODBC) (excepto las transacciones distribuidas)](https://msdn.microsoft.com/library/ms131706.aspx)  
-   [Procesar resultados (ODBC)](https://msdn.microsoft.com/library/ms130812.aspx)  
-   [Ejecutar procedimientos almacenados](../../../relational-databases/native-client-odbc-stored-procedures/running-stored-procedures.md)
-   [Compatibilidad con columnas dispersas (ODBC)](https://msdn.microsoft.com/library/cc280357.aspx)
-   [Cifrado SSL](../../../relational-databases/native-client/features/using-encryption-without-validation.md)
-   [Parámetros con valores de tabla](https://docs.microsoft.com/sql/relational-databases/native-client-odbc-table-valued-parameters/table-valued-parameters-odbc)
-   [UTF-8 y UTF-16 para la API de datos y comandos](https://msdn.microsoft.com/library/ff878241.aspx)
-   [Utilizar funciones de catálogo](../../../relational-databases/native-client/odbc/using-catalog-functions.md)  

## <a name="unsupported-features"></a>Características no admitidas

Las siguientes características no se ha comprobado que funciona correctamente en esta versión del controlador ODBC en macOS y Linux:

-   Conexión de clúster de conmutación por error
-   [Resolución de direcciones IP de red transparente](https://docs.microsoft.com/sql/connect/odbc/linux/using-transparent-network-ip-resolution) (antes del controlador ODBC de 17)
-   [Seguimiento de controlador avanzado](https://blogs.msdn.microsoft.com/mattn/2012/05/15/enabling-advanced-driver-tracing-for-the-sql-native-client-odbc-drivers/)

Las siguientes características no están disponibles en esta versión del controlador ODBC en macOS y Linux: 

-   Transacciones distribuidas (no se admite el atributo SQL_ATTR_ENLIST_IN_DTC)  
-   Creación de reflejo de base de datos  
-   FILESTREAM  
-   Generación de perfiles de rendimiento del controlador ODBC, que se describe en [SQLSetConnectAttr](https://go.microsoft.com/fwlink/?LinkId=234099), y los siguientes atributos de conexión relacionados con el rendimiento:  
    -   SQL_COPT_SS_PERF_DATA  
    -   SQL_COPT_SS_PERF_DATA_LOG  
    -   SQL_COPT_SS_PERF_DATA_LOG_NOW  
    -   SQL_COPT_SS_PERF_QUERY  
    -   SQL_COPT_SS_PERF_QUERY_INTERVAL  
    -   SQL_COPT_SS_PERF_QUERY_LOG  
-   SQLBrowseConnect  
-   Los tipos de intervalo de C como SQL_C_INTERVAL_YEAR_TO_MONTH (se trata en [Identificadores y descriptores de tipo de datos](https://msdn.microsoft.com/library/ms716351(VS.85).aspx))
-   El valor SQL_CUR_USE_ODBC del atributo SQL_ATTR_ODBC_CURSORS de la función SQLSetConnectAttr.

## <a name="character-set-support"></a>Compatibilidad con juegos de caracteres

Para ODBC Driver 13 y 13.1, datos SQLCHAR deben ser UTF-8. No hay otras codificaciones se admiten.

Para ODBC Driver 17, se admiten los datos SQLCHAR de uno de las siguientes conjuntos/codificaciones de caracteres:

|Nombre|Descripción|
|-|-|
|UTF-8|Unicode|
|CP437|MS-DOS Latin EE. UU.|
|CP850|MS-DOS Latín 1|
|CP874|Alfabeto latino/tailandés|
|CP932|Japonés, Shift-JIS|
|CP936|Chino simplificado, GBK|
|CP949|Coreano, EUC-KR|
|CP950|Chino tradicional, Big5|
|CP1251|Cirílico|
|CP1253|Greek|
|CP1256|Árabe|
|CP1257|Báltico|
|CP1258|Vietnamita|
|ISO-8859-1 / CP1252|Latín-1|
|ISO-8859-2 / CP1250|Latín-2|
|ISO-8859-3|Latín-3|
|ISO-8859-4|Latín-4|
|ISO-8859-5|Latino/cirílico|
|ISO-8859-6|Latín y árabe|
|ISO-8859-7|Latino/griego|
|ISO-8859-8 / CP1255|Hebreo|
|ISO-8859-9 / CP1254|Turco|
|ISO-8859-13|Latín-7|
|ISO-8859-15|Latín 9|

Al establecer la conexión, el controlador detecta la configuración regional actual del proceso que se carga en. Si utiliza una de las codificaciones anteriores, el controlador utiliza esa codificación para los datos SQLCHAR (caracteres estrechos); en caso contrario, el valor predeterminado es UTF-8. Dado que todos los procesos iniciarse de forma predeterminada en la configuración regional "C" (y, por tanto, provocar que el controlador de forma predeterminada en UTF-8), si una aplicación necesita utilizar una de las codificaciones anteriores, debe usar el **setlocale** función para establecer correctamente antes de la configuración regional problema de conexión. ya sea especificando la configuración regional deseada explícitamente, o mediante una cadena vacía como `setlocale(LC_ALL, "")` para usar la configuración regional del entorno.

Por lo tanto, en un entorno típico de Linux o Mac que la codificación es UTF-8, los usuarios de la actualización de ODBC Driver 17 de 13 o 13.1 no observarán las diferencias. Sin embargo, las aplicaciones que usan una codificación no UTF-8 en la lista anterior a través de `setlocale()` debe usar esa codificación para los datos hacia y desde el controlador en lugar de UTF-8.

Los datos de SQLWCHAR deben tener la codificación UTF-16LE (Little Endian).

Al enlazar parámetros de entrada con SQLBindParameter, si un carácter estrecho SQL tipo, como se especifica SQL_VARCHAR, el controlador convierte los datos proporcionados desde el cliente de codificación con el valor predeterminado (normalmente, página de códigos 1252) [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] codificación. Para los parámetros de salida, el controlador convierte de la codificación especificada en la información de intercalación asociada con los datos para el cliente de codificación. Sin embargo, es posible pérdida de datos---caracteres en la codificación de origen no se puede representar en la codificación de destino, se convertirá en un signo de interrogación ("?").

Para evitar esta pérdida de datos al enlazar parámetros de entrada, especifique un tipo de carácter Unicode SQL, como SQL_NVARCHAR. En este caso, el controlador convierte desde el cliente de codificación en UTF-16, que puede representar todos los caracteres Unicode. Además, la columna de destino o el parámetro en el servidor debe ser también un tipo de Unicode (**nchar**, **nvarchar**, **ntext**) o uno con una intercalación/codificación, que puede representar todos los caracteres del origen de datos original. Para evitar la pérdida de datos con los parámetros de salida, especifique un tipo de Unicode SQL y un Unicode C tipo (SQL_C_WCHAR), provocando el controlador devolver datos como UTF-16; o una estrecha C escriba y asegúrese de que el cliente de codificación puede representar todos los caracteres del origen de datos (Esto siempre es posible con UTF-8.)

Para obtener más información sobre las intercalaciones y las codificaciones, vea [Compatibilidad con la intercalación y Unicode](../../../relational-databases/collations/collation-and-unicode-support.md).

Hay algunas diferencias de conversión de codificación entre Windows y varias versiones de la biblioteca iconv de Linux y macOS. Datos de texto en la página de códigos 1255 (hebreo) tienen un punto de código (0xCA) que se comporta de manera diferente durante la conversión a Unicode. En Windows, este carácter se convierte en el punto de código UTF-16 de 0x05BA. En macOS y Linux con versiones anteriores a 1.15 de libiconv, lo convierte en 0x00CA. En Linux con bibliotecas iconv que no admiten la revisión de 2003 de CP950/Big5 (denominado `BIG5-2003`), caracteres agregados con esa revisión no convertirá correctamente. En la página de códigos 932 (japonés, Shift-JIS), el resultado de la descodificación de caracteres definidos originalmente en el estándar de codificación también difiere. Por ejemplo, el byte 0 x 80 convierte a u+0080 en Windows, pero puede llegar a ser 30FB U + en Linux y macOS, dependiendo de la versión iconv.

En ODBC Driver 13 y 13.1, cuando los caracteres multibyte UTF-8 o UTF-16 suplentes se dividen en búferes de SQLPutData, se producen daños en los datos. Los búferes se utilizan para transmitir datos de SQLPutData sin codificaciones de caracteres parciales. Esta limitación se ha quitado con ODBC Driver 17.

## <a name="additional-notes"></a>Notas adicionales  

1.  Puede realizar una conexión de administrador dedicada (DAC) con la autenticación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y **host,port**. Un miembro de la función Sysadmin debe detectar primero el puerto DAC. Consulte [conexión de diagnóstico para administradores de base de datos](https://docs.microsoft.com/sql/database-engine/configure-windows/diagnostic-connection-for-database-administrators#dac-port) para descubrir cómo. Por ejemplo, si el puerto DAC fuera 33000, podría conectarse a él con `sqlcmd` de la siguiente forma:  

    ```
    sqlcmd –U <user> -P <pwd> -S <host>,33000
    ```

    > [!NOTE]  
    > Las conexiones DAC deben usar la autenticación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
    
2.  El Administrador de controladores unixODBC devuelve el mensaje "Identificador de opción o atributo no válido" en todos los atributos de instrucción cuando se transmiten a través de SQLSetConnectAttr. En Windows, cuando SQLSetConnectAttr recibe un valor de atributo de instrucción, el controlador tiene que establecer ese valor en todas las instrucciones activas que pertenecen al identificador de conexión.  

## <a name="see-also"></a>Ver también  
[Preguntas más frecuentes](../../../connect/odbc/linux-mac/frequently-asked-questions-faq-for-odbc-linux.md)

[Problemas conocidos en esta versión del controlador](../../../connect/odbc/linux-mac/known-issues-in-this-version-of-the-driver.md)

[Notas de la versión](../../../connect/odbc/linux-mac/release-notes.md)
