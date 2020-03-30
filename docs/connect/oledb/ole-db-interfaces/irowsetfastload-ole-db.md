---
title: IRowsetFastLoad (OLE DB) | Microsoft Docs
description: IRowsetFastLoad (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
apitype: COM
helpviewer_keywords:
- IRowsetFastLoad interface
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 2d21e270eb7e2d387201d66df0bb566c3924d53c
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "67994398"
---
# <a name="irowsetfastload-ole-db"></a>IRowsetFastLoad (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  La interfaz **IRowsetFastLoad** expone la compatibilidad con las operaciones de copia masiva basadas en memoria de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Los consumidores de OLE DB Driver for SQL Server usan la interfaz para agregar datos rápidamente a una tabla [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] existente.  
  
 Si establece SSPROP_ENABLEFASTLOAD en VARIANT_TRUE para una sesión, no puede leer datos de conjuntos de filas devueltos posteriormente de dicha sesión. Cuando SSPROP_ENABLEFASTLOAD se establece en VARIANT_TRUE, todos los conjuntos de filas creados en la sesión serán de tipo IRowsetFastLoad. Los conjuntos de filas de tipo IRowsetFastLoad no admiten la funcionalidad de captura del conjunto de filas; por tanto, no se pueden leer los datos de estos conjuntos de filas.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Método|Descripción|  
|------------|-----------------|  
|[IRowsetFastLoad::Commit &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/irowsetfastload-commit-ole-db.md)|Marca el final de un lote de filas insertadas y escribe las filas en la tabla [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
|[IRowsetFastLoad::InsertRow &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/irowsetfastload-insertrow-ole-db.md)|Agrega una fila al conjunto de filas de copia masiva.|  
  
## <a name="see-also"></a>Consulte también  
 [Interfaces &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)   
 [Copiar datos de forma masiva mediante IRowsetFastLoad &#40;OLE DB&#41;](../../oledb/ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md)   
 [Enviar datos BLOB a SQL SERVER mediante IROWSETFASTLOAD e ISEQUENTIALSTREAM &#40;OLE DB&#41;](../../oledb/ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md)  
  
  
