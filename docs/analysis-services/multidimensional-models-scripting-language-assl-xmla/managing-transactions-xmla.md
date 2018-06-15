---
title: Administrar transacciones (XMLA) | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1f2884d49f03d8557d72d8d6d48cdba432a8c37f
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34022302"
---
# <a name="managing-transactions-xmla"></a>Administrar transacciones (XMLA)
  Cada comando XML for Analysis (XMLA) enviado a una instancia de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] se ejecuta en el contexto de una transacción en la sesión implícita o explícita actual. Para administrar cada una de estas transacciones, utilice la [BeginTransaction](../../analysis-services/xmla/xml-elements-commands/begintransaction-element-xmla.md), [CommitTransaction](../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md), y [RollbackTransaction](../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md) comandos. Mediante estos comandos puede crear transacciones implícitas o explícitas, cambiar el recuento de referencias de transacción, así como iniciar, confirmar o revertir transacciones.  
  
## <a name="implicit-and-explicit-transactions"></a>Transacciones implícitas y explícitas  
 Una transacción es implícita o explícita:  
  
 **Transacción implícita**  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] crea un *implícita* comando de transacción para un XMLA si el **BeginTransaction** comando no especifica el inicio de una transacción. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] siempre confirma una transacción implícita si el comando se ejecuta correctamente y revierte una transacción implícita si el comando produce un error.  
  
 **Transacción explícita**  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] crea un *explícita* transacción si el **BeginTransaction** comando inicia una transacción. Sin embargo, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] solo confirma una transacción explícita si un **CommitTransaction** comando se envía y se revierte una transacción explícita si un **RollbackTransaction** se envía el comando.  
  
 Además, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] revierte tanto transacciones implícitas como explícitas si la sesión actual finaliza antes de que se complete la transacción activa.  
  
## <a name="transactions-and-reference-counts"></a>Transacciones y recuentos de referencias  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] mantiene un recuento de referencias de transacción para cada sesión. Sin embargo, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no admite las transacciones anidadas en las que solo se mantiene una transacción activa por sesión. Si la sesión actual no tiene una transacción activa, el recuento de referencias de transacción se establece en cero.  
  
 En otras palabras, cada uno de ellos **BeginTransaction** comando incrementa el recuento de referencias en uno, mientras que cada **CommitTransaction** disminuye de comando que el recuento de referencias en uno. Si un **CommitTransaction** comando establece el recuento de transacciones a cero, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] confirma la transacción.  
  
 Sin embargo, el **RollbackTransaction** comando revierte la transacción activa independientemente del valor actual del recuento de referencias de transacción. En otras palabras, una sola **RollbackTransaction** comando revierte la transacción activa, independientemente de cuántos **BeginTransaction** comandos o **CommitTransaction** los comandos enviados y establece el recuento de referencias de transacción en cero.  
  
## <a name="beginning-a-transaction"></a>Inicia una transacción  
 El **BeginTransaction** comando inicia una transacción explícita en la sesión actual y se incrementa el recuento de referencias de transacción para la sesión actual en uno. Todos los comandos subsiguientes se consideran dentro de la transacción activa hasta que hay suficiente **CommitTransaction** comandos se envían a confirmar la transacción activa o un único **RollbackTransaction**se envía el comando para revertir la transacción activa.  
  
## <a name="committing-a-transaction"></a>Confirmar una transacción  
 El **CommitTransaction** comando confirma los resultados de los comandos que se ejecutan tras el **BeginTransaction** comando se ejecutó en la sesión actual. Cada **CommitTransaction** comando disminuye el recuento de referencias de las transacciones activas en una sesión. Si un **CommitTransaction** comando establece el recuento de referencias en cero, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] confirma la transacción activa. Si no hay ninguna transacción activa (es decir, el recuento de referencias de transacción para la sesión actual se ha establecido en cero), un **CommitTransaction** comando produce un error.  
  
## <a name="rolling-back-a-transaction"></a>Revertir una transacción  
 El **RollbackTransaction** comando revierte los resultados de los comandos que se ejecutan tras el **BeginTransaction** comando se ejecutó en la sesión actual. El **RollbackTransaction** comando revierte la transacción activa, independientemente del recuento de referencias de transacción actual y establece el recuento de referencias de transacción en cero. Si no hay ninguna transacción activa (es decir, el recuento de referencias de transacción para la sesión actual se ha establecido en cero), un **RollbackTransaction** comando produce un error.  
  
## <a name="see-also"></a>Vea también  
 [Desarrollar con XMLA en Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
