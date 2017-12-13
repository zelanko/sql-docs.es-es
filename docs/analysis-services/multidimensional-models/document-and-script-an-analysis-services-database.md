---
title: Documentar y crear scripts de una base de datos de Analysis Services | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- XML for Analysis, scripts
- XMLA, scripts
- scripts [Analysis Services], databases
- documenting databases
- databases [Analysis Services], documenting
- databases [Analysis Services], scripts
ms.assetid: 125044e2-8d36-4733-8743-8bb68ff9aa4e
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: ceb4145368b88ecc523dc7c5a3b96406bb383c4a
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="document-and-script-an-analysis-services-database"></a>Documentar y crear scripts en una base de datos de Analysis Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Después de un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] se implementa la base de datos, puede usar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para producir los metadatos de la base de datos o de un objeto contenido en la base de datos, como un documento de XML for Analysis (XMLA) script. Puede producir este script en una nueva ventana del **Editor de consultas XMLA** , en un archivo o en el Portapapeles. Para más información sobre XMLA, vea [Referencia de Analysis Services Scripting Language &#40;ASSL&#41;](../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md).  
  
 El script XMLA generado utiliza los elementos del Lenguaje de scripting de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] (ASSL) para definir los objetos contenidos en el script. Si ha generado un script CREATE, el script XMLA resultante contiene un comando **Create** de XMLA y elementos ASSL que se pueden utilizar para crear toda la estructura de la base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en una instancia. Si ha generado un script ALTER, el script XMLA resultante contiene un comando **Alter** de XMLA y elementos ASSL que se pueden utilizar para restaurar la estructura de una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] existente al estado de la base de datos en el momento en que se creó el script.  
  
 Puede utilizar el script XMLA generado a partir de una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de muchas formas, entre las que se incluyen:  
  
-   Para mantener un script de copia de seguridad que le permita volver a crear todos los objetos y permisos de la base de datos.  
  
-   Para crear o actualizar código de programación para el desarrollo de una base de datos.  
  
-   Para crear un entorno de pruebas o de desarrollo a partir de un esquema existente.  
  
## <a name="see-also"></a>Vea también  
 [Modificar o eliminar una base de datos de Analysis Services](../../analysis-services/multidimensional-models/modify-or-delete-an-analysis-services-database.md)   
 [Modificar elemento &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md)   
 [Crear elemento &#40; XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)  
  
  
