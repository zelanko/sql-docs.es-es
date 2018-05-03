---
title: Editar los registros existentes | Documentos de Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- editing data [ADO], existing records
ms.assetid: 17ce1263-5897-452a-9ea5-c7f96b33df65
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f6caa67868172118f7e70b1781b7fbb08ec22641
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="editing-existing-records"></a>Editar los registros existentes
Para editar los registros existentes, vaya a la fila que desea editar y cambiar la **valor** propiedad de los campos que desea cambiar. Para obtener más información sobre la **campo** del objeto **valor** propiedad, vea [examinar datos](../../../ado/guide/data/examining-data.md). Dependiendo del tipo de cursor, se utilizará **actualización** o **UpdateBatch** para enviar los cambios en el origen de datos. Para obtener más información, consulte [actualizar y conservar datos](../../../ado/guide/data/updating-and-persisting-data.md).  
  
 Es normalmente más eficaz utilizar un procedimiento almacenado con un objeto de comando para realizar actualizaciones, así como para realizar otras operaciones, ya que un procedimiento almacenado no requiere la creación de un cursor. Para obtener más información acerca de los cursores, vea [cursores y bloqueos](../../../ado/guide/data/understanding-cursors-and-locks.md).
