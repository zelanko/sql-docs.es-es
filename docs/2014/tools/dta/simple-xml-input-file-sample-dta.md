---
title: Ejemplo de archivo (DTA) de entrada XML simple | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- sample applications [DTA]
ms.assetid: 5b00e4eb-1742-43ec-98d8-d84216b6b840
caps.latest.revision: 21
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 77aac926ba5963fbef68a1b5db83687ddf5f77c7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37321385"
---
# <a name="simple-xml-input-file-sample-dta"></a>Ejemplo de archivo de entrada XML simple (DTA)
  Copie y pegue este ejemplo de archivo de entrada XML simple que se utiliza para optimizar las cargas de trabajo en un editor XML o editor de texto. A continuación, sustituya los valores especificados en los elementos **Server**, **Database**, **Schema**, **Table**, **Workload**y **TuningOptions** por los de la sesión de optimización concreta. Para obtener más información sobre los atributos y elementos secundarios que se pueden usar con estos elementos, vea [XML Input File Reference &#40;Database Engine Tuning Advisor&#41;](xml-input-file-reference-database-engine-tuning-advisor.md). En el siguiente ejemplo, se utiliza únicamente un subconjunto de opciones de atributos y elementos secundarios disponibles.  
  
## <a name="code"></a>código  
 [!code-xml[InputFileSamples#SimpleXMLInputFile](../../snippets/xml/SQL14/dta_xml/inputfilesamples/xml/dta_xml_input_file_samples.xml#simplexmlinputfile)]  
  
## <a name="see-also"></a>Vea también  
 [Iniciar y utilizar el Asistente para la optimización de motor de base de datos](../../relational-databases/performance/start-and-use-the-database-engine-tuning-advisor.md)   
 [Referencia del archivo de entrada XML &#40;Asistente para la optimización de motor de base de datos&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
