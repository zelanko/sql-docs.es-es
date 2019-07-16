---
title: Actualizar y almacenar datos | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- updating data [ADO]
- data updates [ADO]
- ADO, updating data
ms.assetid: 8dc27274-4f96-43d1-913c-4ff7d01b9a27
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 26fabdc205018b8e94575cfb5bd5e945a8fb28ca
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67923726"
---
# <a name="updating-and-persisting-data"></a>Actualizar y conservar datos
En los capítulos anteriores se han explicado cómo utilizar ADO para obtener datos de un origen de datos, cómo moverse por los datos e incluso cómo editar los datos. Por supuesto, si el objetivo de la aplicación es permitir a los usuarios realizar cambios en los datos, deberá comprender cómo guardar los cambios. O bien puede conservar la **Recordset** cambia a un archivo mediante el **guardar** método, o bien puede enviar los cambios de vuelta al origen de datos para almacenamiento mediante el **actualización** o  **UpdateBatch** métodos.  
  
 En los capítulos anteriores, ha cambiado los datos en varias filas de la **Recordset**. ADO admite dos nociones básicas relacionadas con la adición, eliminación y modificación de filas de datos.  
  
 El primer concepto es que no se realizan inmediatamente los cambios en el **Recordset**; en su lugar, se realizan en una instancia interna *búfer de copia*. Si decide que no desea que los cambios, se descartan las modificaciones en el búfer de copia. Si decide conservar los cambios, los cambios en el búfer de copia se aplican a la **Recordset**.  
  
 El segundo concepto es que ya se propagan los cambios al origen de datos tan pronto como se declara el trabajo en una fila completa (es decir, *inmediata* modo), o se recopilan todos los cambios en un conjunto de filas hasta que declara el trabajo para el conjunto completa (es decir, *batch* modo). El **LockType** propiedad determina cuándo se realizaron los cambios al origen de datos subyacente. **adLockOptimistic** o **adLockPessimistic** especifica el modo inmediato, mientras que **adLockBatchOptimistic** especifica el modo por lotes. El **CursorLocation** propiedad puede afectar a la que **LockType** opciones están disponibles. Por ejemplo, el **adLockPessimistic** configuración no se admite si el **CursorLocation** propiedad está establecida en **adUseClient**.  
  
 En el modo inmediato, cada invocación de la **actualización** método propaga los cambios al origen de datos. En modo por lotes, cada invocación de **actualización** o movimiento de la posición de fila actual guarda los cambios en el búfer de copia, pero sólo el **UpdateBatch** método propaga los cambios al origen de datos.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Actualización de datos](../../../ado/guide/data/updating-data.md)  
  
-   [Conservar los datos](../../../ado/guide/data/persisting-data.md)
