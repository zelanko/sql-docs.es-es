---
title: Emisión de comandos al proveedor de datos subyacente | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 2267ff0af67682417b118e9fa01b2dceeb1454a8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63161438"
---
# <a name="issuing-commands-to-the-underlying-data-provider"></a>Emitir comandos al proveedor de datos subyacente
Cualquier comando que no comienzan con la forma se pasa al proveedor de datos. Esto equivale a enviar un comando de la forma en la forma "SHAPE {comando de proveedor}". Estos comandos *no* tienen que producir una **Recordset**. Por ejemplo, "SHAPE {DROP TABLE MyTable} es un comando shape perfectamente válido, suponiendo que el proveedor de datos admite DROP TABLE.  
  
 Esta funcionalidad permite a los comandos de proveedor normal y comandos de forma que comparten la misma conexión y transacción.  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de la forma de datos](../../../ado/guide/data/data-shaping-example.md)   
 [Gramática formal de forma](../../../ado/guide/data/formal-shape-grammar.md)   
 [Comandos Shape en General](../../../ado/guide/data/shape-commands-in-general.md)
