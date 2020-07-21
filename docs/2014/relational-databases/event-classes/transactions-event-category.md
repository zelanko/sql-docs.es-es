---
title: Transacciones (categoría de eventos) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
topic_type:
- apiref
helpviewer_keywords:
- SQL Server event classes, Transactions event category
- event classes [SQL Server], Transactions event category
- Transactions event category [SQL Server]
ms.assetid: bfc75c5b-7115-49d8-9148-a0c84ee66a9a
author: stevestein
ms.author: sstein
ms.openlocfilehash: 3b68a91fb166797c220cb0c4f5cf2607ca267538
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85051316"
---
# <a name="transactions-event-category"></a>Transacciones (categoría de eventos)
  Las clases de eventos **Transactions** se pueden utilizar para supervisar el estado de las transacciones. Los nombres de las clases de eventos prefijados con **TM:** se usan para realizar un seguimiento de las operaciones relacionadas con las transacciones enviadas desde la interfaz de administración de transacciones.  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[DTCTransaction (clase de eventos)](dtctransaction-event-class.md)|Realiza un seguimiento de las transacciones coordinadas por el Coordinador de transacciones distribuidas de [!INCLUDE[msCoName](../../includes/msconame-md.md)] (MS DTC). Se trata de transacciones distribuidas entre dos o más bases de datos o instancias del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].|  
|[SQLTransaction (clase de eventos)](sqltransaction-event-class.md)|Realiza un seguimiento de las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] BEGIN TRAN, COMMIT TRAN, SAVE TRAN y ROLLBACK TRAN.|  
|[TM: Begin Tran Completed (clase de eventos)](tm-begin-tran-completed-event-class.md)|Indica que se ha completado la solicitud BEGIN TRANSACTION.|  
|[TM: Begin Tran Starting (clase de eventos)](tm-begin-tran-starting-event-class.md)|Indica que se está iniciando la solicitud BEGIN TRANSACTION.|  
|[TM: Commit Tran Completed (clase de eventos)](tm-commit-tran-completed-event-class.md)|Indica que se ha completado la solicitud COMMIT TRANSACTION.|  
|[TM: Commit Tran Starting (clase de eventos)](tm-commit-tran-starting-event-class.md)|Indica que se está iniciando la solicitud COMMIT TRANSACTION.|  
|[TM: Promote Tran Completed (clase de eventos)](tm-promote-tran-completed-event-class.md)|Indica que se ha completado la solicitud PROMOTE TRANSACTION.|  
|[TM: Promote Tran Starting (clase de eventos)](tm-promote-tran-starting-event-class.md)|Indica que se está iniciando la solicitud PROMOTE TRANSACTION.|  
|[TM: Rollback Tran Completed (clase de eventos)](tm-rollback-tran-completed-event-class.md)|Indica que se ha completado la solicitud ROLLBACK TRANSACTION.|  
|[TM: Rollback Tran Starting (clase de eventos)](tm-rollback-tran-starting-event-class.md)|Indica que se está iniciando la solicitud ROLLBACK TRANSACTION.|  
|[TM: Save Tran Completed (clase de eventos)](tm-save-tran-completed-event-class.md)|Indica que se ha completado la solicitud SAVE TRANSACTION.|  
|[TM: Save Tran Starting (clase de eventos)](tm-save-tran-starting-event-class.md)|Indica que se está iniciando la solicitud SAVE TRANSACTION.|  
|[TransactionLog (clase de eventos)](transactionlog-event-class.md)|Realiza un seguimiento cuando se escriben transacciones en el registro de transacciones de base de datos.|  
  
  
