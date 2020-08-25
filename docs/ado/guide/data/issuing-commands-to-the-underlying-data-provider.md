---
description: Emitir comandos al proveedor de datos subyacente
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 290ec3a535ac7fe4672f8d0ab6ea19e4d4997333
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "88805882"
---
# <a name="issuing-commands-to-the-underlying-data-provider"></a>Emitir comandos al proveedor de datos subyacente
Cualquier comando que no empiece por SHAPE se pasa a través del proveedor de datos. Esto es equivalente a emitir un comando de forma con el formato "SHAPE {Provider Command}". Estos comandos *no* tienen que generar un **conjunto de registros**. Por ejemplo, "SHAPE {DROP TABLE MyTable} es un comando Shape perfectamente válido, suponiendo que el proveedor de datos admite DROP TABLE.  
  
 Esta funcionalidad permite que los comandos de proveedor normales y los comandos de forma compartan la misma conexión y transacción.  
  
## <a name="see-also"></a>Consulte también  
 [Ejemplo de forma de datos](./data-shaping-example.md)   
 [Gramática de forma formal](./formal-shape-grammar.md)   
 [Comandos Shape en General](./shape-commands-in-general.md)