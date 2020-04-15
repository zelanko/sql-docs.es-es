---
title: IRowsetFastLoad (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: COM
helpviewer_keywords:
- IRowsetFastLoad interface
ms.assetid: d19a7097-48d9-409a-aff9-277891b7aca7
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: feea17329a8e809083263a83217aeb87fbf91bc3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307255"
---
# <a name="irowsetfastload-ole-db"></a>IRowsetFastLoad (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  La interfaz **IRowsetFastLoad** expone la compatibilidad con las operaciones de copia masiva basadas en memoria de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Los consumidores del proveedor OLE DB de Native [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Client usan la interfaz para agregar rápidamente datos a una tabla existente.  
  
 Si establece SSPROP_ENABLEFASTLOAD en VARIANT_TRUE para una sesión, no puede leer datos de conjuntos de filas devueltos posteriormente de dicha sesión. Cuando SSPROP_ENABLEFASTLOAD se establece en VARIANT_TRUE, todos los conjuntos de filas creados en la sesión serán de tipo IRowsetFastLoad. Los conjuntos de filas de tipo IRowsetFastLoad no admiten la funcionalidad de captura del conjunto de filas; por tanto, no se pueden leer los datos de estos conjuntos de filas.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Método|Descripción|  
|------------|-----------------|  
|[IRowsetFastLoad::Commit &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-commit-ole-db.md)|Marca el final de un lote de filas insertadas y escribe las filas en la tabla [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[IRowsetFastLoad::InsertRow &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-interfaces/irowsetfastload-insertrow-ole-db.md)|Agrega una fila al conjunto de filas de copia masiva.|  
  
## <a name="see-also"></a>Consulte también  
 [Interfaces &#40;&#41;OLE DB](https://msdn.microsoft.com/library/34c33364-8538-45db-ae41-5654481cda93)   
 [Copiar datos de forma masiva mediante IRowsetFastLoad &#40;&#41;OLE DB](../../relational-databases/native-client-ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md)   
 [Enviar datos BLOB a SQL SERVER mediante IROWSETFASTLOAD e ISEQUENTIALSTREAM &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md)  
  
  
