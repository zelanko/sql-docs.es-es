---
title: Ejemplo de archivo con la carga de trabajo insertada (DTA) de entrada XML | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- XML
helpviewer_keywords:
- sample applications [DTA]
ms.assetid: 7c04fe1d-6669-44a1-8b73-36d469e9b002
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: f899682e95e50df8fec87e99507f3bb18308db71
ms.contentlocale: es-es
ms.lasthandoff: 10/24/2017

---
# <a name="xml-input-file-sample-with-inline-workload-dta"></a>Ejemplo de archivo de entrada XML con carga de trabajo insertada (DTA)
  Copie y pegue este ejemplo de archivo de entrada XML que especifica una carga de trabajo con el elemento **EventString** en un editor XML o editor de texto. Puede utilizar el elemento **EventString** para especificar una carga de trabajo de scripts [!INCLUDE[tsql](../../includes/tsql-md.md)] en el archivo de entrada XML, en lugar de utilizar un archivo de carga de trabajo independiente. Una vez copiado el ejemplo en la herramienta de edición, sustituya los valores especificados en los elementos **Server**, **Database**, **Schema**, **Table**, **Workload**, **EventString**y **TuningOptions** por los de la sesión de optimización concreta. Para obtener más información sobre todos los atributos y elementos secundarios que se pueden usar con estos elementos, vea [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md). En el siguiente ejemplo, se utiliza únicamente un subconjunto de opciones de atributos y elementos secundarios disponibles.  
  
## <a name="code"></a>código  
 [!code-xml[InputFileSamples#InlineWorkloadInputFile](../../tools/dta/codesnippet/xml/xml-input-file-sample-wi_1.xml)]  
  
## <a name="comments"></a>Comentarios  
 `USE database_name` se pueden especificar en la carga de trabajo insertada incluida en el elemento **EventString** .  
  
## <a name="see-also"></a>Vea también  
 [Iniciar y utilizar el Asistente para la optimización de motor de base de datos](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)   
 [Ver y trabajar con la salida del Asistente para la optimización de motor de base de datos](../../relational-databases/performance/view-and-work-with-the-output-from-the-database-engine-tuning-advisor.md)   
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  

