---
title: Bloqueo y desbloqueo de bases de datos (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- locking [XML for Analysis]
- XML for Analysis, locking
- XMLA, locking
- unlocking objects
ms.assetid: 451afa58-ce03-4ecc-8dd3-9e7e8559b5f1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e1f518f846a6e0bb87f858d7a5798eb9a7e9c8d0
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/26/2018
ms.locfileid: "50146280"
---
# <a name="locking-and-unlocking-databases-xmla"></a>Bloquear y desbloquear bases de datos (XMLA)
  Puede bloquear y desbloquear bases de datos utilizando, respectivamente, la [bloqueo](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla) y [Unlock](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla) comandos de XML for Analysis (XMLA). Normalmente, otros comandos XMLA bloquean y desbloquean objetos automáticamente según sea necesario para completar el comando durante la ejecución. Puede bloquear o desbloquear una base de datos para llevar a cabo varios comandos en una única transacción, como explícitamente un [Batch](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/batch-element-xmla) comando, evitando que otras aplicaciones confirmen una transacción de escritura a la base de datos.  
  
## <a name="locking-databases"></a>Bloquear bases de datos  
 El comando `Lock` bloquea un objeto, para uso compartido o exclusivo, dentro del contexto de la transacción actualmente activa. Un bloqueo en un objeto impide que se confirmen las transacciones hasta que se quita el bloqueo. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] admite dos tipos de bloqueos, bloqueos compartidos y bloqueos exclusivos. Para obtener más información acerca de los tipos de bloqueo admitidos por [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], consulte [elemento Mode &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/mode-element-xmla).  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] solamente permite bloquear las bases de datos. El comando [Object](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla) debe contener una referencia de objeto a una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Si no se especifica el elemento `Object` o el elemento `Object` hace referencia a un objeto que no es una base de datos, se produce un error.  
  
> [!IMPORTANT]  
>  Solo los administradores de bases de datos o de servidores pueden ejecutar explícitamente un comando `Lock`.  
  
 Otros comandos ejecutan implícitamente un comando `Lock` en una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Cualquier operación que lee datos o metadatos de una base de datos, como cualquier método [Discover](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-discover) o un método [Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) que ejecuta un comando [Statement](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/statement-element-xmla) , emite implícitamente un bloqueo compartido en la base de datos. Cualquier transacción que confirma los cambios de datos o metadatos en un objeto en un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] bases de datos, como un `Execute` método que se ejecuta un [Alter](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla) comando, emite implícitamente un bloqueo exclusivo en la base de datos.  
  
## <a name="unlocking-objects"></a>Desbloquear objetos  
 El comando `Unlock` quita un bloqueo establecido dentro del contexto de la transacción que está activa en ese momento.  
  
> [!IMPORTANT]  
>  Solo los administradores de base de datos o servidor pueden ejecutar explícitamente un `Unlock` comando.  
  
 Todos los bloqueos se mantienen en el contexto de la transacción actual. Cuando la transacción actual se confirma o se revierte, se liberan automáticamente todos los bloqueos definidos dentro de la transacción.  
  
## <a name="see-also"></a>Vea también  
 [Bloquear elemento &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla)   
 [Elemento Unlock &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla)   
 [Desarrollo con XMLA en Analysis Services](developing-with-xmla-in-analysis-services.md)  
  
  
