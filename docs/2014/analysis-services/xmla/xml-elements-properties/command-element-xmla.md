---
title: Comando elemento (XMLA) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Command Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.command
- Command
- urn:schemas-microsoft-com:xml-analysis#Command
- http://schemas.microsoft.com/analysisservices/2003/engine#Command
helpviewer_keywords:
- Command element
ms.assetid: 9abc14df-7cbe-46bc-ba0f-f0691c19afad
caps.latest.revision: 31
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: b054c940ae68c8bc7b252349a538777757283da4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36112088"
---
# <a name="command-element-xmla"></a>Elemento Command (XMLA)
  Contiene el comando que va a ejecutar la [Execute](../xml-elements-methods-execute.md) método.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Execute>  
   ...  
   <Command>  
      <Alter>...</Alter>  
      <!-- or -->  
      <Backup>...</Backup>  
      <!-- or -->  
      <Batch>...</Batch>  
      <!-- or -->  
      <BeginTransaction>...</BeginTransaction>  
      <!-- or -->  
      <Cancel>...</Cancel>  
      <!-- or -->  
      <ClearCache>...</ClearCache>  
      <!-- or -->  
      <CommitTransaction>...</CommitTransaction>  
      <!-- or -->  
      <Create>...</Create>  
      <!-- or -->  
      <Delete>...</Delete>  
      <!-- or -->  
      <DesignAggregations>...</DesignAggregations>  
      <!-- or -->  
      <Drop>...</Drop>  
      <!-- or -->  
      <Insert>...</Insert>  
      <!-- or -->  
      <Lock>...</Lock>  
      <!-- or -->  
      <MergePartitions>...</MergePartitions>  
      <!-- or -->  
      <NotifyTableChange>...</NotifyTableChange>  
      <!-- or -->  
      <Process>...</Process>  
      <!-- or -->  
      <Restore>...</Restore>  
      <!-- or -->  
      <RollbackTransaction>...</RollbackTransaction>  
      <!-- or -->  
      <SetPasswordEncryptionKey>...</SetPasswordEncryptionKey>  
      <!-- or -->  
      <Statement>...</Statement>  
      <!-- or -->  
      <Subscribe>...</Subscribe>  
      <!-- or -->  
      <Synchronize>...</Synchronize>  
      <!-- or -->  
      <Unlock>...</Unlock>  
      <!-- or -->  
      <Update>...</Update>  
      <!-- or -->  
      <UpdateCells>...</UpdateCells>  
   </Command>  
   ...  
</Execute>  
```  
  
## <a name="element-characteristics"></a>Características del elemento  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|1-1: Elemento necesario que se produce una vez y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Ejecutar](../xml-elements-methods-execute.md)|  
|Elementos secundarios|[Alter](../xml-elements-commands/alter-element-xmla.md), [Backup](../xml-elements-commands/backup-element-xmla.md), [Batch](../xml-elements-commands/batch-element-xmla.md), [BeginTransaction](../xml-elements-commands/begintransaction-element-xmla.md), [Cancel](../xml-elements-commands/cancel-element-xmla.md), [ClearCache](../xml-elements-commands/clearcache-element-xmla.md), [CommitTransaction](../xml-elements-commands/committransaction-element-xmla.md), [Create](../xml-elements-commands/create-element-xmla.md), [Delete](../xml-elements-commands/delete-element-xmla.md), [DesignAggregations](../xml-elements-commands/designaggregations-element-xmla.md), [Drop](../xml-elements-commands/drop-element-xmla.md), [Insert](../xml-elements-commands/insert-element-xmla.md), [Lock](../xml-elements-commands/lock-element-xmla.md), [MergePartitions](../xml-elements-commands/mergepartitions-element-xmla.md), [NotifyTableChange](../xml-elements-commands/notifytablechange-element-xmla.md), [Process](../xml-elements-commands/process-element-xmla.md), [Restore](../xml-elements-commands/restore-element-xmla.md), [RollbackTransaction](../xml-elements-commands/rollbacktransaction-element-xmla.md), [SetPasswordEncryptionKey](http://msdn.microsoft.com/en-us/fb262737-f0f4-4441-985e-3b2a94d00a9e), [Statement](../xml-elements-commands/statement-element-xmla.md), [Subscribe](../xml-elements-commands/subscribe-element-xmla.md), [Synchronize](../xml-elements-commands/synchronize-element-xmla.md), [Unlock](../xml-elements-commands/unlock-element-xmla.md), [Update](../xml-elements-commands/update-element-xmla.md), [UpdateCells](../xml-elements-commands/drop-element-xmla.md)|  
  
## <a name="remarks"></a>Notas  
 El método `Command` utiliza el elemento `Execute` para retransmitir comandos a un origen de datos. Mientras que el código XML de especificación de Analysis (XMLA) 1.1 solo admite la `Statement` comando, [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] admite numerosos comandos XMLA nuevos. Para obtener más información acerca de los comandos XMLA admitidos por [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], consulte [comandos &#40;XMLA&#41;](../xml-elements-commands/xml-elements-commands.md).  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos XML &#40;XMLA&#41;](../xml-data-types/xml-data-types-xmla.md)   
 [Propiedades &#40;XMLA&#41;](xml-elements-properties.md)  
  
  