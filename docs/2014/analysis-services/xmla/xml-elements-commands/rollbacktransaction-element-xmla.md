---
title: Elemento RollbackTransaction (XMLA) | Microsoft Docs
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
- RollbackTransaction Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#RollbackTransaction
- microsoft.xml.analysis.rollbacktransaction
- urn:schemas-microsoft-com:xml-analysis#RollbackTransaction
helpviewer_keywords:
- RollbackTransaction command
ms.assetid: 40e7dc00-656f-412f-97f0-d05bf7caa196
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: eaaf3d92849e0d2ddb7f94686bb30e627d3abcb7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37300805"
---
# <a name="rollbacktransaction-element-xmla"></a>Elemento RollbackTransaction (XMLA)
  Revierte una transacción en la sesión actual con una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Command>  
   <RollbackTransaction />  
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
 El comando `RollbackTransaction` revierte todas las transacciones activas, definidas explícitamente mediante el elemento `BeginTransaction`, en la sesión actual. Si no existe una transacción activa, se produce un error. Si ya existe una transacción activa, la instancia [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] reduce el recuento de referencias de transacciones para la sesión actual a cero, revirtiendo todas las transacciones activas.  
  
## <a name="see-also"></a>Vea también  
 [Elemento BeginTransaction &#40;XMLA&#41;](begintransaction-element-xmla.md)   
 [Elemento Cancel &#40;XMLA&#41;](cancel-element-xmla.md)   
 [Elemento CommitTransaction &#40;XMLA&#41;](committransaction-element-xmla.md)   
 [Comandos &#40;XMLA&#41;](xml-elements-commands.md)  
  
  
