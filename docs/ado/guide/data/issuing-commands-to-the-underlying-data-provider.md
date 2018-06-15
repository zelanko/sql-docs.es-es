---
title: Emitir comandos al proveedor de datos subyacente | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- underlying providers [ADO]
- data shaping [ADO], commands
ms.assetid: d6001863-7733-4c32-817f-081e48587fa1
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5a2e18440c651a65da820cf2f2d51b00ae98e92d
ms.sourcegitcommit: 62826c291db93c9017ae219f75c3cfeb8140bf06
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/11/2018
ms.locfileid: "35271954"
---
# <a name="issuing-commands-to-the-underlying-data-provider"></a>Emitir comandos al proveedor de datos subyacente
Cualquier comando que no comienzan con forma se pasa al proveedor de datos. Esto es equivalente a la emisión de un comando de forma de la forma "SHAPE {comando de proveedor}". Estos comandos tienen *no* tiene que producir una **conjunto de registros**. Por ejemplo, "forma {DROP TABLE MyTable} es un comando shape perfectamente válido, suponiendo que el proveedor de datos admite DROP TABLE.  
  
 Esta capacidad permite que los comandos de proveedor normal y los comandos shape compartan la misma conexión y transacción.  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de la forma de datos](../../../ado/guide/data/data-shaping-example.md)   
 [Gramática formal de forma](../../../ado/guide/data/formal-shape-grammar.md)   
 [Comandos Shape en General](../../../ado/guide/data/shape-commands-in-general.md)
