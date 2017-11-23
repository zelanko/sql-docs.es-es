---
title: Editar los registros existentes | Documentos de Microsoft
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
helpviewer_keywords: editing data [ADO], existing records
ms.assetid: 17ce1263-5897-452a-9ea5-c7f96b33df65
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b901a7c43ab9df743feff98fbf90959b8a132807
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="editing-existing-records"></a>Editar los registros existentes
Para editar los registros existentes, vaya a la fila que desea editar y cambiar la **valor** propiedad de los campos que desea cambiar. Para obtener más información sobre la **campo** del objeto **valor** propiedad, vea [examinar datos](../../../ado/guide/data/examining-data.md). Dependiendo del tipo de cursor, se utilizará **actualización** o **UpdateBatch** para enviar los cambios en el origen de datos. Para obtener más información, consulte [actualizar y conservar datos](../../../ado/guide/data/updating-and-persisting-data.md).  
  
 Es normalmente más eficaz utilizar un procedimiento almacenado con un objeto de comando para realizar actualizaciones, así como para realizar otras operaciones, ya que un procedimiento almacenado no requiere la creación de un cursor. Para obtener más información acerca de los cursores, vea [cursores y bloqueos](../../../ado/guide/data/understanding-cursors-and-locks.md).
