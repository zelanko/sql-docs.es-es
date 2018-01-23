---
title: Scripting Language (TMSL) referencia del modelo tabular | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: c700d7f8-7e01-4052-a9ad-8200dd4009f2
caps.latest.revision: "20"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: de637476cd0aa2577c850062dffebc0e4fc66238
ms.sourcegitcommit: 82c9868b5bf95e5b0c68137ba434ddd37fc61072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/22/2018
---
# <a name="tabular-model-scripting-language-tmsl-reference"></a>Scripting Language (TMSL) referencia del modelo tabular
[!INCLUDE[ssas-appliesto-sqlas-aas](../includes/ssas-appliesto-sqlas-aas.md)]

  Tabular Model Scripting Language (TMSL) se muestra la sintaxis de definición de modelo de comandos y objetos de bases de datos de modelo tabular de Analysis Services en el nivel de compatibilidad 1200 o superior. TMSL se comunica con Analysis Services a través del protocolo XMLA, donde el [XMLA. Ejecutar](../analysis-services/xmla/xml-elements-methods-execute.md) método acepta tanto basada en JSON **instrucción** scripts en TMSL, así como los scripts tradicionales basado en XML en [Analysis Services Scripting Language &#40; ASSL para XMLA &#41; ](../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md).  
  
 Elementos clave de TMSL incluyen lo siguiente:  
  
-   En función de la semántica de modelo tabular de metadatos tabulares. Un modelo tabular se compone de tablas, columnas y relaciones. Las definiciones de objeto equivalente en TMSL son ahora, obviamente, tablas, columnas, relaciones y así sucesivamente.  
  
     Un nuevo motor de metadatos es compatible con estas definiciones.  
  
-   Las definiciones de objeto se estructuran como JSON en lugar de XML.  
  
 Con la excepción de cómo se da formato a la carga (en formato JSON o XML), TMSL y ASSL son funcionalmente equivalentes en cómo proporcionan comandos y los metadatos a los métodos XMLA usados para la transferencia de comunicación y los datos del servidor.  
  
## <a name="how-to-use-tmsl"></a>Cómo usar TMSL  
 La manera más fácil de explorar scripting TMSL usa los comandos CREATE, ALTER, DELETE o proceso en SQL Server Management Studio (SSMS) en un modelo que ya conoce. Suponiendo que está usando un modelo existente, recuerde actualizar al nivel de compatibilidad 1200 o superior en primer lugar.  
  
1.  Busque el comando que desea usar: [comandos de Tabular Model Scripting Language &#40; TMSL &#41;](../analysis-services/tabular-models-scripting-language-commands/tmsl-reference-commands.md)  
  
2.  Comprobar la referencia de la definición de objeto para los objetos usados en el comando: [definiciones de objetos Tabular Model Scripting Language &#40; TMSL &#41;](../analysis-services/tabular-models-scripting-language-objects/tmsl-reference-tabular-objects.md)  
  
3.  Elija un método para el envío de un script de TMSL:  
  
    -   Ventana XMLA en Management Studio  
  
    -   **Invoke-ascmd** a través de PowerShell de AMO ([cmdlet Invoke-ASCmd](../analysis-services/powershell/invoke-ascmd-cmdlet.md))  
  
    -   [Analysis Services tarea ejecutan DDL de](../integration-services/control-flow/analysis-services-execute-ddl-task.md) en SSIS.  
  
## <a name="model-definition-schema"></a>Esquema de definición de modelo  
 Captura de pantalla siguiente muestra una versión abreviada del esquema, contraída para mostrar los objetos principales.  
  
 ![SSAS_TabularMetadata](../analysis-services/media/ssas-tabularmetadata.JPG "SSAS_TabularMetadata")  
  
## <a name="scripting-languages-in-analysis-services"></a>Lenguajes de scripting de Analysis Services  
 Analysis Services admite los lenguajes de scripting ASSL y TMSL. Solo los modelos tabulares creados en el nivel de compatibilidad de 1200 o superior se describen en TMS en formato JSON.  
  
 [Analysis Services Scripting Language &#40; ASSL para XMLA &#41; ](../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md) fue el primer lenguaje de scripting y sigue siendo el único lenguaje de scripting para modelos multidimensionales como tabulares en niveles de compatibilidad inferiores (1100 o 1103). En ASSL, los modelos tabulares en 110 x se describen en términos multidimensionales, como **cubo** (para un modelo) y **measuregroup** (para una tabla).  
  
> [!NOTE]  
>  En [SQL Server Data Tools (SSDT), puede actualizar un modelo tabular de versiones anterior para usar TMSL cambiando la su **CompatibilityLevel** a 1200 o superior. Recuerde que la actualización es irreversible. Antes de actualizar, realice una copia del modelo en caso de que necesite la versión original más adelante.  
  
 En la tabla siguiente es la matriz de lenguaje de scripting para los modelos de datos de Analysis Services en versiones diferentes en niveles de compatibilidad específico.  

||||||  
|-|-|-|-|-|  
|**Versión**|**Multidimensionales**|**Tabulares 110 x**|**Tabulares 1200.**| **1400 tabular** |
|Azure Analysis Services|N/D|N/D|TMSL|TMSL| 
|SQL Server 2017|ASSL|ASSL|TMSL|TMSL| 
|SQL Server 2016|ASSL|ASSL|TMSL|TMSL| 
|SQL Server 2014|ASSL|ASSL|N/D|N/D|   
|SQL Server 2012|ASSL|ASSL|N/D|N/D|  

  
## <a name="see-also"></a>Vea también  
 [Nivel de compatibilidad para los modelos tabulares de Analysis Services](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [Analysis Services Scripting Language &#40; ASSL para XMLA &#41;](../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md)   
 [Determinar el modo de servidor de una instancia de Analysis Services](../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
