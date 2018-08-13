---
title: Crear un conjunto de filas con IOpenRowset | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- IOpenRowset interface
- rowsets [OLE DB], creating
- SQL Server Native Client OLE DB provider, rowsets
- OLE DB rowsets, creating
ms.assetid: e8bc3de7-4b97-4de9-8df8-e11947d24045
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: e55449d882ebbda8149d25eae447916505ba4ac0
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39562779"
---
# <a name="creating-a-rowset-with-iopenrowset"></a>Crear un conjunto de filas con IOpenRowset
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client admite el **IOpenRowset:: OpenRowset** método con las siguientes restricciones:  
  
-   Debe especificarse una tabla base o una vista en una estructura de identificador de base de datos (DBID) a la que apunte el parámetro *pTableID*.  
  
-   El miembro *eKind* de DBID debe indicar DBKIND_NAME.  
  
-   El miembro *uName* de DBID debe especificar el nombre de una tabla base existente o una vista como una cadena de caracteres Unicode.  
  
-   El parámetro *pIndexID* de **OpenRowset** debe ser NULL.  
  
 El conjunto de resultados de **IOpenRowset::OpenRowset** contiene un único conjunto de filas. Los conjuntos de resultados que contienen un único conjunto de filas pueden admitirse mediante cursores de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La compatibilidad de cursor permite que el programador utilice mecanismos de simultaneidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
  
