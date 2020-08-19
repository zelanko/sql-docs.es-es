---
description: Crear una aplicación de controlador
title: Crear una aplicación
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 6bcb65baaf591267d1c40b254bb23fe19e383192
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88428197"
---
# <a name="creating-a-driver-application"></a>Crear una aplicación de controlador
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

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
  
 Una aplicación más compleja escrita para el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client también puede realizar las siguientes tareas:  
  
-   Usar cursores para controlar la ubicación en un conjunto de resultados.  
  
-   Solicitar operaciones de confirmación o reversión para el control de transacciones.  
  
-   Realizar transacciones distribuidas que impliquen dos o más servidores.  
  
-   Ejecutar procedimientos almacenados en el servidor remoto.  
  
-   Llamar a funciones de catálogo para realizar consultas sobre los atributos de un conjunto de resultados.  
  
-   Realizar operaciones de copia masiva.  
  
-   Administrar operaciones de datos de gran tamaño (**VARCHAR (Max)**, **nvarchar (Max)** y **varbinary (Max)** Columns  
  
-   Usar la lógica de reconexión para facilitar la conmutación por error al configurar la creación de reflejo de la base de datos.  
  
-   Registrar datos de rendimiento y consultas de ejecución prolongada.  
  
 Para realizar llamadas a funciones ODBC, una aplicación C o C++ debe incluir los archivos de encabezado sql.h, sqlext.h y sqltypes.h. Para realizar llamadas a las funciones API del instalador ODBC, una aplicación debe incluir el archivo de encabezado odbcinst.h. Una aplicación ODBC Unicode debe incluir el archivo de encabezado sqlucode.h. Las aplicaciones ODBC deben estar vinculadas al archivo odbc32.lib. Las aplicaciones ODBC que llaman a las funciones API del instalador ODBC deben estar vinculadas al archivo odbccp32.lib. Estos archivos se incluyen en Windows Platform SDK.  
  
 Muchos controladores ODBC, incluido el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client, ofrecen extensiones ODBC específicas del controlador. Para aprovechar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] las extensiones específicas del controlador ODBC de Native Client, una aplicación debe incluir el archivo de encabezado SQLNCLI. h. Este archivo de encabezado incluye:  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Atributos de conexión específicos del controlador ODBC de Native Client.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Atributos de instrucción específicos del controlador ODBC de Native Client.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Atributos de columna específicos del controlador ODBC de Native Client.  
  
-   Tipos de datos específicos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Tipos de datos definidos por el usuario específicos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Tipos de [SQLGetInfo](../../../relational-databases/native-client-odbc-api/sqlgetinfo.md) específicos del controlador ODBC de Native Client.  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Campos de diagnóstico del controlador ODBC de Native Client.  
  
-   Códigos de función dinámica de diagnóstico específicos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Definiciones de tipo de C/C++ para tipos de datos C nativos específicos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (que se devuelven cuando las columnas están enlazadas al tipo de datos C SQL_C_BINARY).  
  
-   Definición de tipo para la estructura de datos SQLPERF.  
  
-   Prototipos y macros de copia masiva para admitir el uso de la API de copia masiva a través de una conexión ODBC.  
  
-   Llame a las funciones API de metadatos de consulta distribuida para obtener listas de servidores vinculados y sus catálogos.  
  
 Cualquier aplicación ODBC de C o C++ que use la característica de copia masiva del [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client debe estar vinculada al archivo sqlncli11. lib. Las aplicaciones que llaman a las funciones API de metadatos de consulta distribuida también deben vincularse a sqlncli11.lib. Los archivos SQLNCLI. h y sqlncli11. lib se distribuyen como parte de las [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] herramientas del desarrollador. Los directorios Include y Lib de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deberían estar en las rutas de acceso LIB e INCLUDE del compilador, como en el siguiente ejemplo:  
  
```  
LIB=c:\Program Files\Microsoft Data Access SDK 2.8\Libs\x86\lib;C:\Program Files\Microsoft SQL Server\100\Tools\SDK\Lib;  
INCLUDE=c:\Program Files\Microsoft Data Access SDK 2.8\inc;C:\Program Files\Microsoft SQL Server\100\Tools\SDK\Include;  
```  
  
 Una decisión de diseño que se realiza al principio del proceso de generación de una aplicación es si la aplicación necesita tener varias llamadas ODBC pendientes al mismo tiempo. Hay dos métodos para admitir varias llamadas ODBC simultáneas, que se describen en los temas restantes en esta sección. Para obtener más información, vea la [Referencia del programador de ODBC](https://go.microsoft.com/fwlink/?LinkId=45250).  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Modo asincrónico y SQLCancel](../../../relational-databases/native-client/odbc/creating-a-driver-application-asynchronous-mode-and-sqlcancel.md)  
  
-   [Aplicaciones multiproceso](../../../relational-databases/native-client/odbc/creating-a-driver-application-multithreaded-applications.md)  
  
## <a name="see-also"></a>Consulte también  
 [SQL Server Native Client &#40;ODBC&#41;](../../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
