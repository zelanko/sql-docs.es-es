---
title: Ampliar la funcionalidad de OLAP | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 06b73c0b9f8b4c2d93bb81762ebec442f94e7198
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="extending-olap-functionality"></a>Extender la funcionalidad de OLAP
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Como programador, puede ampliar Analysis Services escribiendo ensamblados, extensiones personalizadas y procedimientos almacenados que proporcionen la funcionalidad que desea usar y cambiar la finalidad en aplicaciones de base de datos. Los ensamblados se usan para ampliar la funcionalidad de los modelos multidimensionales mediante la adición de nuevos procedimientos y funciones al lenguaje MDX o mediante el complemento de personalización.  
  
 Los procedimientos almacenados se pueden usar para llamar a rutinas externas, simplificando el desarrollo y la implementación de bases de datos de Analysis Services al permitir que el código común se desarrolle una vez y se almacene en una sola ubicación. Los procedimientos almacenados se pueden utilizar para agregar funcionalidades de negocio a las aplicaciones que no sean suministradas por la funcionalidad nativa de MDX.  
  
 Las personalizaciones son objetos personalizados que se agregan a un cubo para proporcionar un comportamiento que varía según el usuario. Las personalizaciones no son objetos permanentes del cubo, sino que la aplicación cliente las aplica dinámicamente durante la sesión del usuario. Los ejemplos incluyen el cambio de la moneda de un valor monetario en función de la persona que tiene acceso a los datos, proporcionando KPI individualizados o una lista de sugerencias de destino para los clientes habituales que compran en línea.  
  
## <a name="in-this-section"></a>En esta sección  
 [Extender OLAP mediante personalizaciones](../../../analysis-services/multidimensional-models/extending-olap/extending-olap-through-personalizations.md)  
  
 [Las extensiones de personalización de Analysis Services](../../../analysis-services/multidimensional-models/extending-olap/analysis-services-personalization-extensions.md)  
  
 [Definir procedimientos almacenados](../../../analysis-services/multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  
