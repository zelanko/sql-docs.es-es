---
title: Creación de un conjunto de filas con IOpenRowset | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- IOpenRowset interface
- rowsets [OLE DB], creating
- SQL Server Native Client OLE DB provider, rowsets
- OLE DB rowsets, creating
ms.assetid: e8bc3de7-4b97-4de9-8df8-e11947d24045
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9a22369ae477bf1cf59fa2266c2178ae3a0147fb
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301722"
---
# <a name="creating-a-rowset-with-iopenrowset"></a>Crear un conjunto de filas con IOpenRowset
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proveedor de OLE DB de Native Client admite el método **IOpenRowset:: OPENROWSET** con las siguientes restricciones:  
  
-   Debe especificarse una tabla base o una vista en una estructura de identificador de base de datos (DBID) a la que apunte el parámetro *pTableID*.  
  
-   El miembro *eKind* de DBID debe indicar DBKIND_NAME.  
  
-   El miembro *uName* de DBID debe especificar el nombre de una tabla base existente o una vista como una cadena de caracteres Unicode.  
  
-   El parámetro *pIndexID* de **OpenRowset** debe ser NULL.  
  
 El conjunto de resultados de **IOpenRowset::OpenRowset** contiene un único conjunto de filas. Los conjuntos de resultados que contienen un único conjunto de filas [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueden ser compatibles con los cursores. La compatibilidad de cursor permite que el programador utilice mecanismos de simultaneidad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte también  
 [Conjuntos de filas](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
  
