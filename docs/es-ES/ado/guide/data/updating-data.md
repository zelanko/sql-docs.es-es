---
title: Actualización de datos | Documentos de Microsoft
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
- data updates [ADO], about data updates
- updating data [ADO], about updating data
ms.assetid: 6508e4e9-e33a-4dad-b340-5d632fd78a91
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cc4f82996079bda6ba54f5329f8c78158677bc8d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="updating-data"></a>Actualización de datos
Comportamiento de actualización y la funcionalidad depende en gran medida actualizar modo (tipo de bloqueo), el tipo de cursor y la ubicación del cursor.  
  
 Use la **actualización** método para guardar los cambios realizados en el registro actual de un **conjunto de registros** objeto desde el que realiza la llamada la **AddNew** método o cambiando los valores de campo en un registro existente. El **Recordset** objeto debe admitir las actualizaciones.  
  
 Si el **Recordset** objeto admite la actualización por lotes, puede almacenar en caché cualquier cambio múltiple en uno o más registros localmente hasta que llame a la **UpdateBatch** método. Si está modificando el registro actual o agregando un nuevo registro cuando se llama a la **UpdateBatch** método, ADO llamará automáticamente el **actualización** método para guardar los cambios pendientes en el registro actual antes de transmitir los cambios por lotes al proveedor.  
  
 El registro actual se mantiene actual después de llamar a la **actualización** o **UpdateBatch** métodos.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Modo inmediato](../../../ado/guide/data/immediate-mode.md)  
  
-   [Modo por lotes](../../../ado/guide/data/batch-mode.md)  
  
-   [Procesamiento de transacciones](../../../ado/guide/data/transaction-processing.md)
