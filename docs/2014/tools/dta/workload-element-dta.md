---
title: Elemento de Workload (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- Workload element
ms.assetid: 68ffd473-6546-4015-98d0-3763165de65c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1bc86764dce10dfad5c25ca7a1bd7f3d2bc519c4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48087305"
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
|**Repetición**|Una obligatoria por cada `DTAInput` elemento.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elementos|  
|------------------|--------------|  
|**Elemento primario**|[Iniciar y utilizar el Asistente para la optimización de motor de base de datos](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)|  
|**Elementos secundarios**|[Elemento file &#40;DTA&#41;](file-element-dta.md)<br /><br /> [Elemento de la base de datos para la carga de trabajo &#40;DTA&#41;](database-element-for-workload-dta.md)<br /><br /> [Elemento EventString &#40;DTA&#41;](eventstring-element-dta.md)|  
  
## <a name="remarks"></a>Comentarios  
 Una carga de trabajo es un conjunto de instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] que se ejecuta en una o varias bases de datos que se desean optimizar. El Asistente para la optimización de motor de base de datos puede utilizar scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] , archivos de seguimiento y tablas de seguimiento como cargas de trabajo.  
  
 Si se especifica una carga de trabajo en un archivo de entrada XML y una carga de trabajo en la línea de comandos mediante la herramienta **dta** , la carga de trabajo especificada en la línea de comandos se utilizará para la optimización. Todas las opciones de optimización especificadas en la línea de comandos tienen preferencia sobre las especificadas en un archivo de entrada XML. La única excepción se produce cuando se usa una configuración especificada por el usuario en el modo de evaluación del archivo de entrada XML. Por ejemplo, si se especifica una configuración en el `Configuration` elemento del archivo de entrada XML y el `EvaluateConfiguration` elemento también se especifica como una de las opciones de optimización, las opciones de optimización especificadas en el archivo de entrada XML invalidará las opciones de optimización especificadas en la línea de comandos.  
  
 Es necesario especificar una carga de trabajo para cada sesión de optimización.  
  
## <a name="example"></a>Ejemplo  
 El ejemplo de código siguiente especifica el **MyDatabase.MyDBOwner.TuningTable001** tabla de seguimiento para el `Workload` elemento. **TuningTable001** se creó utilizando la plantilla Optimización con SQL Server Profiler y guardando el seguimiento generada como una tabla.  
  
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
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
