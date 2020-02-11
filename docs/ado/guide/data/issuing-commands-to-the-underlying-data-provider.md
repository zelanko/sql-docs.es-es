---
title: Emitir comandos para el proveedor de datos subyacente | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- underlying providers [ADO]
- data shaping [ADO], commands
ms.assetid: d6001863-7733-4c32-817f-081e48587fa1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 02a861daa78b798c1b19b5fc2607cfcaf0ce5968
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67924944"
---
# <a name="issuing-commands-to-the-underlying-data-provider"></a>Emitir comandos al proveedor de datos subyacente
Cualquier comando que no empiece por SHAPE se pasa a través del proveedor de datos. Esto es equivalente a emitir un comando de forma con el formato "SHAPE {Provider Command}". Estos comandos *no* tienen que generar un **conjunto de registros**. Por ejemplo, "SHAPE {DROP TABLE MyTable} es un comando Shape perfectamente válido, suponiendo que el proveedor de datos admite DROP TABLE.  
  
 Esta funcionalidad permite que los comandos de proveedor normales y los comandos de forma compartan la misma conexión y transacción.  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de forma de datos](../../../ado/guide/data/data-shaping-example.md)   
 [Gramática de forma formal](../../../ado/guide/data/formal-shape-grammar.md)   
 [Comandos Shape en General](../../../ado/guide/data/shape-commands-in-general.md)
