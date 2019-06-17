---
title: Creación de una aplicación SQL Server Native Client ODBC Driver | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC, architecture
- SQL Server Native Client ODBC driver, creating applications
- ODBC function calls
- ODBC, header files
- ODBC applications
- ODBC applications, creating
- SQL Server Native Client ODBC driver, extensions
- applications [SQL Server Native Client]
- SQL Server Native Client ODBC driver, ODBC architecture
- extensions [ODBC]
- ODBC, driver extensions
- function calls [ODBC]
ms.assetid: c83c36e2-734e-4960-bc7e-92235910bc6f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: db71e2ca03cbefdccf0bdf879fdb43d775125064
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63205265"
---
# <a name="creating-a-sql-server-native-client-odbc-driver-application"></a>Crear una aplicación de controlador ODBC de SQL Server Native Client
  La arquitectura de ODBC tiene cuatro componentes que se encargan de realizar las funciones siguientes.  
  
|Componente|Función|  
|---------------|--------------|  
|Application|Llama a las funciones ODBC para comunicarse con un origen de datos ODBC, envía instrucciones SQL y procesa los conjuntos de resultados.|  
|Administrador de controladores|Administra la comunicación entre una aplicación y todos los controladores ODBC usados por la aplicación.|  
|Controlador|Procesa todas las llamadas de función ODBC desde la aplicación, se conecta a un origen de datos, pasa instrucciones SQL de la aplicación al origen de datos y devuelve resultados a la aplicación. Si es necesario, el controlador traduce el SQL de ODBC de la aplicación al SQL nativo usado por el origen de datos.|  
|Origen de datos|Contiene toda la información que un controlador necesita para obtener acceso a una determinada instancia de datos en un DBMS.|  
  
 Una aplicación que utiliza el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client para comunicarse con una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] realiza las siguientes tareas:  
  
-   Se conecta con un origen de datos.  
  
-   Envía instrucciones SQL al origen de datos.  
  
-   Procesa los resultados de las instrucciones desde el origen de datos.  
  
-   Procesa errores y mensajes.  
  
-   Termina la conexión con el origen de datos.  
  
 Una aplicación más compleja escrita para la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client también podría realizar las tareas siguientes:  
  
-   Usar cursores para controlar la ubicación en un conjunto de resultados.  
  
-   Solicitar operaciones de confirmación o reversión para el control de transacciones.  
  
-   Realizar transacciones distribuidas que impliquen dos o más servidores.  
  
-   Ejecutar procedimientos almacenados en el servidor remoto.  
  
-   Llamar a funciones de catálogo para realizar consultas sobre los atributos de un conjunto de resultados.  
  
-   Realizar operaciones de copia masiva.  
  
-   Administrar datos de gran tamaño (**varchar (max)** , **nvarchar (max)** , y **varbinary (max)** columnas) las operaciones  
  
-   Usar la lógica de reconexión para facilitar la conmutación por error al configurar la creación de reflejo de la base de datos.  
  
-   Registrar datos de rendimiento y consultas de ejecución prolongada.  
  
 Para realizar llamadas a funciones ODBC, una aplicación C o C++ debe incluir los archivos de encabezado sql.h, sqlext.h y sqltypes.h. Para realizar llamadas a las funciones API del instalador ODBC, una aplicación debe incluir el archivo de encabezado odbcinst.h. Una aplicación ODBC Unicode debe incluir el archivo de encabezado sqlucode.h. Las aplicaciones ODBC deben estar vinculadas al archivo odbc32.lib. Las aplicaciones ODBC que llaman a las funciones API del instalador ODBC deben estar vinculadas al archivo odbccp32.lib. Estos archivos se incluyen en Windows Platform SDK.  
  
 Muchos controladores ODBC, incluido el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client, ofrecen extensiones ODBC específicas del controlador. Para aprovechar las ventajas de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] las extensiones específicas del controlador ODBC de Native Client, una aplicación deben incluir el archivo de encabezado sqlncli.h. Este archivo de encabezado incluye:  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Atributos de conexión específicos del controlador ODBC de cliente nativos.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Atributos de instrucción específicos del controlador ODBC de cliente nativos.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Atributos de columna específicos del controlador ODBC de cliente nativos.  
  
-   Tipos de datos específicos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Tipos de datos definidos por el usuario específicos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC específico del controlador [SQLGetInfo](../../native-client-odbc-api/sqlgetinfo.md) tipos.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Campos de diagnóstico de controlador ODBC de cliente nativos.  
  
-   Códigos de función dinámica de diagnóstico específicos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Definiciones de tipo de C/C++ para tipos de datos C nativos específicos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (que se devuelven cuando las columnas están enlazadas al tipo de datos C SQL_C_BINARY).  
  
-   Definición de tipo para la estructura de datos SQLPERF.  
  
-   Prototipos y macros de copia masiva para admitir el uso de la API de copia masiva a través de una conexión ODBC.  
  
-   Llame a las funciones API de metadatos de consulta distribuida para obtener listas de servidores vinculados y sus catálogos.  
  
 Cualquier aplicación ODBC de C o C++ que usa la característica de copia masiva de los [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client debe vincularse al archivo sqlncli11.lib. Las aplicaciones que llaman a las funciones API de metadatos de consulta distribuida también deben vincularse a sqlncli11.lib. Los archivos sqlncli.h y sqlncli11.lib se distribuyen como parte de la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] herramientas del programador. Los directorios Include y Lib de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deberían estar en las rutas de acceso LIB e INCLUDE del compilador, como en el siguiente ejemplo:  
  
```  
LIB=c:\Program Files\Microsoft Data Access SDK 2.8\Libs\x86\lib;C:\Program Files\Microsoft SQL Server\100\Tools\SDK\Lib;  
INCLUDE=c:\Program Files\Microsoft Data Access SDK 2.8\inc;C:\Program Files\Microsoft SQL Server\100\Tools\SDK\Include;  
```  
  
 Una decisión de diseño que se realiza al principio del proceso de generación de una aplicación es si la aplicación necesita tener varias llamadas ODBC pendientes al mismo tiempo. Hay dos métodos para admitir varias llamadas ODBC simultáneas, que se describen en los temas restantes en esta sección. Para obtener más información, consulte el [referencia del programador de ODBC](https://go.microsoft.com/fwlink/?LinkId=45250).  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Modo asincrónico y SQLCancel](../../native-client-odbc-api/sqlcancel.md)  
  
-   [Aplicaciones multiproceso](creating-a-driver-application-multithreaded-applications.md)  
  
## <a name="see-also"></a>Vea también  
 [SQL Server Native Client &#40;ODBC&#41;](sql-server-native-client-odbc.md)  
  
  
