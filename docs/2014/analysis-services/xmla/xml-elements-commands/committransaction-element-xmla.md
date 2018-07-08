---
title: Elemento CommitTransaction (XMLA) | Microsoft Docs
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
api_name:
- CommitTransaction Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#CommitTransaction
- urn:schemas-microsoft-com:xml-analysis#CommitTransaction
- microsoft.xml.analysis.committransaction
helpviewer_keywords:
- CommitTransaction command
ms.assetid: 1cd814dc-a0be-4305-b44d-faf15e843f7d
caps.latest.revision: 14
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 96510ca95048945bca1b822a5dbc72b02af11fa8
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37152766"
---
# <a name="committransaction-element-xmla"></a>Elemento CommitTransaction (XMLA)
  Confirma una transacción en la sesión actual con un [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Command>  
   <CommitTransaction />  
</Command>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Command](../xml-elements-properties/command-element-xmla.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El comando `CommitTransaction` confirma una transacción activa, explícitamente definida mediante el elemento `BeginTransaction`, en la sesión actual. Si no existe una transacción activa, se produce un error. Si una transacción activa ya existe, la instancia [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] reduce el recuento de referencias de transacciones para la sesión actual. Si el recuento de referencias de transacciones activas explícitamente definidas alcanza cero, la instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] confirma la transacción.  
  
## <a name="see-also"></a>Vea también  
 [Elemento BeginTransaction &#40;XMLA&#41;](begintransaction-element-xmla.md)   
 [Elemento Cancel &#40;XMLA&#41;](cancel-element-xmla.md)   
 [Elemento RollbackTransaction &#40;XMLA&#41;](rollbacktransaction-element-xmla.md)   
 [Comandos &#40;XMLA&#41;](xml-elements-commands.md)  
  
  
