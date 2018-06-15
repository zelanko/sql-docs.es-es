---
title: Promoción de transacciones | Documentos de Microsoft
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
- distributed transactions [CLR integration]
- promoting transactions [CLR integration]
- Enlist keyword
- transaction promotion [CLR integration]
ms.assetid: 5bc7e26e-28ad-4198-a40d-8b2c648ba304
caps.latest.revision: 13
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 742ff5f5785fea2c3652fc88e78d5cefc2090281
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32918270"
---
# <a name="transaction-promotion"></a>Promoción de transacciones
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La *promoción* de transacciones describe transacciones ligeras, locales que se pueden promover automáticamente a transacciones totalmente distribuibles, según sea necesario. Cuando se invoca un procedimiento almacenado administrado en una transacción de base de datos del servidor, se ejecuta el código de Common Language Runtime (CLR) en el contexto de una transacción local.  Si se abre una conexión a un servidor remoto en una transacción de base de datos, la conexión al servidor remoto se da de alta en la transacción distribuida y la transacción local se promueve automáticamente a una transacción distribuida. Por lo tanto, la promoción de transacciones minimiza la sobrecarga de las transacciones distribuidas difiriendo la creación de transacciones distribuidas hasta que se necesiten. La promoción de transacciones es automática, si se ha habilitado utilizando la palabra clave **Enlist** y no requiere la intervención del programador. El proveedor de datos de .NET Framework para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona compatibilidad para la promoción de transacciones, controlada a través de las clases de .NET Framework **System.Data.SqlClient** espacio de nombres.  
  
## <a name="the-enlist-keyword"></a>La palabra clave Enlist  
 La propiedad **ConnectionString** de un objeto **SqlConnection** admite la palabra clave **Enlist** , que indica si **System.Data.SqlClient** detecta los contextos transaccionales y da de alta automáticamente la conexión en una transacción distribuida. Si esta palabra clave está establecida en true (el valor predeterminado), la conexión se da de alta automáticamente en el contexto de transacción actual del subproceso de apertura. Si esta palabra clave está establecida en false, la conexión SqlClient no interactúa con una transacción distribuida. Si no se especifica **Enlist** en la cadena de conexión, la conexión se da de alta automáticamente en una transacción distribuida si se detecta una en el momento en que se abre la conexión.  
  
## <a name="distributed-transactions"></a>Transacciones distribuidas  
 Las transacciones distribuidas consumen normalmente recursos del sistema significativos. [!INCLUDE[msCoName](../../includes/msconame-md.md)] DTC (Coordinador de transacciones distribuidas) administra tales transacciones e integra todos los administradores de recursos a los que se obtiene acceso en estas transacciones. Promoción de transacciones, por otro lado, es una forma especial de un **System.Transactions** transacciones que delega con efectividad el trabajo como una simple [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] transacciones. **System.Transactions**, **System.Data.SqlClient**, y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] coordinar el trabajo que supone administrar la transacción y promoverla a una transacción completamente distribuida cuando es necesario.  
  
 La ventaja de utilizar la promoción de transacciones es que cuando se abre una conexión con una transacción **TransactionScope** activa y no hay abierta ninguna otra conexión, se confirma la transacción como una transacción ligera, en lugar de incurrir en la sobrecarga adicional de una transacción completa distribuida. Para obtener más información acerca de **TransactionScope**, consulte [System.Transactions utilizando](../../relational-databases/clr-integration-data-access-transactions/using-system-transactions.md).  
  
## <a name="see-also"></a>Vea también  
 [Las transacciones y la integración CLR](../../relational-databases/clr-integration-data-access-transactions/clr-integration-and-transactions.md)  
  
  
