---
title: Actualizar datos | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data updates [ADO], about data updates
- updating data [ADO], about updating data
ms.assetid: 6508e4e9-e33a-4dad-b340-5d632fd78a91
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5bd3b72e897b8ae12441c7cf28d1995eb45318d1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67923690"
---
# <a name="updating-data"></a>Actualización de datos
El comportamiento y la funcionalidad de las actualizaciones dependen en gran medida del modo de actualización (tipo de bloqueo), del tipo de cursor y de la ubicación del cursor.  
  
 Utilice el método **Update** para guardar los cambios realizados en el registro actual de un objeto de **conjunto de registros** desde la llamada al método **AddNew** o desde el cambio de los valores de campo de un registro existente. El objeto de **conjunto de registros** debe admitir actualizaciones.  
  
 Si el objeto de **conjunto de registros** admite la actualización por lotes, puede almacenar en caché varios cambios en uno o más registros localmente hasta que se llame al método **UpdateBatch** . Si está editando el registro actual o agregando un nuevo registro cuando se llama al método **UpdateBatch** , ADO llamará automáticamente al método **Update** para guardar los cambios pendientes en el registro actual antes de transmitir los cambios por lotes al proveedor.  
  
 El registro actual sigue siendo actual después de llamar a los métodos **Update** o **UpdateBatch** .  
  
 Esta sección contiene los temas siguientes.  
  
-   [Modo inmediato](../../../ado/guide/data/immediate-mode.md)  
  
-   [Modo por lotes](../../../ado/guide/data/batch-mode.md)  
  
-   [Procesamiento de transacciones](../../../ado/guide/data/transaction-processing.md)
