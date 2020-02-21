---
title: 'Propiedades de sesión: controlador OLE DB para SQL Server | Microsoft Docs'
description: 'Propiedades de sesión: controlador OLE DB para SQL Server'
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- sessions [OLE DB]
- OLE DB Driver for SQL Server, sessions
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 7bc2ae9c6908bfcd0bf28b4f05be757d22c55f75
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "68015914"
---
# <a name="session-properties---ole-db-driver-for-sql-server"></a>Propiedades de sesión: controlador OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server interpreta las propiedades de la sesión de OLE DB de la siguiente manera.  
  
|Id. de propiedad|Descripción|  
|-----------------|-----------------|  
|DBPROP_SESS_AUTOCOMMITISOLEVELS|El controlador OLE DB para SQL Server admite todos los niveles de aislamiento de transacción con confirmación automática a excepción del nivel DBPROPVAL_TI_CHAOS.|  
  
 En el conjunto de propiedades específico del proveedor DBPROPSET_SQLSERVERSESSION, el controlador OLE DB para SQL Server define la propiedad de sesión adicional siguiente.  
  
|Id. de propiedad|Descripción|  
|-----------------|-----------------|  
|SSPROP_QUOTEDCATALOGNAMES|Escriba:  VT_BOOL<br /><br /> R (lectura) y W (escritura): Lectura/escritura<br /><br /> Valor predeterminado: VARIANT_FALSE<br /><br /> Descripción: identificadores entre comillas permitidos en restricción CATALOG.<br /><br /> VARIANT_TRUE: identificadores entre comillas reconocidos para una restricción CATALOG en conjuntos de filas de esquema que proporcionan compatibilidad con consultas distribuidas.<br /><br /> VARIANT_FALSE: identificadores entre comillas no reconocidos para una restricción CATALOG en conjuntos de filas de esquema que proporcionan compatibilidad con consultas distribuidas.<br /><br /> Para obtener más información sobre los conjuntos de filas de esquema que proporcionan compatibilidad con consultas distribuidas, vea [Compatibilidad con consultas distribuidas en conjuntos de filas de esquema](../../oledb/ole-db/schema-rowsets-distributed-query-support.md).|  
|SSPROP_ALLOWNATIVEVARIANT|Escriba:  VT_BOOL<br /><br /> R (lectura) y W (escritura): Lectura/Escritura<br /><br /> Valor predeterminado: VARIANT_FALSE<br /><br /> Descripción: determina si los datos se capturan como DBTYPE_VARIANT o DBTYPE_SQLVARIANT.<br /><br /> VARIANT_TRUE: el tipo de columna se devuelve como DBTYPE_SQLVARIANT, en cuyo caso el búfer contendrá la estructura SSVARIANT.<br /><br /> VARIANT_FALSE: el tipo de columna se devuelve como DBTYPE_VARIANT y el búfer contendrá la estructura VARIANT.|  
|SSPROP_ASYNCH_BULKCOPY|Para usar el modo asincrónico, establezca la propiedad de sesión SSPROP_ASYNCH_BULKCOPY específica del proveedor en VARIANT_TRUE antes de llamar al método BCPExec. Esta propiedad se encuentra disponible en el conjunto de propiedades DBPROPSET_SQLSERVERSESSION.|  
  
## <a name="see-also"></a>Consulte también  
 [Objetos de origen de datos (OLE DB)](../../oledb/ole-db-data-source-objects/data-source-objects-ole-db.md)  
  
  
