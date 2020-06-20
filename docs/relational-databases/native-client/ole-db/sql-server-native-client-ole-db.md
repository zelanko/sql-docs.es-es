---
title: OLE DB
description: El proveedor de OLE DB de SQL Server Native Client es una API COM para el acceso a datos, que se usa para herramientas, utilidades o componentes de bajo nivel que necesitan un alto rendimiento.
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, about SQL Server Native Client OLE DB provider
- OLE DB, SQL Server Native Client OLE DB provider
- data access [SQL Server Native Client], OLE DB
- SQLNCLI, OLE DB
- OLE DB
- SQL Server Native Client OLE DB provider
- SQL Server Native Client, OLE DB
ms.assetid: da846da4-ec19-4a4f-81fb-7d5a2b2bf80a
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a5f945ca5abaa515823ea81ad30ca4292cc42690
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84948762"
---
# <a name="sql-server-native-client-ole-db"></a>SQL Server Native Client (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client (SQLNCLI) es una API com de bajo nivel que se utiliza para tener acceso a los datos. El proveedor OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client se recomienda para desarrollar herramientas, utilidades o componentes de bajo nivel que necesitan alto rendimiento. El proveedor OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client es un proveedor nativo, de alto rendimiento con acceso directo al protocolo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Flujo TDS.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client proporciona compatibilidad con OLE DB a las aplicaciones que se conectan a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client es un proveedor compatible con la versión 2,0 de OLE DB.  
 
> [!IMPORTANT]
> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Native Client OLE DB (SQLNCLI) sigue en desuso y no se recomienda usarlo para los nuevos trabajos de desarrollo. En su lugar, use el nuevo [Microsoft OLE DB Driver for SQL Server](../../../connect/oledb/oledb-driver-for-sql-server.md) (MSOLEDBSQL), que se actualizará con las características de servidor más recientes.
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Crear una aplicación de proveedor OLE DB de SQL Server Native Client](../../../relational-databases/native-client-ole-db-provider/creating-a-sql-server-native-client-ole-db-provider-application.md)  
  
-   [Objetos de origen de datos &#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
-   [Comandos](../../../relational-databases/native-client-ole-db-commands/commands.md)  
  
-   [Conjuntos de filas](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
-   [Procedimientos almacenados](../../../relational-databases/native-client/ole-db/stored-procedures.md)  
  
-   [BLOB y objetos OLE](../../../relational-databases/native-client-ole-db-blobs/blobs-and-ole-objects.md)  
  
-   [Tablas e índices](../../../relational-databases/native-client-ole-db-tables-indexes/tables-and-indexes.md)  
  
-   [Tipos de datos &#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-data-types/data-types-ole-db.md)  
  
-   [Compatibilidad con conjuntos de filas de esquema &#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/schema-rowset-support-ole-db.md)  
  
-   [Parámetros con valores de tabla &#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameters-ole-db.md)  
  
-   [Mejoras de fecha y hora &#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
-   [Tipos definidos por el usuario de CLR de gran tamaño &#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/large-clr-user-defined-types-ole-db.md)  
  
-   [Compatibilidad con FILESTREAM &#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/filestream-support-ole-db.md)  
  
-   [Transactions](../../../relational-databases/native-client-ole-db-transactions/transactions.md)  
  
-   [Errores](../../../relational-databases/native-client-ole-db-errors/errors.md)  
  
-   [Nombres de entidad de seguridad de servicio &#40;SPNs&#41; en conexiones cliente &#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/service-principal-names-spns-in-client-connections-ole-db.md)  
  
-   [Compatibilidad con columnas dispersas &#40;OLE DB&#41;](../../../relational-databases/native-client/ole-db/sparse-columns-support-ole-db.md)  
  
-   [Referencia de SQL Server Native Client &#40;OLE DB&#41;](../../../relational-databases/native-client-ole-db-interfaces/sql-server-native-client-ole-db-interfaces.md)  
  
-   [Temas de procedimientos de OLE DB](../../../relational-databases/native-client-ole-db-how-to/ole-db-how-to-topics.md)  
  
## <a name="see-also"></a>Consulte también  
 [Programación de SQL Server Native Client](../../../relational-databases/native-client/sql-server-native-client-programming.md)  
  
  
