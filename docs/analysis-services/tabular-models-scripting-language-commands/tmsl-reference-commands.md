---
title: Comandos de Tabular modelo Scripting Language (TMSL) | Documentos de Microsoft
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tmsl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4fad4984a251167a5e0a36d26911fd969ea3ddea
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="tmsl-reference---commands"></a>Referencia TMSL - comandos
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Puede ejecutar comandos en un punto de conexión XMLA, formular definiciones de objetos JSON mediante la Tabular Model Scripting Language (TMSL), en bases de datos de modelo Tabular.   Vea [definiciones de objetos Tabular Model Scripting Language &#40;TMSL&#41; ](../../analysis-services/tabular-models-scripting-language-objects/tmsl-reference-tabular-objects.md) para obtener una lista de objetos que se usan con los siguientes comandos.  
  
## <a name="object-operations"></a>Operaciones de objeto  
  
|||  
|-|-|  
|[ALTER, comando &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/alter-command-tmsl.md)|Modificar en línea a un objeto sin tener que especificar la definición completa.|  
|[Crear un comando &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/create-command-tmsl.md)|Crea un nuevo objeto, incluidos a sus descendientes.|  
|[El comando CreateOrReplace &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl.md)|Crear o reemplazar las partes de una definición de objeto. Se debe proporcionar la definición completa.|  
|[Comando Delete &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/delete-command-tmsl.md)|Eliminar un objeto, incluidos a sus descendientes.|  
  
## <a name="data-refresh-operations"></a>Operaciones de actualización de datos  
  
|||  
|-|-|  
|[El comando MergePartitions &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/mergepartitions-command-tmsl.md)|Combinar una partición de destino en un origen y elimine el destino.|  
|[Comando Refresh &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/refresh-command-tmsl.md)|Procesar una base de datos, tabla o partición.|  
  
## <a name="scripting"></a>Scripting  
  
|||  
|-|-|  
|[Secuencia de comandos &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/sequence-command-tmsl.md)|Procesar por lotes las operaciones de forma secuencial o en paralelo|  
  
## <a name="database-management-operations"></a>Operaciones de administración de base de datos  
  
|||  
|-|-|  
|[El comando Attach &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/attach-command-tmsl.md)|Agrega un archivo al servidor.|  
|[Detach, comando &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/detach-command-tmsl.md)|Quita un archivo de los servidores.|  
|[Comando de copia de seguridad &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/backup-command-tmsl.md)|Crea un archivo de copia de seguridad de una base de datos.|  
|[Comando restore &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/restore-command-tmsl.md)|Restaura la base de datos en el servidor.|  
|[Synchronize, comando &#40;TMSL&#41;](../../analysis-services/tabular-models-scripting-language-commands/synchronize-command-tmsl.md)|Sincroniza una base de datos de Analysis Services con otra base de datos existente.|  
  
## <a name="see-also"></a>Vea también  
 [Tabular Model Scripting Language &#40;TMSL&#41; Reference (Referencia de Tabular Model Scripting Language [TMSL])](../../analysis-services/tabular-model-scripting-language-tmsl-reference.md)   
 [Instalar proveedores de datos de Analysis Services &#40;AMO, ADOMD.NET, MSOLAP&#41;](../../analysis-services/instances/install-windows/install-analysis-services-data-providers-amo-adomd-net-msolap.md)   
 [Nivel de compatibilidad para modelos tabulares de Analysis Services](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)  
  
  
