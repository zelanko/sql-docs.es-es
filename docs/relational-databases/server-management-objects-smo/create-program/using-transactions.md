---
title: Uso de transacciones | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: smo
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, transactions
- transactions [SMO]
- SMO [SQL Server], transactions
ms.assetid: 399aded8-bee3-4cfb-a671-1877c7d0de9f
caps.latest.revision: 37
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017
ms.openlocfilehash: 95558180d66acb53af1f7c507fa3fea314644296
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39552494"
---
# <a name="using-transactions"></a>Usar transacciones
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  En los objetos de administración de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (SMO), el procesamiento de transacciones se logra a través de la conexión a la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante el objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection>. El <xref:Microsoft.SqlServer.Management.Common.ServerConnection> objeto hace referencia el <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propiedad de la <xref:Microsoft.SqlServer.Management.Smo.Server> objeto cuando se establece la conexión. Métodos como <xref:Microsoft.SqlServer.Management.Common.DataTransferProgressEventType.StartTransaction>, <xref:Microsoft.SqlServer.Management.Common.ServerConnection.RollBackTransaction%2A> y <xref:Microsoft.SqlServer.Management.Common.ServerConnection.CommitTransaction%2A> pertenecen a la propiedad de objeto <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A>.  
  
## <a name="see-also"></a>Vea también  
 [Crear programas SMO](../../../relational-databases/server-management-objects-smo/create-program/creating-smo-programs.md)  
  
  
