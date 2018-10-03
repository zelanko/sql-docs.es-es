---
title: Procesar por lotes (XMLA) del elemento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d402c1f6c35370a506ed57c43b8fbc05d0b6bef7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48178145"
---
# <a name="batch-element-xmla"></a>Elemento Batch (XMLA)
  Realiza una o varias de XML para los comandos de Analysis (XMLA) como una operación por lotes, secuencialmente o en paralelo, en una instancia de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
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
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|None|  
|Valor predeterminado|None|  
|Cardinalidad|0-n: elemento opcional que puede aparecer más de una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elementos primarios|[Command](../xml-elements-properties/command-element-xmla.md)|  
|Elementos secundarios|[Enlaces](../xml-elements-properties/bindings-element-xmla.md), [DataSource](../xml-elements-properties/source-element-xmla.md), [DataSourceView](../xml-elements-properties/datasourceview-element-xmla.md), [ErrorConfiguration](../../scripting/objects/errorconfiguration-element-assl.md), [paralelo](../xml-elements-properties/parallel-element-xmla.md)<br /><br /> Uno o varios de los siguientes comandos XMLA: [Alter](alter-element-xmla.md), [copia de seguridad](backup-element-xmla.md), [BeginTransaction](begintransaction-element-xmla.md), [ClearCache](clearcache-element-xmla.md), [ CommitTransaction](committransaction-element-xmla.md), [crear](create-element-xmla.md), [eliminar](delete-element-xmla.md), [DesignAggregations](designaggregations-element-xmla.md), [Drop](drop-element-xmla.md), [Insertar](insert-element-xmla.md), [bloqueo](lock-element-xmla.md), [MergePartitions](mergepartitions-element-xmla.md), [NotifyTableChange](notifytablechange-element-xmla.md), [proceso](process-element-xmla.md), [Restaurar](restore-element-xmla.md), [RollbackTransaction](rollbacktransaction-element-xmla.md), [SetPasswordEncryptionKey](http://msdn.microsoft.com/en-us/fb262737-f0f4-4441-985e-3b2a94d00a9e), [instrucción](statement-element-xmla.md), [suscribirse](subscribe-element-xmla.md), [Sincronizar](synchronize-element-xmla.md), [desbloquear](unlock-element-xmla.md), [actualización](update-element-xmla.md), [UpdateCells](drop-element-xmla.md)|  
  
## <a name="attributes"></a>Atributos  
  
|Attribute|Descripción|  
|---------------|-----------------|  
|ProcessAffectedObjects|(Atributo `Boolean` opcional) Indica si se procesarán todos los objetos que requieren reprocesamiento.<br /><br /> Si se establece en true, la instancia [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] procesa los objetos que requieren reprocesamiento como resultado de procesar un objeto incluido en el comando `Batch`.<br /><br /> Si se establece en `false`, la instancia [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] procesa solo los objetos incluidos en el comando `Batch`.|  
|Transacción|(Atributo `Boolean` opcional) Indica si el comando incluido en el comando `Batch` se trata como una transacción única o como transacciones individuales.<br /><br /> Si se establece en true, todos los comandos incluidos en el comando `Batch` se consideran una transacción única. Si se produce un error en el comando, los comandos ejecutados antes del comando que ha devuelto un error se revierten y el comando `Batch` se detiene sin ejecutar los comandos posteriores.<br /><br /> Si se establece en `false`, el comando `Batch` intenta ejecutar todos los comandos y confirma los resultados de cada comando que se completa correctamente.|  
  
## <a name="remarks"></a>Comentarios  
  
> [!WARNING]  
>  Command/Execute/Statement no se admite actualmente en una operación por lotes.  
  
 Para obtener más información acerca de cómo realizar operaciones por lotes en XMLA, vea [realizar operaciones por lotes &#40;XMLA&#41;](../../multidimensional-models-scripting-language-assl-xmla/performing-batch-operations-xmla.md).  
  
## <a name="see-also"></a>Vea también  
 [Comandos &#40;XMLA&#41;](xml-elements-commands.md)  
  
  
