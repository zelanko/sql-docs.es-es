---
title: Otros suscriptores que no son de SQL Server | Microsoft Docs
ms.custom: 
ms.date: 03/08/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: non-SQL Server Subscribers, other types
ms.assetid: 96b8beb9-38e8-4ce4-97ca-c0f8656b73b4
caps.latest.revision: "31"
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 035bddbc96126c98d48ac599db9307f565f1d38a
ms.sourcegitcommit: dcac30038f2223990cc21775c84cbd4e7bacdc73
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/18/2018
---
# <a name="other-non-sql-server-subscribers"></a>Otros suscriptores que no son de SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Para obtener una lista de suscriptores que no son de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] compatibles con [!INCLUDE[msCoName](../../../includes/msconame-md.md)], vea [Suscriptores que no son de SQL Server](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md). Este tema incluye información acerca de los requisitos para los controladores ODBC y los proveedores de OLE DB.  
  
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
  
## <a name="see-also"></a>Ver también  
 [Non-SQL Server Subscribers](../../../relational-databases/replication/non-sql/non-sql-server-subscribers.md)  
  
  
