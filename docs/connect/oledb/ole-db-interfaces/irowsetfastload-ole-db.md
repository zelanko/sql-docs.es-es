---
title: IRowsetFastLoad (OLE DB) | Documentos de Microsoft
description: IRowsetFastLoad (OLE DB)
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-interfaces
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
apitype: COM
helpviewer_keywords:
- IRowsetFastLoad interface
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 18279d27c1beb7bf81e61adb901b41cedf3aa47b
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="irowsetfastload-ole-db"></a>IRowsetFastLoad (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  El **IRowsetFastLoad** interfaz expone la compatibilidad para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] operaciones de copia masiva basadas en memoria. Controlador de OLE DB para los consumidores de SQL Server usan la interfaz para rápidamente agregar datos a otra [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] tabla.  
  
 Si establece SSPROP_ENABLEFASTLOAD en VARIANT_TRUE para una sesión, no puede leer datos de conjuntos de filas devueltos posteriormente de dicha sesión. Cuando SSPROP_ENABLEFASTLOAD se establece en VARIANT_TRUE, todos los conjuntos de filas creados en la sesión será de tipo IRowsetFastLoad. Conjuntos de filas iRowsetFastLoad no admiten la funcionalidad de captura del conjunto de filas; por lo tanto, no se puede leer datos de estos conjuntos de filas.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Método|Description|  
|------------|-----------------|  
|[IRowsetFastLoad::Commit &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/irowsetfastload-commit-ole-db.md)|Marca el final de un lote de filas insertadas y escribe las filas en la tabla [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|[IRowsetFastLoad::InsertRow &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/irowsetfastload-insertrow-ole-db.md)|Agrega una fila al conjunto de filas de copia masiva.|  
  
## <a name="see-also"></a>Vea también  
 [Interfaces & #40; OLE DB & #41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md)   
 [Copia masiva de datos mediante IRowsetFastLoad &#40;OLE DB&#41;](../../oledb/ole-db-how-to/bulk-copy-data-using-irowsetfastload-ole-db.md)   
 [Enviar datos BLOB a SQL SERVER mediante IROWSETFASTLOAD y ISEQUENTIALSTREAM & #40; OLE DB & #41;](../../oledb/ole-db-how-to/send-blob-data-to-sql-server-using-irowsetfastload-and-isequentialstream-ole-db.md)  
  
  
