---
title: Generar perfiles del rendimiento del controlador ODBC | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- profiling ODBC driver performance data [SQL Server Native Client]
- performance [ODBC]
- application statistics [ODBC]
- time statistics [ODBC]
- ODBC, performance data
- SQL Server Native Client ODBC driver, profiling performance data
- SQLPERF data structure
- statistical information [ODBC]
ms.assetid: 8f44e194-d556-4119-a759-4c9dec7ecead
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c15c8920d2a0188a7dbe517149dc369dea95522e
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2019
ms.locfileid: "73760708"
---
# <a name="profiling-odbc-driver-performance"></a>Generar perfiles del rendimiento del controlador ODBC
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  El controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client puede generar perfiles de dos tipos de datos de rendimiento:  
  
-   Consultas de ejecución prolongada.  
  
     El controlador puede escribir en un archivo de registro cualquier consulta que no reciba una respuesta del servidor dentro de un período especificado de tiempo. A continuación, los programadores de la aplicación o los administradores de la base de datos pueden examinar cada instrucción SQL registrada para determinar cómo mejorar su rendimiento.  
  
-   Datos del rendimiento del controlador.  
  
     El controlador puede registrar las estadísticas de rendimiento y escribirlas en un archivo o ponerlas a disposición de una aplicación mediante una estructura de datos específica del controlador denominada SQLPERF. El archivo que contiene las estadísticas de rendimiento es un archivo delimitado por tabuladores que se puede analizar fácilmente con cualquier hoja de cálculo que admita archivos delimitados por tabuladores, como Microsoft Excel.  
  
 Cualquiera de los tipos de generación de perfiles se puede activar del siguiente modo:  
  
-   Conectándose a un origen de datos que especifique el registro.  
  
-   Llamar a [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) para establecer los atributos específicos del controlador que controlan la generación de perfiles.  
  
 Cada proceso de la aplicación obtiene su propia copia del controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client y los perfiles se generan de forma global para la combinación de una copia del controlador y un proceso de la aplicación. Cuando algo en la aplicación activa la generación de perfiles, el proceso de generación de perfiles registra información de todas las conexiones activas en el controlador de esa aplicación. Se incluyen incluso las conexiones que no llamaron específicamente para la generación de perfiles.  
  
 Después de que el controlador ha abierto un registro de generación de perfiles (ya sea un registro de datos de rendimiento o de consultas de ejecución prolongada), no lo cierra hasta que el Administrador de controladores ODBC descargue el controlador, momento en que una aplicación libera todos los identificadores del entorno que abrió en el controlador. Si la aplicación abre un nuevo identificador del entorno, se carga una nueva copia del controlador. Si la aplicación se conecta entonces a un origen de datos que especifica el mismo archivo de registro o establece los atributos específicos del controlador para realizar el registro en el mismo archivo, el controlador sobrescribe el registro anterior.  
  
 Si una aplicación empieza a generar perfiles en un archivo de registro y una segunda aplicación intenta empezar a generar perfiles en el mismo archivo de registro, la segunda aplicación no puede registrar ningún dato de generación de perfiles. Si la segunda aplicación empieza a generar perfiles después de que la primera haya descargado su controlador, la segunda aplicación sobrescribirá el archivo de registro de la primera aplicación.  
  
 Si una aplicación se conecta a un origen de datos que tiene habilitada la generación de perfiles, el controlador devuelve SQL_ERROR si la aplicación llama a **SQLSetConnectOption** para iniciar el registro. Una llamada a **SQLGetDiagRec** devuelve lo siguiente:  
  
```  
SQLState: 01000, pfNative = 0  
ErrorMsg: [Microsoft][SQL Server Native Client]  
   An error has occurred during the attempt to access  
   the log file, logging disabled.  
```  
  
 El controlador deja de recopilar datos de rendimiento cuando se cierra un identificador de entorno. Si una aplicación de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client tiene varias conexiones, cada una con su propio identificador de entorno, el controlador dejará de recopilar datos de rendimiento cuando se cierre alguno de los identificadores de entorno asociados.  
  
 Los datos de rendimiento del controlador se pueden almacenar en la estructura de datos SQLPERF o registrar en un archivo delimitado por tabuladores. Los datos incluyen las siguientes categorías de estadísticas:  
  
-   Perfil de aplicación  
  
-   Conexión  
  
-   Red  
  
-   Time  
  
 En la siguiente tabla, las descripciones de los campos de la estructura de datos SQLPERF se aplican también a las estadísticas registradas en el archivo de registro de rendimiento.  
  
### <a name="application-profile-statistics"></a>Estadísticas de perfil de aplicación  
  
