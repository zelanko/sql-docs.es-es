---
title: Información de error relacionada con el conjunto de registros | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Recordset-related errors [ADO]
- errors [ADO], Recordset-related
ms.assetid: 7e103574-59ad-4790-b5f9-fa8d715e711e
author: rothja
ms.author: jroth
ms.openlocfilehash: cb51fa80cff0a17340e289886f0315ea167b88b0
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760961"
---
# <a name="recordset-related-error-information"></a>Información de Error relacionado con el conjunto de registros
Durante el procesamiento por lotes, la propiedad **status** del objeto de **conjunto de registros** proporciona información sobre los registros individuales del **conjunto de registros**. Antes de que tenga lugar una actualización por lotes, la propiedad **status** del **conjunto de registros** refleja información acerca de los registros que se van a agregar, modificar y eliminar. Después de llamar a **UpdateBatch** , la propiedad **status** indica si la operación se ha realizado correctamente o no. A medida que se mueve de un registro a otro en el **conjunto de registros**, el valor de la propiedad **status** cambia para describir el estado del registro actual.
