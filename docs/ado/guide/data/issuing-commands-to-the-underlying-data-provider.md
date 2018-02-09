---
title: Emitir comandos al proveedor de datos subyacente | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- shape commands [ADO]
- underlying providers [ADO]
- data shaping [ADO], commands
ms.assetid: d6001863-7733-4c32-817f-081e48587fa1
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f27f4fb143db0c210097f0ae1ab7804ae827853e
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="issuing-commands-to-the-underlying-data-provider"></a>Emitir comandos al proveedor de datos subyacente
Cualquier comando que no comienzan con forma se pasa al proveedor de datos. Esto es equivalente a la emisión de un comando de forma de la forma "SHAPE {comando de proveedor}". Estos comandos tienen *no* tiene que producir una **conjunto de registros**. Por ejemplo, "forma {DROP TABLE MyTable} es un comando shape perfectamente válido, suponiendo que el proveedor de datos admite DROP TABLE.  
  
 Esta capacidad permite que los comandos de proveedor normal y los comandos shape compartan la misma conexión y transacción.  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de la forma de datos](../../../ado/guide/data/data-shaping-example.md)   
 [Gramática formal de forma](../../../ado/guide/data/formal-shape-grammar.md)   
 [Comandos Shape en General](../../../ado/guide/data/shape-commands-in-general.md)
