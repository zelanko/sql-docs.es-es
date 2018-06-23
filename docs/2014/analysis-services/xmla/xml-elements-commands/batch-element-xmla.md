---
title: Procesar por lotes elemento (XMLA) | Documentos de Microsoft
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
- Batch Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Batch
- microsoft.xml.analysis.batch
- http://schemas.microsoft.com/analysisservices/2003/engine#Batch
helpviewer_keywords:
- Batch command
ms.assetid: 818f3212-9605-4e34-8623-1154d9fae1f0
caps.latest.revision: 14
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 76fcd68ca71db298bc66dc63a3fa20c394c196c8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36201894"
---
# <a name="batch-element-xmla"></a>Elemento Batch (XMLA)
  Realiza XML de uno o más para los comandos de Analysis (XMLA) como una operación por lotes, ya sea de forma secuencial o en paralelo, en una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<Command>  
   <Batch Transaction="Boolean" ProcessAffectedObjects="Boolean">  
      <Bindings>...</Bindings>  
      <DataSource>...</DataSource>  
      <DataSourceView>...</DataSourceView>  
      <ErrorConfiguration>...</ErrorConfiguration>  
      <Parallel>...</Parallel>  
      <!-- One or more XMLA commands -->  
   </Batch>  
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
|Elementos secundarios|[Enlaces](../xml-elements-properties/bindings-element-xmla.md), [DataSource](../xml-elements-properties/source-element-xmla.md), [DataSourceView](../xml-elements-properties/datasourceview-element-xmla.md), [ErrorConfiguration](../../scripting/objects/errorconfiguration-element-assl.md), [paralelas](../xml-elements-properties/parallel-element-xmla.md)<br /><br /> One or more of the following XMLA commands: [Alter](alter-element-xmla.md), [Backup](backup-element-xmla.md), [BeginTransaction](begintransaction-element-xmla.md), [ClearCache](clearcache-element-xmla.md), [CommitTransaction](committransaction-element-xmla.md), [Create](create-element-xmla.md), [Delete](delete-element-xmla.md), [DesignAggregations](designaggregations-element-xmla.md), [Drop](drop-element-xmla.md), [Insert](insert-element-xmla.md), [Lock](lock-element-xmla.md), [MergePartitions](mergepartitions-element-xmla.md), [NotifyTableChange](notifytablechange-element-xmla.md), [Process](process-element-xmla.md), [Restore](restore-element-xmla.md), [RollbackTransaction](rollbacktransaction-element-xmla.md), [SetPasswordEncryptionKey](http://msdn.microsoft.com/en-us/fb262737-f0f4-4441-985e-3b2a94d00a9e), [Statement](statement-element-xmla.md), [Subscribe](subscribe-element-xmla.md), [Synchronize](synchronize-element-xmla.md), [Unlock](unlock-element-xmla.md), [Update](update-element-xmla.md), [UpdateCells](drop-element-xmla.md)|  
  
## <a name="attributes"></a>Atributos  
  
|Attribute|Descripción|  
|---------------|-----------------|  
|ProcessAffectedObjects|(Atributo `Boolean` opcional) Indica si se procesarán todos los objetos que requieren reprocesamiento.<br /><br /> Si se establece en true, la instancia [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] procesa los objetos que requieren reprocesamiento como resultado de procesar un objeto incluido en el comando `Batch`.<br /><br /> Si se establece en `false`, la instancia [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] procesa solo los objetos incluidos en el comando `Batch`.|  
|Transaction|(Atributo `Boolean` opcional) Indica si el comando incluido en el comando `Batch` se trata como una transacción única o como transacciones individuales.<br /><br /> Si se establece en true, todos los comandos incluidos en el comando `Batch` se consideran una transacción única. Si se produce un error en el comando, los comandos ejecutados antes del comando que ha devuelto un error se revierten y el comando `Batch` se detiene sin ejecutar los comandos posteriores.<br /><br /> Si se establece en `false`, el comando `Batch` intenta ejecutar todos los comandos y confirma los resultados de cada comando que se completa correctamente.|  
  
## <a name="remarks"></a>Notas  
  
> [!WARNING]  
>  Command/Execute/Statement no se admite actualmente en una operación por lotes.  
  
 Para obtener más información acerca de cómo realizar operaciones por lotes en XMLA, vea [realizar operaciones por lotes &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/performing-batch-operations-xmla.md).  
  
## <a name="see-also"></a>Vea también  
 [Comandos &#40;XMLA&#41;](xml-elements-commands.md)  
  
  