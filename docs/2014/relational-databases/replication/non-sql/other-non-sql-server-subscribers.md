---
title: Otros suscriptores que no son de SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- non-SQL Server Subscribers, other types
ms.assetid: 96b8beb9-38e8-4ce4-97ca-c0f8656b73b4
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 135d317d74a720d51c966ed92f1c305f8c04b838
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63021944"
---
# <a name="other-non-sql-server-subscribers"></a>Otros suscriptores que no son de SQL Server
  Para obtener una lista de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] suscriptores que no son [!INCLUDE[msCoName](../../../includes/msconame-md.md)]de compatibles con, vea [suscriptores que no son de SQL Server](non-sql-server-subscribers.md). Este tema incluye información acerca de los requisitos para los controladores ODBC y los proveedores de OLE DB.  
  
## <a name="odbc-driver-requirements"></a>Requisitos para los controladores ODBC  
 El controlador ODBC:  
  
-   Tiene que cumplir el nivel 1 de ODBC.  
  
-   Tiene que ser de subproceso seguro, y para la arquitectura de procesador (Intel o Alpha) y la plataforma (32 ó 64 bits) en la que se ejecuta el distribuidor de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Tiene que ser compatible con las transacciones.  
  
-   Tiene que aceptar el Lenguaje de definición de datos (DDL, Data Definition Language).  
  
-   No puede ser de solo lectura.  
  
-   Debe admitir nombres de tabla largos, como **MSreplication_subscriptions**.  
  
## <a name="replicating-using-ole-db-interfaces"></a>Replicación con interfaces OLE DB  
 Los proveedores OLE DB deben ser compatibles con estos objetos para la replicación transaccional:  
  
-   Objeto **DataSource**  
  
-   Objeto de **sesión**  
  
-   Objeto **Command**  
  
-   Objeto **Rowset**  
  
-   **Error** (objeto)  
  
### <a name="datasource-object-interfaces"></a>Interfaces del objeto DataSource  
 Para conectar con un origen de datos se requieren las siguientes interfaces:  
  
-   `IDBInitialize`  
  
-   `IDBCreateSession`  
  
-   `IDBProperties`  
  
 Si el proveedor es compatible con la interfaz **IDBInfo** , [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] utiliza la interfaz para obtener información como el carácter de identificador entre comillas, la longitud máxima de instrucciones SQL y el número máximo de caracteres en nombres de tablas y de columnas.  
  
### <a name="session-object-interfaces"></a>Interfaces del objeto Session  
 Se requieren las siguientes interfaces:  
  
-   **IDBCreateCommand**  
  
-   **ITransaction**  
  
-   **ITransactionLocal**  
  
-   **IDBSchemaRowset**  
  
### <a name="command-object-interfaces"></a>Interfaces del objeto Command  
 Se requieren las siguientes interfaces:  
  
-   **ICommand**  
  
-   **ICommandProperties**  
  
-   **ICommandText**  
  
-   **ICommandPrepare**  
  
-   **IColumnsInfo**  
  
-   **IAccessor**  
  
-   **ICommandWithParameters**  
  
 **IAccessor** es necesaria para crear descriptores de acceso de parámetros. Si el proveedor es **** compatible con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] IColumnRowset, utiliza esa interfaz para determinar si una columna es una columna de identidad.  
  
### <a name="rowset-object-interfaces"></a>Interfaces del objeto Rowset  
 Se requieren las siguientes interfaces:  
  
-   **IRowset**  
  
-   **IAccessor**  
  
-   **IColumnsInfo**  
  
 La aplicación tiene que abrir un conjunto de filas en una tabla replicada creada en la base de datos de suscripciones. Se necesita **IColumnsInfo** e **IAccessor** para tener acceso a los datos del conjunto de filas.  
  
### <a name="error-object-interfaces"></a>Interfaces del objeto Error  
 Para controlar los errores, utilice las siguientes interfaces:  
  
-   **IErrorRecords**  
  
-   **IErrorInfo**  
  
 Utilice **ISQLErrorInfo** si el proveedor OLE DB es compatible.  
  
 Para obtener más información acerca del proveedor OLE DB, vea la documentación que se suministra con el proveedor OLE DB.  
  
## <a name="see-also"></a>Consulte también  
 [suscriptores que no son de SQL Server](non-sql-server-subscribers.md)  
  
  
