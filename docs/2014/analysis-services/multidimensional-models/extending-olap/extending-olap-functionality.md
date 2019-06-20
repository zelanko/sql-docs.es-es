---
title: Extender la funcionalidad OLAP | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
ms.assetid: 49a17ff3-94e9-4969-84fc-37d49e63933b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2d4d08795351b93615954ad64e004482745f768d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62725959"
---
# <a name="extending-olap-functionality"></a>Extender la funcionalidad de OLAP
  Como programador, puede ampliar Analysis Services escribiendo ensamblados, extensiones personalizadas y procedimientos almacenados que proporcionen la funcionalidad que desea usar y cambiar la finalidad en aplicaciones de base de datos. Los ensamblados se usan para ampliar la funcionalidad de los modelos multidimensionales mediante la adición de nuevos procedimientos y funciones al lenguaje MDX o mediante el complemento de personalización.  
  
 Los procedimientos almacenados se pueden usar para llamar a rutinas externas, simplificando el desarrollo y la implementación de bases de datos de Analysis Services al permitir que el código común se desarrolle una vez y se almacene en una sola ubicación. Los procedimientos almacenados se pueden utilizar para agregar funcionalidades de negocio a las aplicaciones que no sean suministradas por la funcionalidad nativa de MDX.  
  
 Las personalizaciones son objetos personalizados que se agregan a un cubo para proporcionar un comportamiento que varía según el usuario. Las personalizaciones no son objetos permanentes del cubo, sino que la aplicación cliente las aplica dinámicamente durante la sesión del usuario. Los ejemplos incluyen el cambio de la moneda de un valor monetario en función de la persona que tiene acceso a los datos, proporcionando KPI individualizados o una lista de sugerencias de destino para los clientes habituales que compran en línea.  
  
## <a name="in-this-section"></a>En esta sección  
 [Extensión de OLAP mediante personalizaciones](extending-olap-through-personalizations.md)  
  
 [Extensiones de personalización de Analysis Services](analysis-services-personalization-extensions.md)  
  
 [Definición de procedimientos almacenados](../../multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  
