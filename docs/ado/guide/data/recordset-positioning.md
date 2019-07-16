---
title: Posición del conjunto de registros | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- record positioning [ADO]
- Recordset object [ADO]
- repositioning record [ADO]
- AbsolutePosition property [ADO]
ms.assetid: c8f6fbcb-6675-4133-b37e-430de43949c1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cdce4c7b08a8b15cdb0a9ee1111a216aeef005bf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924431"
---
# <a name="recordset-positioning"></a>Posición de conjunto de registros
Use la **AbsolutePosition** propiedad que se va a mover a un registro, según su posición ordinal en la **Recordset** objeto, o para determinar la posición ordinal del registro actual. El proveedor debe admitir la funcionalidad adecuada para esta propiedad esté disponible.  
  
 **AbsolutePosition** está basado en 1 y es igual a 1 cuando el registro actual es el primer registro en el **Recordset**. Como se mencionó anteriormente, puede obtener el número total de registros en el **Recordset** objeto desde el **RecordCount** propiedad.  
  
 Al establecer el **AbsolutePosition** propiedad, incluso si se van a un registro en la memoria caché actual, ADO vuelve a cargar la memoria caché con un nuevo grupo de registros empezando por el registro especificado. El **CacheSize** propiedad determina el tamaño de este grupo.  
  
> [!NOTE]
>  No se debe usar el **AbsolutePosition** propiedad como un número de registro suplente. La posición de un registro determinado cambia cuando se elimina un registro anterior. También no hay ninguna garantía de que un registro determinado tendrá el mismo **AbsolutePosition** si el **Recordset** objeto se vuelve a consultar o se vuelve a abrir. Los marcadores son el método recomendado para mantener y volver a una posición determinada y son la única manera de posicionamiento en todos los tipos de **Recordset** objetos.
