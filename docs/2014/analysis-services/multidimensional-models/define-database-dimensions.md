---
title: Definir dimensiones de base de datos | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- dimensions [Analysis Services], defining
ms.assetid: fe84588b-66a3-4100-a1cf-59b21b7adf01
caps.latest.revision: 26
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: dad1c138202c64a4768f944c9308edd0144602d0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36104816"
---
# <a name="define-database-dimensions"></a>Definir dimensiones de base de datos
  Utilice el Diseñador de dimensiones de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] para configurar una dimensión de base de datos existente en un proyecto o base de datos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Puede usar el Diseñador de dimensiones para realizar lo siguiente:  
  
-   Configurar las propiedades de dimensión-nivel.  
  
-   Agregar y configurar atributos de dimensión.  
  
-   Definir y configurar jerarquías definidas por el usuario.  
  
-   Definir y configurar relaciones entre los atributos.  
  
-   Definir las traducciones de las dimensiones.  
  
-   En dimensiones procesadas, puede examinar la estructura de la dimensión y ver sus datos.  
  
 Después de modificar una dimensión, un atributo o una jerarquía, debe procesar la dimensión para ver los cambios. Al trabajar en modo de proyecto, el usuario implementa los cambios en la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] antes del procesamiento.  
  
 Para más información sobre cómo abrir una dimensión en el Diseñador de dimensiones, vea [Modificar o eliminar una dimensión de base de datos en el Explorador de soluciones](database-dimensions-modify-or-delete-a-database-dimension-in-solution-explorer.md).  
  
 El Diseñador de dimensiones tiene tres pestañas, que se describen en la siguiente tabla.  
  
|Pestaña|Descripción|  
|---------|-----------------|  
|**Estructura de dimensión**|Utilice esta pestaña para trabajar con la estructura de una dimensión: para examinar o crear el esquema de vista del origen de datos para una dimensión, trabajar con atributos y organizar atributos en jerarquías definidas por el usuario.|  
|**Relaciones de atributo**|Utilice esta pestaña para crear, modificar o eliminar las relaciones de atributo de una dimensión.|  
|**Traducciones**|Utilice esta pestaña para agregar y modificar traducciones de metadatos de dimensiones en distintos idiomas.|  
|**Browser**|Utilice esta pestaña para examinar los miembros de una dimensión procesada y revisar las traducciones de metadatos de dimensiones.|  
  
 En los siguientes temas se describen las tareas que puede realizar en el Diseñador de dimensiones.  
  
 [Referencia de las propiedades de los atributos de dimensión](dimension-attribute-properties-reference.md)  
 Describe cómo definir y configurar un atributo de dimensión.  
  
 [Crear jerarquías definidas por el usuario](user-defined-hierarchies-create.md)  
 Describe cómo definir y configurar una jerarquía definida por el usuario.  
  
 [Definir relaciones de atributo](attribute-relationships-define.md)  
 Describe cómo definir y configurar una relación de atributo.  
  
 [Usar al Asistente de Business Intelligence para mejorar dimensiones](../use-the-business-intelligence-wizard-to-enhance-dimensions.md)  
 Describe cómo mejorar una dimensión con el Asistente de Business Intelligence.  
  
  