---
title: Creación de un conjunto de filas con IOpenRowset (controlador OLE DB) | Microsoft Docs
description: Creación de un conjunto de filas con la interfaz IOpenRowset de OLE DB Driver for SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- IOpenRowset interface
- rowsets [OLE DB], creating
- OLE DB Driver for SQL Server, rowsets
- OLE DB rowsets, creating
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 721a54d4e423675fa5dad39d22e8f94c178228d6
ms.sourcegitcommit: 591bbf4c7e4e2092f8abda6a2ffed263cb61c585
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/22/2020
ms.locfileid: "86942395"
---
# <a name="creating-a-rowset-with-iopenrowset"></a>Crear un conjunto de filas con IOpenRowset
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server admite el método **IOpenRowset::OpenRowset** con las restricciones siguientes:  
  
-   Debe especificarse una tabla base o una vista en una estructura de identificador de base de datos (DBID) a la que apunte el parámetro *pTableID*.  
  
-   El miembro *eKind* de DBID debe indicar DBKIND_NAME.  
  
-   El miembro *uName* de DBID debe especificar el nombre de una tabla base existente o una vista como una cadena de caracteres Unicode.  
  
-   El parámetro *pIndexID* de **OpenRowset** debe ser NULL.  
  
 El conjunto de resultados de **IOpenRowset::OpenRowset** contiene un único conjunto de filas. Los conjuntos de resultados que contienen un único conjunto de filas pueden admitirse mediante cursores de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. La compatibilidad de cursor permite que el programador utilice mecanismos de simultaneidad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte también  
 [Conjuntos de filas](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
