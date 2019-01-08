---
title: Ejemplo de archivo de entrada XML con configuración especificada por el usuario (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- sample applications [DTA]
ms.assetid: b29c9716-e5c3-4003-9efb-3ade2197b630
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4fefcec96100a9848810bc37a7b02760a3005cc3
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52781855"
---
# <a name="xml-input-file-sample-with-user-specified-configuration-dta"></a>Ejemplo de archivo de entrada XML con configuración especificada por el usuario (DTA)
  Copie y pegue este ejemplo de archivo de entrada XML que especifica una configuración especificada por el usuario con el elemento **Configuration** en un editor XML o editor de texto. Esto le permitirá realizar análisis de escenarios condicionales. Los análisis de escenarios condicionales implican el uso del elemento **Configuration** para especificar un conjunto de estructuras de diseño físico hipotéticas para la base de datos que se quiere optimizar. A continuación se utiliza el Asistente para la optimización de motor de base de datos para analizar los efectos de la ejecución de una carga de trabajo en esta configuración hipotética con el objetivo de descubrir si mejora el rendimiento a la hora de procesar las consultas. Este tipo de análisis tiene la ventaja de evaluar la nueva configuración sin incurrir en la sobrecarga que supone implementarla realmente. Si la configuración hipotética no proporciona las mejoras de rendimiento que desea, es fácil modificarla y volver a analizarla hasta conseguir la configuración que produzca los resultados necesarios.  
  
 Una vez copiado el ejemplo en la herramienta de edición, sustituya los valores especificados en los elementos **Server**, **Database**, **Schema**, **Table**, **Workload**, **TuningOptions**y **Configuration** por los de la sesión de optimización concreta. Para obtener más información sobre todos los atributos y elementos secundarios que se pueden usar con estos elementos, vea [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](xml-input-file-reference-database-engine-tuning-advisor.md). En el siguiente ejemplo, se utiliza únicamente un subconjunto de opciones de atributos y elementos secundarios disponibles.  
  
## <a name="code"></a>Código  
 [!code-xml[InputFileSamples#UserSpecifiedConfigInputFile](../../snippets/xml/SQL14/dta_xml/inputfilesamples/xml/dta_xml_input_file_samples.xml#userspecifiedconfiginputfile)]  
  
## <a name="comments"></a>Comentarios  
  
-   Cuando se especifica el modo **Absolute** para el elemento **Configuration** (`Configuration SpecificationMode="Absolute"`), no se permite quitar las estructuras de diseño físico.  
  
-   No es posible crear y quitar la misma estructura de diseño físico en ningún modo (**Relative** o **Absolute**) del elemento **Configuration** .  
  
## <a name="see-also"></a>Vea también  
 [Iniciar y utilizar el Asistente para la optimización de motor de base de datos](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)   
 [Ver y trabajar con la salida del Asistente para la optimización de motor de base de datos](../../relational-databases/performance/view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md)   
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
