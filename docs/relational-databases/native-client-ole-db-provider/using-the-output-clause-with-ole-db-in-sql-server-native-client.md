---
title: Usar la cláusula OUTPUT con OLE DB en SQL Server Native Client | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 53deeb99-c088-4fde-844b-b2d91d6de1eb
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: f631875ee4b6283fe07f229e77a950ff10c2dfa5
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37406940"
---
# <a name="using-the-output-clause-with-ole-db-in-sql-server-native-client"></a>Usar la cláusula OUTPUT con OLE DB en SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Si utiliza una cláusula OUTPUT en un comando INSERT, UPDATE, DELETE o MERGE, no estará disponible el recuento de filas afectadas. La aplicación debe contar el número de filas del conjunto de filas que devuelve la cláusula OUTPUT.  
  
## <a name="see-also"></a>Vea también  
 [Crear una aplicación de proveedor OLE DB de SQL Server Native Client](../../relational-databases/native-client-ole-db-provider/creating-a-sql-server-native-client-ole-db-provider-application.md)  
  
  
