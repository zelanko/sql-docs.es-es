---
title: Uso de transacciones | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, transactions
- transactions [SMO]
- SMO [SQL Server], transactions
ms.assetid: 399aded8-bee3-4cfb-a671-1877c7d0de9f
caps.latest.revision: 36
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 2c132ac199fb6af9e0349c463d5b30954acbf8bd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199632"
---
# <a name="using-transactions"></a>Usar transacciones
  En los objetos de administración de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (SMO), el procesamiento de transacciones se logra a través de la conexión a la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante el objeto <xref:Microsoft.SqlServer.Management.Common.ServerConnection>. El <xref:Microsoft.SqlServer.Management.Common.ServerConnection> objeto hace referencia el <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> propiedad de la <xref:Microsoft.SqlServer.Management.Smo.Server> objeto cuando se establece la conexión. Métodos como <xref:Microsoft.SqlServer.Management.Common.DataTransferProgressEventType.StartTransaction>, <xref:Microsoft.SqlServer.Management.Common.ServerConnection.RollBackTransaction%2A> y <xref:Microsoft.SqlServer.Management.Common.ServerConnection.CommitTransaction%2A> pertenecen a la propiedad de objeto <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A>.  
  
## <a name="see-also"></a>Vea también  
 [Crear programas SMO](creating-smo-programs.md)  
  
  