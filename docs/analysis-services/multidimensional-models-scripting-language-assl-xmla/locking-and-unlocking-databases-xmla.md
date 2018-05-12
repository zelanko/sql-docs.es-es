---
title: Bloquear y desbloquear bases de datos (XMLA) | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d9868b251ff95fae1822abb5844ff7e909940dae
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="locking-and-unlocking-databases-xmla"></a>Bloquear y desbloquear bases de datos (XMLA)
  Puede bloquear y desbloquear bases de datos utilizando, respectivamente, el [bloqueo](../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md) y [Unlock](../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md) comandos de XML for Analysis (XMLA). Normalmente, otros comandos XMLA bloquean y desbloquean objetos automáticamente según sea necesario para completar el comando durante la ejecución. Se puede bloquear o desbloquear una base de datos para llevar a cabo varios comandos en una única transacción, como explícitamente un [lote](../../analysis-services/xmla/xml-elements-commands/batch-element-xmla.md) comando, evitando que otras aplicaciones confirmen una transacción de escritura a la base de datos.  
  
## <a name="locking-databases"></a>Bloquear bases de datos  
 El comando **Lock** bloquea un objeto, para uso compartido o exclusivo, dentro del contexto de la transacción actualmente activa. Un bloqueo en un objeto impide que se confirmen las transacciones hasta que se quita el bloqueo. [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] admite dos tipos de bloqueos, bloqueos compartidos y bloqueos exclusivos. Para obtener más información acerca de los tipos de bloqueo compatibles con [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], consulte [elemento Mode & #40; XMLA & #41; ](../../analysis-services/xmla/xml-elements-properties/mode-element-xmla.md).  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] solamente permite bloquear las bases de datos. El [objeto](../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md) elemento debe contener una referencia de objeto a una [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] base de datos. Si no se especifica el elemento **Object** o el elemento **Object** hace referencia a un objeto que no es una base de datos, se produce un error.  
  
> [!IMPORTANT]  
>  Solo los administradores de bases de datos o de servidores pueden ejecutar explícitamente un comando **Lock** .  
  
 Otros comandos ejecutan implícitamente un **bloqueo** comando un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] base de datos. Cualquier operación que lee datos o metadatos de una base de datos, como cualquier [Discover](../../analysis-services/xmla/xml-elements-methods-discover.md) método o una [Execute](../../analysis-services/xmla/xml-elements-methods-execute.md) método que se ejecuta un [instrucción](../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md) comando, emite implícitamente un compartido bloqueo en la base de datos. Cualquier transacción que confirma los cambios de datos o metadatos en un objeto en un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] base de datos, como un **Execute** método que se ejecuta un [Alter](../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md) comando, emite implícitamente un bloqueo exclusivo en el base de datos.  
  
## <a name="unlocking-objects"></a>Desbloquear objetos  
 El comando **Unlock** quita un bloqueo establecido dentro del contexto de la transacción que está activa en ese momento.  
  
> [!IMPORTANT]  
>  Solo los administradores de bases de datos o de servidores pueden ejecutar explícitamente un comando **Unlock** .  
  
 Todos los bloqueos se mantienen en el contexto de la transacción actual. Cuando la transacción actual se confirma o se revierte, se liberan automáticamente todos los bloqueos definidos dentro de la transacción.  
  
## <a name="see-also"></a>Vea también  
 [Bloquear elemento &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md)   
 [Desbloquear elemento & #40; XMLA & #41;](../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md)   
 [Desarrollar con XMLA en Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
