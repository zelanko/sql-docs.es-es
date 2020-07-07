---
title: Asignando un identificador de conexión | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC applications, passwords
- ODBC applications, connections
- handles [SQL Server Native Client]
- expiration [SQL Server Native Client]
- passwords [SQL Server], modifying
- SQL Server Native Client ODBC driver, connection handles
- connection handles [SQL Server Native Client]
- modifying passwords
- SQLAllocHandle function
ms.assetid: 471d8a31-199c-4f92-bb10-004fc7733b35
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7aee78c5b9f9b151710e3dc5feb662347b588f08
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86007143"
---
# <a name="allocating-a-connection-handle"></a>Asignar un identificador de conexión
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Antes de que la aplicación se pueda conectar a un origen de datos o controlador, debe asignar un identificador de conexión. Esto se hace llamando a **SQLAllocHandle** con el parámetro *HandleType* establecido en SQL_HANDLE_DBC y *InputHandle* que apunta a un identificador de entorno inicializado.  
  
 Las características de la conexión se controlan estableciendo los atributos de conexión. Por ejemplo, dado que las transacciones se producen en el nivel de conexión, el nivel de aislamiento de transacción es un atributo de conexión. De igual forma, el tiempo de espera del inicio de sesión, o número de segundos que se espera mientras se intenta conectar antes de agotar el tiempo, es un atributo de conexión.  
  
 Los atributos de conexión se establecen con [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)y su configuración actual se recupera con [SQLGetConnectAttr](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md). Si se llama a **SQLSetConnectAttr** antes de que se intente una conexión, el administrador de controladores ODBC almacena los atributos en su estructura de conexión y los establece en el controlador como parte del proceso de conexión. Algunos atributos de conexión se deben establecer antes de la aplicación intente conectar; otros se pueden establecer después de que la conexión se haya completado. Por ejemplo, SQL_ATTR_ODBC_CURSORS se debe establecer antes de que se realice una conexión, pero SQL_ATTR_AUTOCOMMIT se puede establecer después de conectar.  
  
 En ocasiones, las aplicaciones que se ejecutan en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] versión 7.0 o versiones posteriores pueden mejorar su rendimiento si restablecen el tamaño de paquete de red del flujo TDS. El tamaño de paquete predeterminado se establece en el servidor, en 4 KB. Un tamaño de paquete entre 4 y 8 KB generalmente proporciona el máximo rendimiento. Si las pruebas muestran que el rendimiento es mejor con un tamaño de paquete diferente, la aplicación puede restablecer el tamaño de paquete. Las aplicaciones ODBC pueden hacerlo antes de la conexión mediante una llamada a **SQLSetConnectAttr** con la opción SQL_ATTR_PACKET_SIZE. Algunas aplicaciones presentan un mejor rendimiento con un tamaño de paquete mayor, pero las mejoras de rendimiento suelen ser mínimas en tamaños de paquete mayores que 8 KB.  
  
 El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] controlador ODBC de Native Client tiene una serie de atributos de conexión extendidos que una aplicación puede utilizar para aumentar su funcionalidad. Algunos de estos atributos controlan las mismas opciones que se pueden especificar en orígenes de datos y se utilizan para invalidar las opciones establecidas en un origen de datos. Por ejemplo, si una aplicación utiliza identificadores entrecomillados, puede establecer el atributo SQL_COPT_SS_QUOTED_IDENT específico de controlador en SQL_QI_ON para asegurarse de que esta opción siempre se establece sin tener en cuenta el valor en cualquier origen de datos.  
  
## <a name="see-also"></a>Consulte también  
 [Comunicarse con SQL Server &#40;ODBC&#41;](../../relational-databases/native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
  
