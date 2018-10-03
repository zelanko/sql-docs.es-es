---
title: Realizar transacciones en ADOMD.NET | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- transactions [ADOMD.NET]
- ADOMD.NET, transactions
- AdomdTransaction object
ms.assetid: 7978c28b-c255-43c0-ad05-f38604d4d8fe
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: aa3fd6ad27ced739c6d8ebd5d2fb2ad00bd6f707
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48169755"
---
# <a name="performing-transactions-in-adomdnet"></a>Realizar transacciones en ADOMD.NET
  En ADOMD.NET, usa el objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction> para administrar el contexto de transacción para un objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> determinado. Esta funcionalidad le permite ejecutar varios comandos dentro del mismo contexto. Cada comando leerá los mismos datos sin los datos de la lectura que cambian entre cada ejecución de comandos.  
  
> [!NOTE]  
>  La clase <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction> es la implementación de la interfaz `System.Data.IDbTransaction`, parte de la biblioteca de clases de [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework e implementada por todos los proveedores de datos de .NET Framework que admiten transacciones.  
  
 El objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction> únicamente admite transacciones de lectura confirmada, que contiene los bloqueos compartidos mientras los datos se leen para evitar las lecturas no actualizadas.  
  
 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> se usa para iniciar la transacción. Para usar la transacción, los comandos se ejecutan en la conexión que inició la transacción. Cuando termine la transacción, puede revertir o confirmar la transacción.  
  
## <a name="starting-a-transaction"></a>Iniciar una transacción  
 Puede crear una instancia de un objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction> llamando al método <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.BeginTransaction%2A> del objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>. En el ejemplo siguiente se muestra cómo se crea una instancia del objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction>.  
  
```  
Dim objTransaction As AdomdTransaction = objConnection.BeginTransaction()  
AdomdTransaction objTransaction = objConnection.BeginTransaction();  
```  
  
## <a name="rolling-back-a-transaction"></a>Revertir una transacción  
 Para revertir una transacción existente e incompleta, debe llamar al método <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction.Rollback%2A> del objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction>. Si llama a este método en una transacción existente y completa, se produce una excepción.  
  
## <a name="committing-a-transaction"></a>Confirmar una transacción  
 Después de llamar al método <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.BeginTransaction%2A> para iniciar una transacción, puede completar la transacción llamando al método <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction.Commit%2A> del objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction>. Si llama a este método en una transacción existente y completa, se produce una excepción.  
  
## <a name="see-also"></a>Vea también  
 [Establecer conexiones en ADOMD.NET](connections-in-adomd-net.md)   
 [Programación del cliente de ADOMD.NET](adomd-net-client-programming.md)  
  
  
