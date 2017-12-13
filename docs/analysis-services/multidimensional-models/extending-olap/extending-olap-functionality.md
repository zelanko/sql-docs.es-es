---
title: Ampliar la funcionalidad de OLAP | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: 49a17ff3-94e9-4969-84fc-37d49e63933b
caps.latest.revision: "5"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 5a502afc3be82d238dc20077c526a9f94ac47689
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="extending-olap-functionality"></a>Extender la funcionalidad de OLAP
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]Como programador, puede ampliar Analysis Services escribiendo ensamblados, extensiones personalizadas y procedimientos almacenados que proporcionan la funcionalidad que desea utilizar y cambiar la finalidad de varias aplicaciones de base de datos. Los ensamblados se usan para ampliar la funcionalidad de los modelos multidimensionales mediante la adición de nuevos procedimientos y funciones al lenguaje MDX o mediante el complemento de personalización.  
  
 Los procedimientos almacenados se pueden usar para llamar a rutinas externas, simplificando el desarrollo y la implementación de bases de datos de Analysis Services al permitir que el código común se desarrolle una vez y se almacene en una sola ubicación. Los procedimientos almacenados se pueden utilizar para agregar funcionalidades de negocio a las aplicaciones que no sean suministradas por la funcionalidad nativa de MDX.  
  
 Las personalizaciones son objetos personalizados que se agregan a un cubo para proporcionar un comportamiento que varía según el usuario. Las personalizaciones no son objetos permanentes del cubo, sino que la aplicación cliente las aplica dinámicamente durante la sesión del usuario. Los ejemplos incluyen el cambio de la moneda de un valor monetario en función de la persona que tiene acceso a los datos, proporcionando KPI individualizados o una lista de sugerencias de destino para los clientes habituales que compran en línea.  
  
## <a name="in-this-section"></a>En esta sección  
 [Extensión de OLAP mediante personalizaciones](../../../analysis-services/multidimensional-models/extending-olap/extending-olap-through-personalizations.md)  
  
 [Extensiones de personalización de Analysis Services](../../../analysis-services/multidimensional-models/extending-olap/analysis-services-personalization-extensions.md)  
  
 [Definición de procedimientos almacenados](../../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  
