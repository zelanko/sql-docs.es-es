---
title: Conservar conjuntos de registros jerárquicos y filtrados | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- filtered Recordset persistence [ADO]
- persisting data [ADO]
- data updates [ADO], persisting data
- data persistence [ADO]
- updating data [ADO], persisting data
ms.assetid: d01aeb4d-4e43-450b-b3f2-0c27eaaf9f86
author: rothja
ms.author: jroth
ms.openlocfilehash: 5fa3fdd55fb78f16629907c174b08aab64ceb86e
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2020
ms.locfileid: "82763116"
---
# <a name="persisting-filtered-and-hierarchical-recordsets"></a>Almacenar conjuntos de registros filtrados y jerárquicos
Si la propiedad [Filter](../../../ado/reference/ado-api/filter-property.md) está en vigor para el **conjunto de registros**, solo se guardan las filas a las que se puede tener acceso en el filtro. Si el **conjunto de registros** es jerárquico, se guardan el **conjunto de registros** secundario actual y sus elementos secundarios, incluido el **conjunto de registros**primario. Si se llama al método **Save** de un **conjunto de registros** secundario, se guardan el elemento secundario y todos sus elementos secundarios, pero el elemento primario no lo es. Para obtener más información sobre los **conjuntos de registros**jerárquicos, vea [modelado de datos](../../../ado/guide/data/data-shaping.md).  
  
> [!NOTE]
>  Se aplican algunas limitaciones al guardar **conjuntos de registros** jerárquicos (formas de datos) en formato XML. Para obtener más información, vea [guardar registros en formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md).
