---
title: "Posición de conjunto de registros | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- record positioning [ADO]
- Recordset object [ADO]
- repositioning record [ADO]
- AbsolutePosition property [ADO]
ms.assetid: c8f6fbcb-6675-4133-b37e-430de43949c1
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fe94f3a39a42bedd5bd3d1569e5210320b1e7c4f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="recordset-positioning"></a>Posición de conjunto de registros
Use la **AbsolutePosition** propiedad que se va a mover a un registro, en función de su posición ordinal en la **Recordset** objeto, o para determinar la posición ordinal del registro actual. El proveedor debe admitir la funcionalidad adecuada para que esta propiedad esté disponible.  
  
 **AbsolutePosition** está basado en 1 y es igual a 1 cuando el registro actual es el primer registro de la **conjunto de registros**. Como se mencionó anteriormente, puede obtener el número total de registros en el **Recordset** objeto desde el **RecordCount** propiedad.  
  
 Al establecer el **AbsolutePosition** propiedad, incluso si es a un registro en la memoria caché actual, ADO vuelve a cargar la memoria caché con un nuevo grupo de registros empezando por el registro especificado. El **CacheSize** propiedad determina el tamaño de este grupo.  
  
> [!NOTE]
>  No debe utilizar el **AbsolutePosition** propiedad como un número de registro suplente. La posición de un registro determinado cambia cuando se elimina un registro anterior. También no hay ninguna garantía de que un registro determinado tenga el mismo **AbsolutePosition** si la **Recordset** objeto se realiza una nueva consulta o se vuelve a abrir. Los marcadores son el método recomendado para retener y volver a una posición determinada y son la única manera de ubicarse a través de todos los tipos de **Recordset** objetos.
