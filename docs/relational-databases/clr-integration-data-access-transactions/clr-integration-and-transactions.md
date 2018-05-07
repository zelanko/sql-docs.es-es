---
title: Integración de CLR y transacciones | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: clr
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- ADO.NET [CLR integration]
- common language runtime [SQL Server], ADO.NET
- managed code [SQL Server], transactions
- common language runtime [SQL Server], transactions
- System.Transactions namespace
- transactions [CLR integration]
ms.assetid: 381d206e-06e2-48d0-8206-295fcf06ac98
caps.latest.revision: 19
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9cab6c061f8baac232563b4afe41952da1b4892e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="clr-integration-and-transactions"></a>Integración CLR y transacciones
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  El espacio de nombres **System.Transactions** proporciona un nuevo marco de transacciones totalmente integrado con ADO.NET y la característica de integración con Common Language Runtime (CLR) en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . **System.Transactions** y ADO.NET trabajan en conjunto para extender y simplificar el uso de transacciones locales y distribuidas en las aplicaciones administradas.  
  
> [!NOTE]  
>  Un procedimiento definido por el usuario (UDP) CLR no puede establecer una conexión al mismo servidor donde se ejecuta (una conexión de bucle invertido) ni darse de alta en la misma transacción. Si se intenta efectuar la conexión, ésta se bloqueará y no se devolverá el control al UDP. Esto producirá un error de tiempo de espera (mensaje 1206) en el UDP.  
  
 Para obtener más información sobre las transacciones y .NET Framework, vea los temas sobre la realización de transacciones y el aprovechamiento de las transacciones en .NET Framework SDK.  
  
## <a name="in-this-section"></a>En esta sección  
 [Promoción de transacciones](../../relational-databases/clr-integration-data-access-transactions/transaction-promotion.md)  
 Describe la capacidad de promover transacciones y cómo utilizar esta característica.  
  
 [Obtener acceso a la transacción actual](../../relational-databases/clr-integration-data-access-transactions/accessing-the-current-transaction.md)  
 Describe cómo tener acceso a una transacción que se ejecuta actualmente en proceso en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Utilizar System.Transactions](../../relational-databases/clr-integration-data-access-transactions/using-system-transactions.md)  
 Describe cómo utilizar el **System.Transactions** interfaz de programación de aplicaciones (API) en una aplicación administrada.  
  
 [Período de duración de las transacciones](../../relational-databases/clr-integration-data-access-transactions/transaction-lifetimes.md)  
 Describe la diferencia en duración entre las transacciones iniciadas en procedimientos almacenados de [!INCLUDE[tsql](../../includes/tsql-md.md)] y las transacciones iniciadas en aplicaciones CLR.  
  
## <a name="see-also"></a>Vea también  
 [Acceso a datos de objetos de base de datos de CLR](../../relational-databases/clr-integration/data-access/data-access-from-clr-database-objects.md)  
  
  
