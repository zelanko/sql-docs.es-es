---
title: Otros suscriptores que no son de SQL Server | Microsoft Docs
ms.custom: 
ms.date: 03/08/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- non-SQL Server Subscribers, other types
ms.assetid: 96b8beb9-38e8-4ce4-97ca-c0f8656b73b4
caps.latest.revision: 31
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: d7002d1aeae61b16976b9a8230c58fb12f882042
ms.lasthandoff: 04/11/2017

---
# <a name="other-non-sql-server-subscribers"></a>Otros suscriptores que no son de SQL Server
  Para obtener una lista de suscriptores que no son de[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] compatibles con [!INCLUDE[msCoName](../../../includes/msconame-md.md)], vea [Non-SQL Server Subscribers](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md). Este tema incluye información acerca de los requisitos para los controladores ODBC y los proveedores de OLE DB.  
  
## <a name="odbc-driver-requirements"></a>Requisitos para los controladores ODBC  
 El controlador ODBC:  
  
-   Tiene que cumplir el nivel 1 de ODBC.  
  
-   Debe ser un entorno de distribuidor seguro para subprocesos.  
  
-   Tiene que ser compatible con las transacciones.  
  
-   Tiene que aceptar el Lenguaje de definición de datos (DDL, Data Definition Language).  
  
-   No puede ser de solo lectura.  
  
-   Debe admitir nombres de tabla largos, como **MSreplication_subscriptions**.  
  
## <a name="replicating-using-ole-db-interfaces"></a>Replicación con interfaces OLE DB  
 Los proveedores OLE DB deben ser compatibles con estos objetos para la replicación transaccional:  
  
-   Objeto**DataSource**   
  
-   Objeto**Session**   
  
-   Objeto**Command**   
  
-   Objeto**Rowset**   
  
-   Objeto**Error**   
  
### <a name="datasource-object-interfaces"></a>Interfaces del objeto DataSource  
 Para conectar con un origen de datos se requieren las siguientes interfaces:  
  
-   **IDBInitialize**  
  
-   **IDBCreateSession**  
  
-   **IDBProperties**  
  
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
  
 Se necesita**IAccessor** para crear descriptores de acceso a parámetros. Si el proveedor es compatible con **IColumnRowset**, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] utiliza esa interfaz para determinar si una columna es una columna de identidad.  
  
### <a name="rowset-object-interfaces"></a>Interfaces del objeto Rowset  
 Se requieren las siguientes interfaces:  
  
-   **IRowset**  
  
-   **IAccessor**  
  
-   **IColumnsInfo**  
  
 La aplicación tiene que abrir un conjunto de filas en una tabla replicada creada en la base de datos de suscripciones. Se necesita**IColumnsInfo** e **IAccessor** para tener acceso a los datos del conjunto de filas.  
  
### <a name="error-object-interfaces"></a>Interfaces del objeto Error  
 Para controlar los errores, utilice las siguientes interfaces:  
  
-   **IErrorRecords**  
  
-   **IErrorInfo**  
  
 Utilice **ISQLErrorInfo** si el proveedor OLE DB es compatible.  
  
 Para obtener más información acerca del proveedor OLE DB, vea la documentación que se suministra con el proveedor OLE DB.  
  
## <a name="see-also"></a>Vea también  
 [Non-SQL Server Subscribers](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)  
  
  

