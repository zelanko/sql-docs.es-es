---
description: Posición de conjunto de registros
title: Posicionamiento del conjunto de registros | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 1f97f5b9c9a947362edffaa88f878c96d63b270f
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88979886"
---
# <a name="recordset-positioning"></a>Posición de conjunto de registros
Use la propiedad **AbsolutePosition** para moverse a un registro, en función de su posición ordinal en el objeto de **conjunto de registros** , o para determinar la posición ordinal del registro actual. El proveedor debe admitir la funcionalidad adecuada para que esta propiedad esté disponible.  
  
 **AbsolutePosition** es de base 1 y es igual a 1 cuando el registro actual es el primer registro del **conjunto de registros**. Como se mencionó anteriormente, puede obtener el número total de registros en el objeto de **conjunto de registros** de la propiedad **RecordCount** .  
  
 Cuando se establece la propiedad **AbsolutePosition** , incluso si se trata de un registro en la caché actual, ADO vuelve a cargar la memoria caché con un nuevo grupo de registros a partir del registro especificado. La propiedad **CacheSize** determina el tamaño de este grupo.  
  
> [!NOTE]
>  No debe utilizar la propiedad **AbsolutePosition** como un número de registro suplente. La posición de un registro determinado cambia cuando se elimina un registro anterior. Tampoco hay ninguna garantía de que un registro determinado tendrá el mismo **AbsolutePosition** si el objeto de **conjunto de registros** se reconsulta o se vuelve a abrir. Los marcadores son el método recomendado para conservar y volver a una posición determinada y son la única forma de colocar en todos los tipos de objetos de **conjunto de registros** .
