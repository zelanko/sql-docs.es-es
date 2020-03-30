---
title: Workload (DTA, elemento)
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Workload element
ms.assetid: 68ffd473-6546-4015-98d0-3763165de65c
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: 22331332715639b12f7a2cc82d8b71d723a1fecd
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "75307894"
---
# <a name="workload-element-dta"></a>Workload (DTA, elemento)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Especifica la carga de trabajo que se va a utilizar durante una sesión de optimización.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
<DTAInput>  
    <Server>  
...code removed...  
    <Workload>...</Workload>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|**Tipo y longitud de los datos**|Ninguno.|  
|**Valor predeterminado**|Ninguno.|  
|**Repetición**|Una obligatoria por cada elemento **DTAInput** .|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[Iniciar y utilizar el Asistente para la optimización de motor de base de datos](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)|  
|**Elementos secundarios**|[File &#40;DTA, elemento&#41;](../../tools/dta/file-element-dta.md)<br /><br /> [Database &#40;DTA, elemento de Workload&#41;](../../tools/dta/database-element-for-workload-dta.md)<br /><br /> [EventString &#40;DTA, elemento&#41;](../../tools/dta/eventstring-element-dta.md)|  
  
## <a name="remarks"></a>Observaciones  
 Una carga de trabajo es un conjunto de instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] que se ejecuta en una o varias bases de datos que se desean optimizar. El Asistente para la optimización de motor de base de datos puede utilizar scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] , archivos de seguimiento y tablas de seguimiento como cargas de trabajo.  
  
 Si se especifica una carga de trabajo en un archivo de entrada XML y una carga de trabajo en la línea de comandos mediante la herramienta **dta** , la carga de trabajo especificada en la línea de comandos se utilizará para la optimización. Todas las opciones de optimización especificadas en la línea de comandos tienen preferencia sobre las especificadas en un archivo de entrada XML. La única excepción se produce cuando se usa una configuración especificada por el usuario en el modo de evaluación del archivo de entrada XML. Por ejemplo, si se especifica una configuración en el elemento **Configuration** del archivo de entrada XML y el elemento **EvaluateConfiguration** también se ha especificado como una de las opciones de optimización, las opciones de optimización especificadas en el archivo de entrada XML tendrán preferencia sobre aquellas especificadas en la línea de comandos.  
  
 Es necesario especificar una carga de trabajo para cada sesión de optimización.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo de código siguiente especifica la tabla de seguimiento **de MyDatabase.MyDBOwner.TuningTable001** para el elemento **Workload** . **TuningTable001** se creó utilizando la plantilla Optimización con SQL Server Profiler y guardando el seguimiento generada como una tabla.  
  
```  
<DTAXML ...>  
  <DTAInput>  
    <Server>  
...code removed here...  
    </Server>  
    <Workload>  
      <Database>  
        <Name>MyDatabase</Name>  
        <Schema>  
          <Name>MyDBOwner</Name>  
            <Table>  
              <Name>TuningTable001</Name>  
            </Table>  
        </Schema>  
      </Database>  
    </Workload>  
...code removed here...  
  </DTAInput>  
</DTAXML>  
```  
  
## <a name="see-also"></a>Consulte también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
