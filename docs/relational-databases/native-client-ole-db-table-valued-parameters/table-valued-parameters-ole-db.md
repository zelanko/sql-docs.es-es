---
title: Parámetros con valores de tabla (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- OLE DB, table-valued parameters
- table-valued parameters (OLE DB)
ms.assetid: 4298b73d-615b-4d28-9843-03b4d5fc489e
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 15055f582d7add6194753e2743d63b5e082318b5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300239"
---
# <a name="table-valued-parameters-ole-db"></a>Parámetros con valores de tabla (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  En esta sección se describe la compatibilidad con parámetros con valores de tabla en el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client. Para obtener información general adicional, vea Parámetros con valores de [tabla &#40;SQL ServerSQL Server Native Client&#41;](../../relational-databases/native-client/features/table-valued-parameters-sql-server-native-client.md). Para ver un ejemplo, consulte [Uso de parámetros con valores de tabla &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md).  
  
## <a name="remarks"></a>Observaciones  
 Actualmente, puede enviar datos de varias filas al servidor como parámetros de un procedimiento con conjuntos de parámetros (el parámetro DBPARAMS en **ICommand::Execute**). Con los conjuntos de parámetros, cada elemento del conjunto se debe enviar al servidor en una solicitud de llamada a procedimiento remoto (RPC) independiente. Los parámetros con valores de tabla proporcionan una funcionalidad similar, pero existe una mejor integración con el servidor. Esto reduce el número de solicitudes RPC y habilita las operaciones basadas en conjunto en el servidor.  
  
 Los parámetros de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] valor de tabla se admiten en el proveedor OLE DB de Native Client como objetos de **conjunto** de filas OLE DB. Cualquier objeto **Rowset** podría ser proporcionado por el consumidor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (es decir, la aplicación cliente que usa el proveedor OLE DB de Native Client) como marcador de posición para los parámetros de parámetro con valores de tabla. Los parámetros con valores de tabla se tratan como otros tipos de parámetros de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El proveedor OLE DB de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client proporciona interfaces de creación, detección, especificación, enlace y esquema.  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Creación de conjuntos de filas de parámetros con valores de tabla](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameter-rowset-creation.md)  
  
-   [Detección de tipos de parámetros con valores de tabla](../../relational-databases/native-client-ole-db-table-valued-parameters/table-valued-parameter-type-discovery.md)  
  
-   [Ejecutar comandos que contienen parámetros con valores de tabla](../../relational-databases/native-client-ole-db-table-valued-parameters/executing-commands-containing-table-valued-parameters.md)  
  
-   [Insertar datos en parámetros con valores de tabla](../../relational-databases/native-client-ole-db-table-valued-parameters/inserting-data-into-table-valued-parameters.md)  
  
-   [Conjuntos de filas de esquema cambiados para los parámetros con valores de tabla de OLE DB](../../relational-databases/native-client-ole-db-table-valued-parameters/schema-rowsets-changed-for-ole-db-table-valued-parameters.md)  
  
-   [Compatibilidad con tipos de parámetros con valores de tablas de OLE DB](../../relational-databases/native-client-ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support.md)  
  
-   [Compatibilidad con tipos de parámetro con valores de tabla de OLE DB &#40;métodos&#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-methods.md)  
  
-   [Compatibilidad con tipos de parámetros con valores de tabla de OLE DB &#40;propiedades&#41;](../../relational-databases/native-client-ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support-properties.md)  
  
## <a name="see-also"></a>Consulte también  
 [SQL ServerSQL Server Native Client &#40;&#41;OLE DB](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)   
 [Usar parámetros con valores de tabla &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
