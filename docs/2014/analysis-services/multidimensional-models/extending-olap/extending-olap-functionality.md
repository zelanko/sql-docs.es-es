---
title: Extender la funcionalidad OLAP | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 49a17ff3-94e9-4969-84fc-37d49e63933b
caps.latest.revision: 4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d55ef159195d42935db271c3b3a51860fd698ec9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37220265"
---
# <a name="extending-olap-functionality"></a>Extender la funcionalidad de OLAP
  Como programador, puede ampliar Analysis Services escribiendo ensamblados, extensiones personalizadas y procedimientos almacenados que proporcionen la funcionalidad que desea usar y cambiar la finalidad en aplicaciones de base de datos. Los ensamblados se usan para ampliar la funcionalidad de los modelos multidimensionales mediante la adición de nuevos procedimientos y funciones al lenguaje MDX o mediante el complemento de personalización.  
  
 Los procedimientos almacenados se pueden usar para llamar a rutinas externas, simplificando el desarrollo y la implementación de bases de datos de Analysis Services al permitir que el código común se desarrolle una vez y se almacene en una sola ubicación. Los procedimientos almacenados se pueden utilizar para agregar funcionalidades de negocio a las aplicaciones que no sean suministradas por la funcionalidad nativa de MDX.  
  
 Las personalizaciones son objetos personalizados que se agregan a un cubo para proporcionar un comportamiento que varía según el usuario. Las personalizaciones no son objetos permanentes del cubo, sino que la aplicación cliente las aplica dinámicamente durante la sesión del usuario. Los ejemplos incluyen el cambio de la moneda de un valor monetario en función de la persona que tiene acceso a los datos, proporcionando KPI individualizados o una lista de sugerencias de destino para los clientes habituales que compran en línea.  
  
## <a name="in-this-section"></a>En esta sección  
 [Extensión de OLAP mediante personalizaciones](extending-olap-through-personalizations.md)  
  
 [Extensiones de personalización de Analysis Services](analysis-services-personalization-extensions.md)  
  
 [Definición de procedimientos almacenados](../../multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  
