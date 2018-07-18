---
title: Elemento BeginTransaction (XMLA) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: eb4a4dea3658ad03fd6205f9076bd1cb65ca9ba7
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38038383"
---
# <a name="begintransaction-element-xmla"></a>Elemento BeginTransaction (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Comienza una transacción en la sesión actual con una instancia de Analysis Services.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Command>  
   <BeginTransaction />  
</Command>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones de elementos  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Notas  
 El comando **BeginTransaction** comienza una transacción activa en la sesión actual. Si una transacción activa ya existe, la instancia [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] incrementa el recuento de referencias de transacciones para la sesión actual. Si no, la instancia comenzará una nueva transacción y establecerá el recuento de referencias de la sesión actual a 1. Si una transacción activa se especifica explícitamente utilizando el comando **BeginTransaction** , todos los comandos subsiguientes se ejecutan dentro de la transacción especificada explícitamente.  
  
 Cuando la sesión actual está finalizada y el recuento de referencias para las transacciones es mayor que cero, se revierten todas las transacciones activas.  
  
 Si no hay ninguna transacción activa especificada explícitamente en la sesión actual, cada comando emitido en la sesión actual se ejecuta dentro de una transacción definida implícitamente. La transacción implícita se confirma si el comando se ejecuta o se revierte si produce un error.  
  
## <a name="see-also"></a>Vea también
 [Elemento Cancel &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md)   
 [Elemento CommitTransaction &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md)   
 [Elemento RollbackTransaction &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md)   
 [Comandos &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
