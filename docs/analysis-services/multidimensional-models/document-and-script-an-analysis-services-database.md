---
title: Documentar y crear scripts de una base de datos de Analysis Services | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7862be07bd3b01db8dcc2a0beb115a883e4550e7
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34023112"
---
# <a name="document-and-script-an-analysis-services-database"></a>Documentar y crear scripts en una base de datos de Analysis Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Después de implementar una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , puede usar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para producir los metadatos de la base de datos o de un objeto contenido en la base de datos, como un script de XML for Analysis (XMLA). Puede producir este script en una nueva ventana del **Editor de consultas XMLA** , en un archivo o en el Portapapeles. Para más información sobre XMLA, vea [Referencia de Analysis Services Scripting Language &#40;ASSL&#41;](../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md).  
  
 El script XMLA generado utiliza los elementos del Lenguaje de scripting de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] (ASSL) para definir los objetos contenidos en el script. Si ha generado un script CREATE, el script XMLA resultante contiene un comando **Create** de XMLA y elementos ASSL que se pueden utilizar para crear toda la estructura de la base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en una instancia. Si ha generado un script ALTER, el script XMLA resultante contiene un comando **Alter** de XMLA y elementos ASSL que se pueden utilizar para restaurar la estructura de una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] existente al estado de la base de datos en el momento en que se creó el script.  
  
 Puede utilizar el script XMLA generado a partir de una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de muchas formas, entre las que se incluyen:  
  
-   Para mantener un script de copia de seguridad que le permita volver a crear todos los objetos y permisos de la base de datos.  
  
-   Para crear o actualizar código de programación para el desarrollo de una base de datos.  
  
-   Para crear un entorno de pruebas o de desarrollo a partir de un esquema existente.  
  
## <a name="see-also"></a>Vea también  
 [Modificar o eliminar una base de datos de Analysis Services](../../analysis-services/multidimensional-models/modify-or-delete-an-analysis-services-database.md)   
 [Elemento ALTER &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/alter-element-xmla.md)   
 [Crear el elemento &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-commands/create-element-xmla.md)  
  
  
