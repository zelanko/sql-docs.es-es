---
title: Documentar y crear scripts de una base de datos de Analysis Services | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- XML for Analysis, scripts
- XMLA, scripts
- scripts [Analysis Services], databases
- documenting databases
- databases [Analysis Services], documenting
- databases [Analysis Services], scripts
ms.assetid: 125044e2-8d36-4733-8743-8bb68ff9aa4e
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 97a922007c9205aee23624a0c17e9f36e2570e5d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36202619"
---
# <a name="document-and-script-an-analysis-services-database"></a>Documentar y crear scripts en una base de datos de Analysis Services
  Después de implementar una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , puede usar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para producir los metadatos de la base de datos o de un objeto contenido en la base de datos, como un script de XML for Analysis (XMLA). Puede producir este script en una nueva ventana del **Editor de consultas XMLA** , en un archivo o en el Portapapeles. Para obtener más información acerca de XMLA, vea [Analysis Services Scripting Language &#40;ASSL&#41; referencia](../scripting/analysis-services-scripting-language-assl-for-xmla.md).  
  
 El script XMLA generado utiliza los elementos del Lenguaje de scripting de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] (ASSL) para definir los objetos contenidos en el script. Si ha generado un script CREATE, el script XMLA resultante contiene un comando **Create** de XMLA y elementos ASSL que se pueden utilizar para crear toda la estructura de la base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] en una instancia. Si ha generado un script ALTER, el script XMLA resultante contiene un comando **Alter** de XMLA y elementos ASSL que se pueden utilizar para restaurar la estructura de una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] existente al estado de la base de datos en el momento en que se creó el script.  
  
 Puede utilizar el script XMLA generado a partir de una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] de muchas formas, entre las que se incluyen:  
  
-   Para mantener un script de copia de seguridad que le permita volver a crear todos los objetos y permisos de la base de datos.  
  
-   Para crear o actualizar código de programación para el desarrollo de una base de datos.  
  
-   Para crear un entorno de pruebas o de desarrollo a partir de un esquema existente.  
  
## <a name="see-also"></a>Vea también  
 [Modificar o eliminar una base de datos de Analysis Services](modify-or-delete-an-analysis-services-database.md)   
 [Elemento ALTER &#40;XMLA&#41;](../xmla/xml-elements-commands/alter-element-xmla.md)   
 [Crear el elemento &#40;XMLA&#41;](../xmla/xml-elements-commands/create-element-xmla.md)  
  
  