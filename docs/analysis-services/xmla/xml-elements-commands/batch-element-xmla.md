---
title: Procesar por lotes elemento (XMLA) | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4644b8775212eae0cb6d912df9bc415c5fc96ec7
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34573947"
---
# <a name="batch-element-xmla"></a>Elemento Batch (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Realiza XML de uno o más para los comandos de Analysis (XMLA) como una operación por lotes, ya sea de forma secuencial o en paralelo, en una instancia de Analysis Services.  
  
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
|Elementos primarios|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|Elementos secundarios|[Enlaces](../../../analysis-services/xmla/xml-elements-properties/bindings-element-xmla.md), [DataSource](../../../analysis-services/xmla/xml-elements-properties/datasource-element-xmla.md), [DataSourceView](../../../analysis-services/xmla/xml-elements-properties/datasourceview-element-xmla.md), [ErrorConfiguration](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md), [paralelas](../../../analysis-services/xmla/xml-elements-properties/parallel-element-xmla.md)<br /><br /> Uno o varios de los siguientes comandos XMLA: [Alter](../../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md), [copia de seguridad](../../../analysis-services/xmla/xml-elements-commands/backup-element-xmla.md), [BeginTransaction](../../../analysis-services/xmla/xml-elements-commands/begintransaction-element-xmla.md), [ClearCache](../../../analysis-services/xmla/xml-elements-commands/clearcache-element-xmla.md), [ CommitTransaction](../../../analysis-services/xmla/xml-elements-commands/committransaction-element-xmla.md), [crear](../../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md), [eliminar](../../../analysis-services/xmla/xml-elements-commands/delete-element-xmla.md), [DesignAggregations](../../../analysis-services/xmla/xml-elements-commands/designaggregations-element-xmla.md), [Drop](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md), [Insertar](../../../analysis-services/xmla/xml-elements-commands/insert-element-xmla.md), [bloqueo](../../../analysis-services/xmla/xml-elements-commands/lock-element-xmla.md), [MergePartitions](../../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md), [NotifyTableChange](../../../analysis-services/xmla/xml-elements-commands/notifytablechange-element-xmla.md), [proceso](../../../analysis-services/xmla/xml-elements-commands/process-element-xmla.md), [Restaurar](../../../analysis-services/xmla/xml-elements-commands/restore-element-xmla.md), [RollbackTransaction](../../../analysis-services/xmla/xml-elements-commands/rollbacktransaction-element-xmla.md), [SetPasswordEncryptionKey](http://msdn.microsoft.com/en-us/fb262737-f0f4-4441-985e-3b2a94d00a9e), [instrucción](../../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md), [suscribirse](../../../analysis-services/xmla/xml-elements-commands/subscribe-element-xmla.md), [Sincronizar](../../../analysis-services/xmla/xml-elements-commands/synchronize-element-xmla.md), [desbloquear](../../../analysis-services/xmla/xml-elements-commands/unlock-element-xmla.md), [actualización](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md), [UpdateCells](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)|  
  
## <a name="attributes"></a>Atributos  
  
|Attribute|Descripción|  
|---------------|-----------------|  
|ProcessAffectedObjects|(Opcional **booleano** atributo) indica si se procesarán todos los objetos que requieren volver a procesar.<br /><br /> Si establece en true, el [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia procesa los objetos que requieren reprocesamiento como resultado del procesamiento de un objeto incluido en la **lote** comando.<br /><br /> Si establece en **false**, el [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia procesa solo los objetos incluidos en el **lote** comando.|  
|Transaction|(Opcional **booleano** atributo) indica si el comando se incluye en el **lote** comando se tratan como una única transacción o transacciones individuales.<br /><br /> Si establece en true, todos los comandos incluidos en el **lote** comando se considera una sola transacción. Si cualquiera de los comandos se produce un error, los comandos ejecutados antes del comando con errores se revierten y el **lote** comando detiene sin ejecutar los comandos siguientes.<br /><br /> Si establece en **false**, **lote** comando intenta ejecutar todos los comandos y confirma los resultados de cada comando que se completa correctamente.|  
  
## <a name="remarks"></a>Notas  
  
> [!WARNING]  
>  Command/Execute/Statement no se admite actualmente en una operación por lotes.  
  
 Para obtener más información acerca de cómo realizar operaciones por lotes en XMLA, vea [realizar operaciones por lotes &#40;XMLA&#41;](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/performing-batch-operations-xmla.md).  
  
## <a name="see-also"></a>Vea también
 [Comandos &#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
