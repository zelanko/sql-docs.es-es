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
ms.openlocfilehash: 11ab68775e19ec1d3ce3c888917588f41ad65287
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924636"
---
# <a name="persisting-filtered-and-hierarchical-recordsets"></a>Almacenar conjuntos de registros filtrados y jerárquicos
Si el [filtro](../../../ado/reference/ado-api/filter-property.md) propiedad está en vigor para la **Recordset**, se guardan las filas accesibles con el filtro. Si el **Recordset** es jerárquico, el elemento secundario actual **Recordset** y sus elementos secundarios se guardan, incluido el elemento primario **Recordset**. Si el **guardar** método de un elemento secundario **Recordset** es llama, el elemento secundario y todos sus elementos secundarios se guardan, pero el elemento primario no lo es. Para obtener más información acerca de jerárquica **conjuntos de registros**, consulte [dar forma a datos](../../../ado/guide/data/data-shaping.md).  
  
> [!NOTE]
>  Existen algunas limitaciones al guardar jerárquica **conjuntos de registros** (formas de datos) en formato XML. Para obtener más información, consulte [almacenar registros en formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md).
