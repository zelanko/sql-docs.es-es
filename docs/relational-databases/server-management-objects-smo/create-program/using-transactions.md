---
description: Usar transacciones
title: Usar transacciones | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, transactions
- transactions [SMO]
- SMO [SQL Server], transactions
ms.assetid: 399aded8-bee3-4cfb-a671-1877c7d0de9f
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4e12a321436f13b6db9ae7c5a63f29a6d69766b0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88420299"
---
# <a name="using-transactions"></a>Usar transacciones
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  En los objetos de administración de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (SMO), el procesamiento de transacciones se logra a través de la conexión a la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante el objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection>. La <xref:Microsoft.SqlServer.Management.Common.ServerConnection> propiedad del objeto hace referencia al objeto <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> <xref:Microsoft.SqlServer.Management.Smo.Server> cuando se establece la conexión. Métodos como <xref:Microsoft.SqlServer.Management.Common.DataTransferProgressEventType.StartTransaction>, <xref:Microsoft.SqlServer.Management.Common.ServerConnection.RollBackTransaction%2A> y <xref:Microsoft.SqlServer.Management.Common.ServerConnection.CommitTransaction%2A> pertenecen a la propiedad de objeto <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A>.  
  
## <a name="see-also"></a>Consulte también  
 [Crear programas SMO](../../../relational-databases/server-management-objects-smo/create-program/creating-smo-programs.md)  
  
  
