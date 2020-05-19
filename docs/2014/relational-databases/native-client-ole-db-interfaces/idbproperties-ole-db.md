---
title: IDBProperties (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 2e5a4fd8-5164-495a-9986-3477aef8d8a5
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 7598f1c865395f2a43eba8f67c86a68bd46d586b
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82707364"
---
# <a name="idbproperties-ole-db"></a>IDBProperties (OLE DB)
  La especificación estándar OLE DB permite a los proveedores especificar VT_EMPTY para `DBPROPINFO::vValues`. Sin embargo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB siempre devuelve VT_EMPTY cuando se llama a `IDBProperties::GetPropertyInfo` con `DBPROPSET_ROWSETALL` para recuperar las propiedades del conjunto de filas.  
  
## <a name="see-also"></a>Consulte también  
 [Interfaces &#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)  
  
  
