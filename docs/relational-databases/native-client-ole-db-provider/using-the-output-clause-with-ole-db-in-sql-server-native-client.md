---
title: Usar la cláusula OUTPUT con OLE DB en SQL Server Native Client | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 53deeb99-c088-4fde-844b-b2d91d6de1eb
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: a7f93f6dc2f8080775588168bfd6ca10733712b0
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/07/2019
ms.locfileid: "73789066"
---
# <a name="using-the-output-clause-with-ole-db-in-sql-server-native-client"></a>Usar la cláusula OUTPUT con OLE DB en SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Si utiliza una cláusula OUTPUT en un comando INSERT, UPDATE, DELETE o MERGE, no estará disponible el recuento de filas afectadas. La aplicación debe contar el número de filas del conjunto de filas que devuelve la cláusula OUTPUT.  
  
## <a name="see-also"></a>Vea también  
 [Crear una aplicación de proveedor OLE DB de SQL Server Native Client](../../relational-databases/native-client-ole-db-provider/creating-a-sql-server-native-client-ole-db-provider-application.md)  
  
  
