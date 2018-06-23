---
title: Elemento role (XMLA) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 2b851ad5-cc46-4a2e-8873-d8556faca809
caps.latest.revision: 5
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: bc1b3e4733625334e284946338beaaa7f65e7f0d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36203490"
---
# <a name="role-element--xmla"></a>Elemento role (XMLA)
  Identifica un extremo de una relación uno a varios que va a usar el elemento primario [RelationshipEnd](../../scripting/data-type/relationshipend-data-type-assl.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<RelationshipEnd  
   ...  
   <Role>...</Role>  
   ...  
</RelationshipEnd>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String|  
|Valor predeterminado|None|  
|Cardinalidad|1: elemento necesario que puede aparecer una vez y solo una vez|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[RelationshipEnd](../../scripting/data-type/relationshipend-data-type-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
  