---
title: Conceder permisos Leer definición en metadatos de objeto (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- metadata [Analysis Services]
- permissions [Analysis Services], read metadata
- read metadata permissions
ms.assetid: c857e48e-64b0-4ffe-900d-a0a3ddafcefb
author: minewiskan
ms.author: owend
ms.openlocfilehash: 92edbbb45438622566b240d6c600428dff61ac96
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84546627"
---
# <a name="grant-read-definition-permissions-on-object-metadata-analysis-services"></a>Otorgar permisos Leer definición en metatados de objetos (Analysis Services)
  Los permisos para leer una definición de objeto o sus metadatos en objetos seleccionados permiten a los administradores otorgar permisos para ver información sobre los objetos sin necesidad de otorgar permisos para modificar la definición del objeto, modificar la estructura del objeto o ver los propios datos del objeto. `Read Definition`los permisos se pueden conceder en los niveles de base de datos, origen de datos, dimensión, estructura de minería de datos y modelo de minería de datos. Si necesita `Read Definition` permisos para un cubo, debe habilitar `Read Definition` para la base de datos. Recuerde que los permisos son aditivos. Por ejemplo, un rol otorga permisos para leer los metadatos de un cubo, mientras que otro rol otorga al mismo usuario permisos para leer los metadatos de una dimensión. Los permisos de los dos roles diferentes se combinan para conceder al usuario permiso para leer tanto los metadatos para el cubo como los metadatos para la dimensión dentro de la base de datos.  
  
> [!NOTE]  
>  El permiso para leer los metadatos de una base de datos es el mínimo necesario para conectar con una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] mediante [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] o [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Un usuario que tenga permiso para leer los metadatos también puede usar el conjunto de filas del esquema DISCOVER_XML_METADATA para hacer consultas en el objeto y ver sus metadatos. Para obtener más información, vea [Conjunto de filas DISCOVER_XML_METADATA](https://docs.microsoft.com/bi-reference/schema-rowsets/xml/discover-xml-metadata-rowset).  
  
## <a name="set-read-definition-permissions-on-a-database"></a>Establecer permisos de Leer definición en una base de datos  
 Al otorgar un permiso para leer los metadatos de una base de datos, también se otorga permiso para leer los metadatos de todos los objetos de la base de datos.  
  
 Le recomendamos que incluya el `Read Definition` permiso en el nivel de base de datos cada vez que configure roles para el procesamiento dedicado. Tener `Read Definition` permite a los usuarios que no son administradores ver la jerarquía de objetos de un modelo en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y navegar a objetos individuales para su posterior procesamiento.  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] , conéctese a la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , expanda **roles** para la base de datos adecuada en explorador de objetos y, a continuación, haga clic en un rol de base de datos (o cree un nuevo rol de base de datos).  
  
2.  En la pestaña **General** , seleccione la `Read Definition` opción.  
  
3.  En el panel **Pertenencia** , especifique las cuentas de usuario y grupo de Windows que se conectan a Analysis Services con este rol.  
  
4.  Haga clic en **Aceptar** para completar la creación del rol.  
  
## <a name="set-read-definition-permissions-on-individual-objects"></a>Establecer permisos de Leer definición en objetos individuales  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conéctese a la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], abra la carpeta **Bases de datos** , seleccione una base de datos, expanda **Roles** para la base de datos correspondiente en el Explorador de objetos y, después, haga clic en un rol de base de datos (o cree un rol de base de datos).  
  
2.  En el panel **General** , desactive el permiso de base de datos para `Read Definition` . Mediante este paso se quita la funcionalidad de heredar permisos para que pueda establecer permisos en objetos individuales.  
  
3.  Seleccione el objeto para el que está especificando `Read Definition` las propiedades:  
  
    -   En el panel **orígenes de datos** , haga clic en la `Read Definition` casilla correspondiente a ese origen de datos. Los miembros del rol podrán ver la cadena de conexión al origen de datos, incluso el nombre del servidor y probablemente el nombre de usuario. Este permiso se encuentra disponible en caso de que quiera proporcionar información sobre la cadena de conexión, sin necesidad, por otra parte, de otorgar permisos para modificar la cadena de conexión o ver las definiciones de alguno de los objetos.  
  
    -   En el panel **dimensiones** , haga clic en la `Read Definition` casilla correspondiente a esa dimensión. Es posible que nos analistas y desarrolladores con experiencia necesiten ver la definición sin permiso para modificarla o ver las definiciones de otros objetos (como otras dimensiones, objetos de cubo o estructuras y modelos de minería de datos).  
  
    -   En el panel estructuras de minería de datos, active la `Read Definition` casilla para estructuras o modelos de minería de datos. `Read Definition`se requiere para examinar el modelo de datos. Para obtener más información, vea [Otorgar permisos para estructuras y modelos de minería de datos &#40;Analysis Services&#41;](grant-permissions-on-data-mining-structures-and-models-analysis-services.md).  
  
4.  En el panel **Pertenencia** , especifique las cuentas de usuario y grupo de Windows que se conectan a Analysis Services con este rol.  
  
5.  Haga clic en **Aceptar** para completar la creación del rol.  
  
## <a name="see-also"></a>Consulte también  
 [Conceder permisos de base de datos &#40;Analysis Services&#41;](grant-database-permissions-analysis-services.md)   
 [Otorgar permisos de procesamiento &#40;Analysis Services&#41;](grant-process-permissions-analysis-services.md)  
  
  
