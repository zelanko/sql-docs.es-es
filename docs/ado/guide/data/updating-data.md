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
author: rothja
ms.author: jroth
ms.openlocfilehash: 26f3ca9220ea41db43b9f98a12429dcb5874bba4
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82750225"
---
# <a name="updating-data"></a>Actualización de datos
El comportamiento y la funcionalidad de las actualizaciones dependen en gran medida del modo de actualización (tipo de bloqueo), del tipo de cursor y de la ubicación del cursor.  
  
 Utilice el método **Update** para guardar los cambios realizados en el registro actual de un objeto de **conjunto de registros** desde la llamada al método **AddNew** o desde el cambio de los valores de campo de un registro existente. El objeto de **conjunto de registros** debe admitir actualizaciones.  
  
 Si el objeto de **conjunto de registros** admite la actualización por lotes, puede almacenar en caché varios cambios en uno o más registros localmente hasta que se llame al método **UpdateBatch** . Si está editando el registro actual o agregando un nuevo registro cuando se llama al método **UpdateBatch** , ADO llamará automáticamente al método **Update** para guardar los cambios pendientes en el registro actual antes de transmitir los cambios por lotes al proveedor.  
  
 El registro actual sigue siendo actual después de llamar a los métodos **Update** o **UpdateBatch** .  
  
 Esta sección contiene los temas siguientes.  
  
-   [Modo inmediato](../../../ado/guide/data/immediate-mode.md)  
  
-   [Batch Mode](../../../ado/guide/data/batch-mode.md)  
  
-   [Procesar transacciones](../../../ado/guide/data/transaction-processing.md)
