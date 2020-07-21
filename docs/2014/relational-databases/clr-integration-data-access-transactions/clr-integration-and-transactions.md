---
title: Integración de CLR y transacciones | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- ADO.NET [CLR integration]
- common language runtime [SQL Server], ADO.NET
- managed code [SQL Server], transactions
- common language runtime [SQL Server], transactions
- System.Transactions namespace
- transactions [CLR integration]
ms.assetid: 381d206e-06e2-48d0-8206-295fcf06ac98
author: rothja
ms.author: jroth
ms.openlocfilehash: de72a2113aeb568decbdc9b5ee0174160cc0d3ef
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84955074"
---
# <a name="clr-integration-and-transactions"></a>Integración CLR y transacciones
  El espacio de nombres `System.Transactions` proporciona un nuevo marco de transacciones totalmente integrado con ADO.NET y la característica de integración con Common Language Runtime (CLR) en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. `System.Transactions` y ADO.NET trabajan en conjunto para extender y simplificar el uso de transacciones locales y distribuidas en aplicaciones administradas.  
  
> [!NOTE]  
>  Un procedimiento definido por el usuario (UDP) CLR no puede establecer una conexión al mismo servidor donde se ejecuta (una conexión de bucle invertido) ni darse de alta en la misma transacción. Si se intenta efectuar la conexión, ésta se bloqueará y no se devolverá el control al UDP. Esto producirá un error de tiempo de espera (mensaje 1206) en el UDP.  
  
 Para obtener más información sobre las transacciones y .NET Framework, vea los temas sobre la realización de transacciones y el aprovechamiento de las transacciones en .NET Framework SDK.  
  
## <a name="in-this-section"></a>En esta sección  
 [Promoción de transacciones](transaction-promotion.md)  
 Describe la capacidad de promover transacciones y cómo utilizar esta característica.  
  
 [Obtener acceso a la transacción actual](accessing-the-current-transaction.md)  
 Describe cómo tener acceso a una transacción que se ejecuta actualmente en proceso en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Utilizar System.Transactions](../native-client-ole-db-transactions/transactions.md)  
 Describe cómo utilizar la interfaz de programación de aplicaciones (API) `System.Transactions` en la aplicación administrada.  
  
 [Período de duración de las transacciones](transaction-lifetimes.md)  
 Describe la diferencia en duración entre las transacciones iniciadas en procedimientos almacenados de [!INCLUDE[tsql](../../includes/tsql-md.md)] y las transacciones iniciadas en aplicaciones CLR.  
  
## <a name="see-also"></a>Consulte también  
 [Acceso a datos de objetos de base de datos de CLR](../clr-integration/data-access/data-access-from-clr-database-objects.md)  
  
  
