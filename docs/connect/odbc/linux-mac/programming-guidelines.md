---
title: "Instrucciones de programación | Documentos de Microsoft"
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
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 7bdb349022f82d29045c7277185485b595675bc3
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/01/2017
---
# <a name="programming-guidelines"></a>Instrucciones de programación

[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Las características de programación de la [!INCLUDE[msCoName](../../../includes/msconame_md.md)] ODBC Driver 13 y 13.1 para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] en Mac OS y Linux se basan en el controlador ODBC en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] Native Client ([SQL Server Native Client (ODBC)](http://go.microsoft.com/fwlink/?LinkID=134151)). [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]Native Client se basa en el controlador ODBC en Windows Data Access Components ([referencia del programador de ODBC](http://go.microsoft.com/fwlink/?LinkID=45250)).  

Puede usar una aplicación ODBC Multiple Active Result Sets (MARS) y otros [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] características específicas mediante la inclusión de `/usr/local/include/msodbcsql.h` después de incluir los encabezados de unixODBC (`sql.h`, `sqlext.h`, `sqltypes.h`, y `sqlucode.h`). A continuación, utilice los mismos nombres simbólicos para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]-elementos específicos que lo haría en las aplicaciones ODBC de Windows.  

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
-   [Resolución IP de red transparente](https://docs.microsoft.com/en-us/sql/connect/odbc/linux/using-transparent-network-ip-resolution)
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

El controlador admite datos SQLCHAR en uno de los juegos de caracteres siguientes:

  -  UTF-8
  -  CP437
  -  CP850
  -  CP874
  -  CP932
  -  CP936
  -  CP949
  -  CP950
  -  CP1251
  -  CP1253
  -  CP1256
  -  CP1257
  -  CP1258
  -  ISO-8859-1 / CP1252
  -  ISO-8859-2 / CP1250
  -  ISO-8859-3
  -  ISO-8859-4
  -  ISO-8859-5
  -  ISO-8859-6
  -  ISO-8859-7
  -  ISO-8859-8 / CP1255
  -  ISO-8859-9 / CP1254
  -  ISO-8859-13
  -  ISO-8859-15

Tras la conexión, el controlador detecta la configuración regional actual del proceso que se carga en. Si es una de las codificaciones admitidas anteriores, el controlador utilizará esa codificación para los datos SQLCHAR (caracteres estrechos); en caso contrario, el valor predeterminado es UTF-8. Dado que todos los procesos de inicio en la configuración regional "C" de forma predeterminada (y, por tanto, hacer que el controlador predeterminado UTF-8), si una aplicación necesita utilizar una de las codificaciones anteriores, debe utilizar el **setlocale** función para establecer la configuración regional correctamente antes problema de conexión. ya sea especificando la configuración regional deseada explícitamente, o mediante una cadena vacía, por ejemplo, `setlocale(LC_ALL, "")`, para usar la configuración regional del entorno.

Los datos de SQLWCHAR deben tener la codificación UTF-16LE (Little Endian).

Si SQLDescribeParameter no especifica un tipo de datos SQL en el servidor, el controlador utilizará el especificado en el parámetro *ParameterType* de SQLBindParameter. Si se especifica un tipo SQL de caracteres estrechos, como SQL_VARCHAR, en SQLBindParameter, el controlador convierte los datos proporcionados desde la página de códigos de cliente en el valor predeterminado [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] página de códigos. (El valor predeterminado [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] página de códigos es normalmente 1252.) Si no se admite la página de códigos de cliente, se establecerá en UTF-8. En este caso, el controlador, a continuación, convierte los datos UTF-8 en la página de códigos predeterminada. No obstante, es posible que se pierdan datos. Si la página de códigos 1252 no puede representar un carácter, el controlador lo convertirá a un signo de interrogación ("?"). Para evitar esta pérdida de datos, especifique un tipo de carácter Unicode SQL, como SQL_NVARCHAR, en SQLBindParameter. En este caso, el controlador convierte los datos Unicode proporcionados en codificación UTF-8 a UTF-16 sin pérdida de datos.

Hay una diferencia de conversión de codificación de texto entre Windows y varias versiones de la biblioteca iconv de Linux y macOS. Datos de texto que se codifican en la página de códigos 1255 (hebreo) tienen un punto de código (0xCA) que tiene un comportamiento diferente tras la conversión. Convertir este carácter a Unicode en Windows, produce un punto de código UTF-16 de 0x05BA. Convertirlos a Unicode en Mac OS y Linux con libiconv versiones anteriores a 1.15 produce un punto de código UTF-16 de 0x00CA.

Cuando los caracteres multibyte UTF-8 o UTF-16 suplentes se dividen en búferes de SQLPutData, se producen daños en los datos. Los búferes se utilizan para transmitir datos de SQLPutData sin codificaciones de caracteres parciales.  

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
