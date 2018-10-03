---
title: IDBProperties (OLE DB) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 2e5a4fd8-5164-495a-9986-3477aef8d8a5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3b6dada26e15fc83d890b270ad553eb051bb08fa
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48135875"
---
# <a name="idbproperties-ole-db"></a>IDBProperties (OLE DB)
  La especificación estándar OLE DB permite a los proveedores especificar VT_EMPTY para `DBPROPINFO::vValues`. Sin embargo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OLE DB de Native Client siempre devuelve VT_EMPTY cuando se llama a `IDBProperties::GetPropertyInfo` con `DBPROPSET_ROWSETALL` para recuperar las propiedades del conjunto de filas.  
  
## <a name="see-also"></a>Vea también  
 [Interfaces &#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)  
  
  
