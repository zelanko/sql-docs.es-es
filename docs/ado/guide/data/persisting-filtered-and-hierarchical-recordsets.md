---
title: Almacenar conjuntos de registros filtrados y jerárquicos | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: cbd237580dc8c56284552e6fe2fb00e469832c5b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66702046"
---
# <a name="persisting-filtered-and-hierarchical-recordsets"></a>Almacenar conjuntos de registros filtrados y jerárquicos
Si el [filtro](../../../ado/reference/ado-api/filter-property.md) propiedad está en vigor para la **Recordset**, se guardan las filas accesibles con el filtro. Si el **Recordset** es jerárquico, el elemento secundario actual **Recordset** y sus elementos secundarios se guardan, incluido el elemento primario **Recordset**. Si el **guardar** método de un elemento secundario **Recordset** es llama, el elemento secundario y todos sus elementos secundarios se guardan, pero el elemento primario no lo es. Para obtener más información acerca de jerárquica **conjuntos de registros**, consulte [dar forma a datos](../../../ado/guide/data/data-shaping.md).  
  
> [!NOTE]
>  Existen algunas limitaciones al guardar jerárquica **conjuntos de registros** (formas de datos) en formato XML. Para obtener más información, consulte [almacenar registros en formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md).
