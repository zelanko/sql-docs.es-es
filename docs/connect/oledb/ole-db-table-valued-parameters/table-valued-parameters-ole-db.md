---
title: Parámetros con valores de tabla (OLE DB) | Documentos de Microsoft
description: Parámetros con valores de tabla (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-table-valued-parameters
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB, table-valued parameters
- table-valued parameters (OLE DB)
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f8f219346a4ed5ed6e03d6cca707bbf14091df1a
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2018
---
# <a name="table-valued-parameters-ole-db"></a>Parámetros con valores de tabla (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Esta sección describe la compatibilidad con parámetros con valores de tabla en el controlador OLE DB para SQL Server. Para obtener información general adicional, vea [parámetros con valores de tabla &#40;controlador OLE DB para SQL Server&#41;](../../oledb/features/table-valued-parameters-oledb-driver-for-sql-server.md). Para obtener un ejemplo, vea [usar parámetros &#40;OLE DB&#41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md).  
  
## <a name="remarks"></a>Comentarios  
 Actualmente, puede enviar datos en varias filas al servidor como parámetros a un procedimiento con conjuntos de parámetros (el parámetro DBPARAMS en **ICommand:: Execute**). Con los conjuntos de parámetros, cada elemento del conjunto se debe enviar al servidor en una solicitud de llamada a procedimiento remoto (RPC) independiente. Los parámetros con valores de tabla proporcionan una funcionalidad similar, pero existe una mejor integración con el servidor. Reduce el número de solicitudes RPC y habilita las operaciones basadas en conjuntos en el servidor.  
  
 Se admiten parámetros con valores de tabla en el controlador de OLE DB para SQL Server como OLE DB **conjunto de filas** objetos. Cualquier **conjunto de filas** objeto puede proporcionar el consumidor (es decir, la aplicación cliente mediante el controlador OLE DB para SQL Server) como marcador de posición para los parámetros del parámetro con valores de tabla. Los parámetros con valores de tabla se tratan como otros tipos de parámetros de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. El controlador OLE DB para SQL Server proporciona la creación, detección, especificación, enlace y las interfaces de esquema.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Creación de conjuntos de filas de parámetros con valores de tabla](../../oledb/ole-db-table-valued-parameters/table-valued-parameter-rowset-creation.md)  
  
-   [Detección de tipos de parámetros con valores de tabla](../../oledb/ole-db-table-valued-parameters/table-valued-parameter-type-discovery.md)  
  
-   [Ejecutar comandos que contienen parámetros con valores de tabla](../../oledb/ole-db-table-valued-parameters/executing-commands-containing-table-valued-parameters.md)  
  
-   [Insertar datos en parámetros con valores de tabla](../../oledb/ole-db-table-valued-parameters/inserting-data-into-table-valued-parameters.md)  
  
-   [Conjuntos de filas de esquema cambiados para los parámetros con valores de tabla de OLE DB](../../oledb/ole-db-table-valued-parameters/schema-rowsets-changed-for-ole-db-table-valued-parameters.md)  
  
-   [Compatibilidad con tipos de parámetros con valores de tablas de OLE DB](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support.md)  
  
-   [Compatibilidad con tipos de parámetro con valores de tabla OLE DB &#40;métodos&#41;](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-methods.md)  
  
-   [Compatibilidad con tipos de parámetro con valores de tabla OLE DB &#40;propiedades&#41;](../../oledb/ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-properties.md)  
  
## <a name="see-also"></a>Vea también  
 [Controlador OLE DB para SQL Server &#40;OLE DB&#41;](../../oledb/ole-db/oledb-driver-for-sql-server-ole-db.md)   
 [Usar con valores de tabla parámetros &#40; OLE DB &#41;](../../oledb/ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