|Campo SQLPERF|Descripción|  
|-------------------|-----------------|  
|TimerResolution|Resolución mínima de la hora del reloj del servidor en milisegundos. Normalmente se indica como 0 (cero) y solo debe considerarse si el número notificado es grande. Si la resolución mínima del reloj del servidor es mayor que el intervalo probable para algunas de las estadísticas basadas en temporizador, esas estadísticas se podrían exagerar.|  
|SQLidu|Número de instrucciones INSERT, DELETE o UPDATE después de SQL_PERF_START.|  
|SQLiduRows|Número de instrucciones INSERT, DELETE o UPDATE después de SQL_PERF_START.|  
|SQLSelects|Número de instrucciones SELECT procesadas después de SQL_PERF_START.|  
|SQLSelectRows|Número de filas seleccionadas después de SQL_PERF_START.|  
|Transacciones|Número de transacciones de usuario después de SQL_PERF_START, incluidas las reversiones. Cuando una aplicación ODBC se ejecuta con SQL_AUTOCOMMIT_ON, cada comando se considera una transacción.|  
|SQLPrepares|Número de llamadas a la [función SQLPrepare](https://go.microsoft.com/fwlink/?LinkId=59360) después de SQL_PERF_START.|  
|ExecDirects|Número de llamadas **SQLExecDirect** después de SQL_PERF_START.|  
|SQLExecutes|Número de llamadas **SQLExecute** después de SQL_PERF_START.|  
|CursorOpens|Número de veces que el controlador ha abierto un cursor del servidor después de SQL_PERF_START.|  
|CursorSize|Número de filas en los conjuntos de resultados abiertos por los cursores después de SQL_PERF_START.|  
|CursorUsed|Número de filas recuperadas realmente mediante el controlador de los cursores después de SQL_PERF_START.|  
|PercentCursorUsed|Igual que CursorUsed/CursorSize. Por ejemplo, si una aplicación hace que el controlador abra un cursor de servidor para realizar "SELECT COUNT (*) FROM Authors", habrá 23 filas en el conjunto de resultados de la instrucción SELECT. Si la aplicación captura solo tres de estas filas, CursorUsed/CursorSize será 3/23, por lo que PercentCursorUsed será 13,043478.|  
|AvgFetchTime|Igual que SQLFetchTime/SQLFetchCount.|  
|AvgCursorSize|Igual que CursorSize/CursorOpens.|  
|AvgCursorUsed|Igual que CursorUsed/CursorOpens.|  
|SQLFetchTime|Cantidad acumulada de tiempo que tardaron en completarse las capturas de los cursores de servidor.|  
|SQLFetchCount|Número de capturas realizadas de los cursores del servidor después de SQL_PERF_START.|  
|CurrentStmtCount|Número de identificadores de instrucciones abiertos actualmente en todas las conexiones abiertas del controlador.|  
|MaxOpenStmt|Número máximo de identificadores de instrucciones abiertos simultáneamente después de SQL_PERF_START.|  
|SumOpenStmt|Número de identificadores de instrucciones que se han abierto después de SQL_PERF_START.|  
|**Estadísticas de conexión:**||  
|CurrentConnectionCount|Número actual de controladores de conexiones activas que la aplicación ha abierto en el servidor.|  
|MaxConnectionsOpened|Número máximo de controladores de conexiones simultáneas abiertos después de SQL_PERF_START.|  
|SumConnectionsOpened|Suma del número de controladores de conexión abiertos después de SQL_PERF_START.|  
|SumConnectionTime|Suma de la cantidad de tiempo que han estado abiertas todas las conexiones después de SQL_PERF_START. Por ejemplo, si una aplicación abrió 10 conexiones y mantuvo cada conexión durante 5 segundos, el valor de SumConnectionTime sería 50 segundos.|  
|AvgTimeOpened|Igual que SumConnectionsOpened/SumConnectionTime.|  
|**Estadísticas de red:**||  
|ServerRndTrips|Número de veces que el controlador envió comandos al servidor y obtuvo una respuesta.|  
|BuffersSent|Número de paquetes de flujo TDS que el controlador ha enviado a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] después de SQL_PERF_START. Los comandos grandes pueden tomar varios búferes, de modo que si se envía un comando grande al servidor y llena seis paquetes, ServerRndTrips en uno y BuffersSent se incrementa en seis.|  
|BuffersRec|Número de paquetes TDS recibidos por el controlador desde [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] después de que la aplicación empezase a utilizar el controlador.|  
|BytesSent|Número de bytes de datos enviados a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en paquetes TDS después de que la aplicación empezase a utilizar el controlador.|  
|BytesRec|Número de bytes de datos en paquetes TDS recibidos por el controlador de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] después de que la aplicación empezase a utilizar el controlador.|  
  
### <a name="time-statistics"></a>Estadísticas de tiempo  
  
|Campo SQLPERF|Descripción|  
|-------------------|-----------------|  
|msExecutionTime|Cantidad acumulada de tiempo que ha dedicado el controlador al procesamiento después de SQL_PERF_START, incluido el tiempo que ha pasado esperando respuestas del servidor.|  
|msNetworkServerTime|Cantidad acumulada de tiempo que el controlador ha pasado esperando respuestas del servidor.|  
  
## <a name="see-also"></a>Vea también  
   de [SQL Server Native Client &#40;ODBC&#41; ](../../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
 [Temas &#40;de procedimientos de generación de perfiles de rendimiento del controlador ODBC ODBC&#41;](../../../relational-databases/native-client-odbc-how-to/profiling-odbc-driver-performance-odbc.md)  
  
  
