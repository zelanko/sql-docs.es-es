---
title: Administrar transacciones (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- XML for Analysis, transactions
- XMLA, transactions
- explicit transactions [XMLA]
- implicit transactions
- transactions [XML for Analysis]
- rolling back transactions, XMLA
- reference counts [XML for Analysis]
- committing transactions
- starting transactions
ms.assetid: f5112e01-82f8-4870-bfb7-caa00182c999
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ad8a77d1d8552dc811c1232afb53c142452658db
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62727249"
---
# <a name="managing-transactions-xmla"></a>Administrar transacciones (XMLA)
  Cada comando de XML for Analysis (XMLA) enviado a una instancia [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de se ejecuta en el contexto de una transacción en la sesión implícita o explícita actual. Para administrar cada una de estas transacciones, se usan los comandos [BeginTransaction](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/begintransaction-element-xmla), [CommitTransaction](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/committransaction-element-xmla)y [RollbackTransaction](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/rollbacktransaction-element-xmla) . Mediante estos comandos puede crear transacciones implícitas o explícitas, cambiar el recuento de referencias de transacción, así como iniciar, confirmar o revertir transacciones.  
  
## <a name="implicit-and-explicit-transactions"></a>Transacciones implícitas y explícitas  
 Una transacción es implícita o explícita:  
  
 **Transacción implícita**  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]crea una transacción *implícita* para un comando XMLA si el `BeginTransaction` comando no especifica el inicio de una transacción. 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] siempre confirma una transacción implícita si el comando se ejecuta correctamente y revierte una transacción implícita si el comando produce un error.  
  
 **Transacción explícita**  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]crea una transacción *explícita* si el `BeginTransaction` comando inicia una transacción. Sin embargo, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] solo confirma una transacción explícita si se envía un comando `CommitTransaction` y revierte una transacción explícita si se envía un comando `RollbackTransaction`.  
  
 Además, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] revierte tanto transacciones implícitas como explícitas si la sesión actual finaliza antes de que se complete la transacción activa.  
  
## <a name="transactions-and-reference-counts"></a>Transacciones y recuentos de referencias  
 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] mantiene un recuento de referencias de transacción para cada sesión. Sin embargo, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no admite las transacciones anidadas en las que solo se mantiene una transacción activa por sesión. Si la sesión actual no tiene una transacción activa, el recuento de referencias de transacción se establece en cero.  
  
 En otras palabras, cada comando `BeginTransaction` incrementa en uno el recuento de referencias, mientras que cada comando `CommitTransaction` disminuye el recuento de referencias en uno. Si un comando `CommitTransaction` establece el recuento de transacciones en cero, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] confirma la transacción.  
  
 Sin embargo, el comando `RollbackTransaction` revierte la transacción activa independientemente del valor actual del recuento de referencias de transacción. En otras palabras, un único comando `RollbackTransaction` revierte la transacción activa, independientemente del número de comandos `BeginTransaction` o `CommitTransaction` enviados, y establece el recuento de referencias de transacción en cero.  
  
## <a name="beginning-a-transaction"></a>Inicio de una transacción  
 El comando `BeginTransaction` inicia una transacción explícita en la sesión actual e incrementa en uno el recuento de referencias de transacción para la sesión actual. Todos los comandos subsiguientes se consideran parte de la transacción activa hasta que se envíen suficientes comandos `CommitTransaction` para confirmar dicha transacción o bien se envíe un comando `RollbackTransaction` único para revertir la transacción activa.  
  
## <a name="committing-a-transaction"></a>Confirmar una transacción  
 El comando `CommitTransaction` confirma los resultados de los comandos que se ejecutan tras el comando `BeginTransaction` en la sesión actual. Cada comando `CommitTransaction` disminuye el recuento de referencias de las transacciones activas en una sesión. Si un comando `CommitTransaction` establece el recuento de referencias en cero, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] confirma la transacción activa. Si no hay ninguna transacción activa (en otras palabras, el recuento de referencias de transacción de la sesión actual ya está establecido en cero), un comando `CommitTransaction` produce un error.  
  
## <a name="rolling-back-a-transaction"></a>Revertir una transacción  
 El comando `RollbackTransaction` revierte los resultados de los comandos que se ejecutan tras el comando `BeginTransaction` en la sesión actual. El comando `RollbackTransaction` revierte la transacción activa, independientemente del recuento de referencias de la transacción actual, y establece el recuento de referencias de la transacción en cero. Si no hay ninguna transacción activa (en otras palabras, el recuento de referencias de transacción de la sesión actual ya está establecido en cero), un comando `RollbackTransaction` produce un error.  
  
## <a name="see-also"></a>Consulte también  
 [Desarrollar con XMLA en Analysis Services](developing-with-xmla-in-analysis-services.md)  
  
  
