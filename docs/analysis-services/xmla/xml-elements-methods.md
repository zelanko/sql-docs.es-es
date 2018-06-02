---
title: Métodos (XMLA) | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 15f930695e13d824e70da748dad20cf574e9bc38
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/02/2018
ms.locfileid: "34579147"
---
# <a name="xml-elements---methods"></a>Elementos XML: métodos
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  El protocolo XML for Analysis (XMLA) utiliza dos métodos, **Discover** y **Execute**, para proporcionar una manera estándar para las aplicaciones tener acceso a información en una instancia de Analysis Services. Dado que estos métodos se invocan utilizando el Protocolo simple de acceso a objetos (SOAP), aceptan la entrada y entregan el resultado en XML. Analysis Services implementa ambos métodos, conforme a la especificación de XML for Analysis 1.1.  
  
## <a name="in-this-section"></a>En esta sección  
 Los temas siguientes describen los métodos XMLA implementados por Analysis Services.  
  
|Método|Descripción|  
|------------|-----------------|  
|[Método Discover &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-methods-discover.md)|Recupera información, como la lista de bases de datos disponibles o los detalles sobre un objeto concreto, de una instancia de Analysis Services. Los datos recuperados con el método **Discover** dependen de los valores de los parámetros que se le pasan.|  
|[Ejecutar el método &#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-methods-execute.md)|Envía comandos XMLA a una instancia de Analysis Services. Están incluidas las solicitudes que conllevan transferencia de datos, como recuperar o actualizar los datos del servidor.|  
  
## <a name="see-also"></a>Vea también
 [Elementos XML &#40;XMLA&#41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)   
 [Tipos de datos XML &#40;XMLA&#41;](../../analysis-services/xmla/xml-data-types/xml-data-types-xmla.md)   
 [Elementos XML &#40;XMLA&#41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)  
  
  
