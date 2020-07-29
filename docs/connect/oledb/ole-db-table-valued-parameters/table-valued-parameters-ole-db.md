---
title: Parámetros con valores de tabla (OLE DB) | Microsoft Docs
description: Parámetros con valores de tabla (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB, table-valued parameters
- table-valued parameters (OLE DB)
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 8b93503bbf538cd5cb58488b5df7de9190dd3c78
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "85998920"
---
# <a name="table-valued-parameters-ole-db"></a>Parámetros con valores de tabla (OLE DB)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  En esta sección se describe la compatibilidad con los parámetros con valores de tabla de OLE DB Driver for SQL Server. Para información general adicional, consulte [Parámetros con valores de tabla &#40;OLE DB Driver for SQL Server&#41;](../../oledb/features/table-valued-parameters-oledb-driver-for-sql-server.md). Para ver un ejemplo, consulte [Uso de parámetros con valores de tabla &#40;OLE DB&#41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md).  
  
## <a name="remarks"></a>Observaciones  
 Actualmente, puede enviar datos de varias filas al servidor como parámetros de un procedimiento con conjuntos de parámetros (el parámetro DBPARAMS en **ICommand::Execute**). Con los conjuntos de parámetros, cada elemento del conjunto se debe enviar al servidor en una solicitud de llamada a procedimiento remoto (RPC) independiente. Los parámetros con valores de tabla proporcionan una funcionalidad similar, pero existe una mejor integración con el servidor. Esto reduce el número de solicitudes RPC y habilita las operaciones basadas en conjunto en el servidor.  
  
 Se admiten parámetros con valores de tabla en OLE DB Driver for SQL Server como objetos **Rowset** de OLE DB. El consumidor (es decir, la aplicación cliente que usa el controlador OLE DB para SQL Server) puede proporcionar cualquier objeto **Rowset** como un marcador de posición para los parámetros con valores de tabla. Los parámetros con valores de tabla se tratan como otros tipos de parámetros de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. OLE DB Driver for SQL Server proporciona interfaces de creación, detección, especificación, enlace y esquema.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Creación de conjuntos de filas de parámetros con valores de tabla](../../oledb/ole-db-table-valued-parameters/table-valued-parameter-rowset-creation.md)  
  
-   [Detección de tipos de parámetros con valores de tabla](../../oledb/ole-db-table-valued-parameters/table-valued-parameter-type-discovery.md)  
  
-   [Ejecutar comandos que contienen parámetros con valores de tabla](../../oledb/ole-db-table-valued-parameters/executing-commands-containing-table-valued-parameters.md)  
  
-   [Insertar datos en parámetros con valores de tabla](../../oledb/ole-db-table-valued-parameters/inserting-data-into-table-valued-parameters.md)  
  
-   [Conjuntos de filas de esquema cambiados para los parámetros con valores de tabla de OLE DB](../../oledb/ole-db-table-valued-parameters/schema-rowsets-changed-for-ole-db-table-valued-parameters.md)  
  
-   [Compatibilidad con tipos de parámetros con valores de tablas de OLE DB](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support.md)  
  
-   [Compatibilidad con tipos de parámetro con valores de tabla de OLE DB &#40;métodos&#41;](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-methods.md)  
  
-   [Compatibilidad con tipos de parámetros con valores de tabla de OLE DB &#40;propiedades&#41;](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-properties.md)  
  
## <a name="see-also"></a>Consulte también  
 [Programación del controlador OLE DB para SQL Server](../../oledb/ole-db/oledb-driver-for-sql-server-programming.md)   
 [Usar parámetros con valores de tabla &#40;OLE DB&#41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
