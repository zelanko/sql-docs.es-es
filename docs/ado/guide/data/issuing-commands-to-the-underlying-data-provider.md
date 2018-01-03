---
title: Emitir comandos al proveedor de datos subyacente | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
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
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 24498f4d57627a1a7fb265a22703c0e9f8e581af
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="issuing-commands-to-the-underlying-data-provider"></a>Emitir comandos al proveedor de datos subyacente
Cualquier comando que no comienzan con forma se pasa al proveedor de datos. Esto es equivalente a la emisión de un comando de forma de la forma "SHAPE {comando de proveedor}". Estos comandos tienen *no* tiene que producir una **conjunto de registros**. Por ejemplo, "forma {DROP TABLE MyTable} es un comando shape perfectamente válido, suponiendo que el proveedor de datos admite DROP TABLE.  
  
 Esta capacidad permite que los comandos de proveedor normal y los comandos shape compartan la misma conexión y transacción.  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de la forma de datos](../../../ado/guide/data/data-shaping-example.md)   
 [Gramática formal de forma](../../../ado/guide/data/formal-shape-grammar.md)   
 [Comandos Shape en General](../../../ado/guide/data/shape-commands-in-general.md)
