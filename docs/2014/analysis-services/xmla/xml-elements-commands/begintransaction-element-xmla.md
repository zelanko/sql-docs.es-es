---
title: Elemento BeginTransaction (XMLA) | Microsoft Docs
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
- BeginTransaction Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#BeginTransaction
- microsoft.xml.analysis.begintransaction
- http://schemas.microsoft.com/analysisservices/2003/engine#BeginTransaction
helpviewer_keywords:
- BeginTransaction command
ms.assetid: fca122fc-b57c-4ba6-849b-ca8c93cf64e9
caps.latest.revision: 14
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1685c1c61c248cf37672cab17ccf3144e7d5e7ec
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37253047"
---
# <a name="begintransaction-element-xmla"></a>Elemento BeginTransaction (XMLA)
  Comienza una transacción en la sesión actual con una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Command>  
   <BeginTransaction />  
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
 El comando `BeginTransaction` comienza una transacción activa en la sesión actual. Si una transacción activa ya existe, la instancia [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] incrementa el recuento de referencias de transacciones para la sesión actual. Si no, la instancia comenzará una nueva transacción y establecerá el recuento de referencias de la sesión actual a 1. Si una transacción activa se especifica explícitamente utilizando el comando `BeginTransaction`, todos los comandos subsiguientes se ejecutan dentro de la transacción especificada explícitamente.  
  
 Cuando la sesión actual está finalizada y el recuento de referencias para las transacciones es mayor que cero, se revierten todas las transacciones activas.  
  
 Si no hay ninguna transacción activa especificada explícitamente en la sesión actual, cada comando emitido en la sesión actual se ejecuta dentro de una transacción definida implícitamente. La transacción implícita se confirma si el comando se ejecuta o se revierte si produce un error.  
  
## <a name="see-also"></a>Vea también  
 [Elemento Cancel &#40;XMLA&#41;](cancel-element-xmla.md)   
 [Elemento CommitTransaction &#40;XMLA&#41;](committransaction-element-xmla.md)   
 [Elemento RollbackTransaction &#40;XMLA&#41;](rollbacktransaction-element-xmla.md)   
 [Comandos &#40;XMLA&#41;](xml-elements-commands.md)  
  
  
