---
title: Editar los registros existentes | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- editing data [ADO], existing records
ms.assetid: 17ce1263-5897-452a-9ea5-c7f96b33df65
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: e5c003dc06c9f7e3c598eb73c883b8a0ea160be8
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="editing-existing-records"></a>Editar los registros existentes
Para editar los registros existentes, vaya a la fila que desea editar y cambiar la **valor** propiedad de los campos que desea cambiar. Para obtener más información sobre la **campo** del objeto **valor** propiedad, vea [examinar datos](../../../ado/guide/data/examining-data.md). Dependiendo del tipo de cursor, se utilizará **actualización** o **UpdateBatch** para enviar los cambios en el origen de datos. Para obtener más información, consulte [actualizar y conservar datos](../../../ado/guide/data/updating-and-persisting-data.md).  
  
 Es normalmente más eficaz utilizar un procedimiento almacenado con un objeto de comando para realizar actualizaciones, así como para realizar otras operaciones, ya que un procedimiento almacenado no requiere la creación de un cursor. Para obtener más información acerca de los cursores, vea [cursores y bloqueos](../../../ado/guide/data/understanding-cursors-and-locks.md).
