---
description: Almacenar conjuntos de registros filtrados y jerárquicos
title: Conservar conjuntos de registros jerárquicos y filtrados | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: fc18622d3fda977d4a19d9946430c9e1cd0b2444
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2020
ms.locfileid: "88980096"
---
# <a name="persisting-filtered-and-hierarchical-recordsets"></a>Almacenar conjuntos de registros filtrados y jerárquicos
Si la propiedad [Filter](../../../ado/reference/ado-api/filter-property.md) está en vigor para el **conjunto de registros**, solo se guardan las filas a las que se puede tener acceso en el filtro. Si el **conjunto de registros** es jerárquico, se guardan el **conjunto de registros** secundario actual y sus elementos secundarios, incluido el **conjunto de registros**primario. Si se llama al método **Save** de un **conjunto de registros** secundario, se guardan el elemento secundario y todos sus elementos secundarios, pero el elemento primario no lo es. Para obtener más información sobre los **conjuntos de registros**jerárquicos, vea [modelado de datos](../../../ado/guide/data/data-shaping.md).  
  
> [!NOTE]
>  Se aplican algunas limitaciones al guardar **conjuntos de registros** jerárquicos (formas de datos) en formato XML. Para obtener más información, vea [guardar registros en formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md).
