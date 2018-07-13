---
title: IDBProperties (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 2e5a4fd8-5164-495a-9986-3477aef8d8a5
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 71999899b70c8eab76e26dba22f09884618277d2
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37413613"
---
# <a name="idbproperties-ole-db"></a>IDBProperties (OLE DB)
  La especificación estándar OLE DB permite a los proveedores especificar VT_EMPTY para `DBPROPINFO::vValues`. Sin embargo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OLE DB de Native Client siempre devuelve VT_EMPTY cuando se llama a `IDBProperties::GetPropertyInfo` con `DBPROPSET_ROWSETALL` para recuperar las propiedades del conjunto de filas.  
  
## <a name="see-also"></a>Vea también  
 [Interfaces &#40;OLE DB&#41;](../../database-engine/dev-guide/interfaces-ole-db.md)  
  
  
