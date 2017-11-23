---
title: Workload, elemento (DTA) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: XML
helpviewer_keywords: Workload element
ms.assetid: 68ffd473-6546-4015-98d0-3763165de65c
caps.latest.revision: "16"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 5a2ff19d6a4044a6a3e29cb59592cdd7dd653e79
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="workload-element-dta"></a>Workload (DTA, elemento)
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
  
## <a name="remarks"></a>Comentarios  
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
  
## <a name="see-also"></a>Vea también  
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
