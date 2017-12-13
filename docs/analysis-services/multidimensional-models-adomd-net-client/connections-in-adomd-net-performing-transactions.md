---
title: Realizar transacciones en ADOMD.NET | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- transactions [ADOMD.NET]
- ADOMD.NET, transactions
- AdomdTransaction object
ms.assetid: 7978c28b-c255-43c0-ad05-f38604d4d8fe
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: abe2e4bcc48a86e26e9a70e4f39e6bfbf7ba13ee
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="connections-in-adomdnet---performing-transactions"></a>Conexiones en ADOMD.NET: realizar transacciones
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]En ADOMD.NET, usa el <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction> objeto para administrar el contexto de transacción para un determinado <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> objeto. Esta funcionalidad le permite ejecutar varios comandos dentro del mismo contexto. Cada comando leerá los mismos datos sin los datos de la lectura que cambian entre cada ejecución de comandos.  
  
> [!NOTE]  
>  El <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction> clase es la implementación de la **System.Data.IDbTransaction** interfaz, la parte de la [!INCLUDE[msCoName](../../includes/msconame-md.md)] biblioteca de clases de .NET Framework e implementada por todos los proveedores de datos de .NET Framework que admiten transacciones.  
  
 El objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction> únicamente admite transacciones de lectura confirmada, que contiene los bloqueos compartidos mientras los datos se leen para evitar las lecturas no actualizadas.  
  
 <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection> se usa para iniciar la transacción. Para usar la transacción, los comandos se ejecutan en la conexión que inició la transacción. Cuando termine la transacción, puede revertir o confirmar la transacción.  
  
## <a name="starting-a-transaction"></a>Iniciar una transacción  
 Puede crear una instancia de un objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction> llamando al método <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.BeginTransaction%2A> del objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection>. En el ejemplo siguiente se muestra cómo se crea una instancia del objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction>.  
  
```  
Dim objTransaction As AdomdTransaction = objConnection.BeginTransaction()  
AdomdTransaction objTransaction = objConnection.BeginTransaction();  
```  
  
## <a name="rolling-back-a-transaction"></a>Revertir una transacción  
 Para revertir una transacción existente e incompleta, debe llamar al método <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction.Rollback%2A> del objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction>. Si se llama a este método en una transacción existente y completa, se produce una excepción.  
  
## <a name="committing-a-transaction"></a>Confirmar una transacción  
 Después de llamar al método <xref:Microsoft.AnalysisServices.AdomdClient.AdomdConnection.BeginTransaction%2A> para iniciar una transacción, puede completar la transacción llamando al método <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction.Commit%2A> del objeto <xref:Microsoft.AnalysisServices.AdomdClient.AdomdTransaction>. Si llama a este método en una transacción existente y completa, se produce una excepción.  
  
## <a name="see-also"></a>Vea también  
 [Para establecer conexiones en ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-client/connections-in-adomd-net.md)   
 [Programación del cliente de ADOMD.NET](../../analysis-services/multidimensional-models-adomd-net-client/adomd-net-client-programming.md)  
  
  
