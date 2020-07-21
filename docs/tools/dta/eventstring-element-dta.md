---
title: EventString (DTA, elemento)
description: En la utilidad DTA, el elemento EventString especifica una carga de trabajo de script de Transact-SQL directamente en el archivo de entrada XML.
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- EventString element
ms.assetid: f76c37b4-2f6e-4274-8ee2-87e89d98e8a2
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: f9944a2e9d9dc1ec8aad069aa74b90a6a420fad4
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82826530"
---
# <a name="eventstring-element-dta"></a>EventString (DTA, elemento)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Especifica una carga de trabajo de scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] directamente en el archivo de entrada XML.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<Workload>  
    <EventString Weight="...">  
    ...code removed here...  
    </EventString>  
</Workload>  
```  
  
## <a name="element-attributes"></a>Atributos del elemento  
  
|Atributo|Descripción|  
|---------------|-----------------|  
|**Peso**|Opcional. Especifica el factor de peso de la consulta (un factor de importancia) del evento especificado. Utilice un tipo de datos **float** para especificar el peso. Por ejemplo, **Weight**="100.01". El valor mínimo que se puede especificar para **Weight** es "0".|  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|**Tipo y longitud de los datos**|**string**, longitud ilimitada.|  
|**Valor predeterminado**|Ninguno.|  
|**Repetición**|Una obligatoria si no se especifica ningún otro tipo de carga de trabajo. Es necesario especificar un elemento secundario **EventString**, **File**o **Database** para el elemento primario **Workload** , aunque solo se puede utilizar un tipo. Por ejemplo, si se especifica una carga de trabajo con el elemento **EventString** , no se puede especificar una carga de trabajo con el elemento **File** en el mismo archivo de entrada XML.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[Workload &#40;DTA, elemento&#41;](../../tools/dta/workload-element-dta.md)|  
|**Elementos secundarios**|Ninguno.|  
  
## <a name="example"></a>Ejemplo  
 Para obtener un ejemplo de uso de este elemento, vea [Ejemplo de archivo de entrada XML con carga de trabajo insertada &#40;DTA&#41;](../../tools/dta/xml-input-file-sample-with-inline-workload-dta.md).  
  
## <a name="see-also"></a>Consulte también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
