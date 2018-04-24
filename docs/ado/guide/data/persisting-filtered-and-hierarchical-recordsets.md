---
title: Conjuntos de registros filtrados y jerárquicos persistentes | Documentos de Microsoft
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
- filtered Recordset persistence [ADO]
- persisting data [ADO]
- data updates [ADO], persisting data
- data persistence [ADO]
- updating data [ADO], persisting data
ms.assetid: d01aeb4d-4e43-450b-b3f2-0c27eaaf9f86
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: d945999ef7feb34ebe7de3b945868bc35c154589
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2018
---
# <a name="persisting-filtered-and-hierarchical-recordsets"></a>Almacenar conjuntos de registros filtrados y jerárquicos
Si el [filtro](../../../ado/reference/ado-api/filter-property.md) propiedad está en vigor para la **Recordset**, se guardan únicamente las filas accesibles con el filtro. Si el **Recordset** es jerárquico, el elemento secundario actual **Recordset** y sus elementos secundarios se guardan, incluida la primaria **conjunto de registros**. Si el **guardar** método de un elemento secundario **Recordset** es llama, el elemento secundario y todos sus elementos secundarios se guardan, pero el elemento primario no lo es. Para obtener más información acerca de jerárquica **conjuntos de registros**, consulte [dar forma a datos](../../../ado/guide/data/data-shaping.md).  
  
> [!NOTE]
>  Existen algunas limitaciones cuando se guarda jerárquica **conjuntos de registros** (formas de datos) en formato XML. Para obtener más información, consulte [almacenar registros en formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md).
