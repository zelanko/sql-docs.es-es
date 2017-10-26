---
title: Elemento BeginTransaction (XMLA) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- BeginTransaction Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#BeginTransaction
- microsoft.xml.analysis.begintransaction
- http://schemas.microsoft.com/analysisservices/2003/engine#BeginTransaction
helpviewer_keywords:
- BeginTransaction command
ms.assetid: fca122fc-b57c-4ba6-849b-ca8c93cf64e9
caps.latest.revision: 14
author: jeannt
ms.author: jeannt
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 677ad07e9ce6206bbc4e7946ec111f8865bcfcce
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="begintransaction-element-xmla"></a>Elemento BeginTransaction (XMLA)
  Comienza una transacción en la sesión actual con una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Command>  
   <BeginTransaction />  
</Command>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|Ninguno|  
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 El comando **BeginTransaction** comienza una transacción activa en la sesión actual. Si una transacción activa ya existe, la instancia [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] incrementa el recuento de referencias de transacciones para la sesión actual. Si no, la instancia comenzará una nueva transacción y establecerá el recuento de referencias de la sesión actual a 1. Si una transacción activa se especifica explícitamente utilizando el comando **BeginTransaction** , todos los comandos subsiguientes se ejecutan dentro de la transacción especificada explícitamente.  
  
 Cuando la sesión actual está finalizada y el recuento de referencias para las transacciones es mayor que cero, se revierten todas las transacciones activas.  
  
 Si no hay ninguna transacción activa especificada explícitamente en la sesión actual, cada comando emitido en la sesión actual se ejecuta dentro de una transacción definida implícitamente. La transacción implícita se confirma si el comando se ejecuta o se revierte si produce un error.  
  
## <a name="see-also"></a>Vea también  
 [Cancelar elemento &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/cancel-element-xmla.md)   
 [Elemento CommitTransaction &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md)   
 [Elemento RollbackTransaction &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md)   
 [Comandos &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  

