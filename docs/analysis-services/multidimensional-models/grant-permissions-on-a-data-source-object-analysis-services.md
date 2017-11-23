---
title: Conceder permisos en un objeto de origen de datos (Analysis Services) | Documentos de Microsoft
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.asvs.roledesignerdialog.datasources.f1
helpviewer_keywords:
- read/write permissions
- user access rights [Analysis Services], data sources
- security [Analysis Services], data sources
- connection strings [Analysis Services]
- data sources [Analysis Services], security
ms.assetid: b4e302d3-c93b-4383-aa4a-37d15c129830
caps.latest.revision: "38"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c774f7711a32eb512c28914146b05f2db52f4b2c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="grant-permissions-on-a-data-source-object-analysis-services"></a>Otorgar permisos para un objeto de origen de datos (Analysis Services)
  Normalmente, la mayoría de los usuarios de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no necesitan acceso a los orígenes de datos subyacentes de un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Los usuarios normalmente solo consultan los datos en una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . No obstante, en el contexto de minería de datos, como en el de realizar predicciones basadas en un modelo de minería de datos, un usuario tiene que combinar los datos obtenidos de un modelo de minería de datos con los datos proporcionados por el usuario. Para conectar con el origen de datos que contiene los datos proporcionados por el usuario, el usuario emplea una consulta de Extensiones de minería de datos (DMX) que contiene la cláusula [OPENQUERY &#40;DMX&#41;](../../dmx/source-data-query-openquery.md) y [OPENROWSET &#40;DMX&#41;](../../dmx/source-data-query-openrowset.md).  
  
 Para ejecutar una consulta DMX que conecte con un origen de datos, el usuario debe tener acceso al objeto de origen de datos en la base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . De forma predeterminada, solamente los administradores de servidor y de base de datos tienen acceso a los objetos de origen de datos. Es decir, un usuario no puede tener acceso a un objeto de origen de datos salvo que un administrador le conceda permisos.  
  
> [!IMPORTANT]  
>  Por razones de seguridad, está deshabilitado el envío de consultas DMX mediante una cadena de conexión abierta en la cláusula OPENROWSET.  
  
## <a name="set-read-permissions-to-a-data-source"></a>Establecer permisos de Lectura a un origen de datos  
 A un rol de base de datos se le pueden conceder permisos de lectura o ningún permiso de acceso a un objeto de origen de datos.  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conéctese a la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], expanda **Roles** para la base de datos correspondiente en el Explorador de objetos y, después, haga clic en un rol de base de datos (o cree un rol de base de datos).  
  
2.  En el panel **Acceso del origen de datos** , busque el objeto de origen de datos en la lista **Origen de datos** y, después, seleccione **Lectura** en la lista **Acceso** para el origen de datos. Si esta opción no está disponible, compruebe el panel **General** para ver si se ha seleccionado Control total. Si Control total ya está proporcionando el permiso, no podrá invalidar los permisos en el origen de datos.  
  
## <a name="working-with-the-connection-string-used-by-a-data-source-object"></a>Trabajar con la cadena de conexión utilizada por un objeto de origen de datos  
 El objeto de origen de datos contiene la cadena de conexión que se utiliza para conectar con el origen de datos subyacente. Esta cadena de conexión puede especificar uno de los siguientes:  
  
-   **Un nombre de usuario y una contraseña**  
  
     Si la cadena de conexión que utiliza un objeto de origen de datos especifica un nombre de usuario y una contraseña, podría crear varios objetos de origen de datos, cada uno con cuentas de usuario diferentes. La creación de varios objetos de origen de datos permite a los usuarios obtener acceso a objetos de origen de datos específicos e impide que estos usuarios tengan acceso a otros objetos de origen de datos. Estos otros objetos de origen de datos los puede utilizar [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para procesar objetos, por ejemplo, cubos y modelos de minería de datos.  
  
-   **Especificar la autenticación de Windows**  
  
     Si la cadena de conexión que usa un objeto de origen de datos especifica la autenticación de Windows, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] deberá suplantar al cliente. Si el origen de datos está en un equipo remoto, los dos equipos deben tener establecida la confianza para suplantar mediante la autenticación Kerberos o se producirá un error en la consulta. Consulte [Configure Analysis Services for Kerberos constrained delegation](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md) para obtener más información.  
  
     Si el cliente no permite suplantar (mediante la propiedad Impersonation Level en OLE DB y otros componentes cliente), [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] intentará establecer una conexión anónima con el origen de datos subyacente. Las conexiones anónimas a orígenes de datos remotos no suelen establecerse correctamente, ya que la mayoría de los orígenes de datos no aceptan conexiones anónimas.  
  
## <a name="see-also"></a>Vea también  
 [Orígenes de datos en modelos multidimensionales](../../analysis-services/multidimensional-models/data-sources-in-multidimensional-models.md)   
 [Propiedades de la cadena de conexión &#40; Analysis Services &#41;](../../analysis-services/instances/connection-string-properties-analysis-services.md)   
 [Metodologías de autenticación admitidas por Analysis Services](../../analysis-services/instances/authentication-methodologies-supported-by-analysis-services.md)   
 [Conceder acceso personalizado a la dimensión de datos &#40; Analysis Services &#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md)   
 [Otorgar permisos para cubos o modelos &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md)   
 [Otorgar acceso personalizado a los datos de las celdas &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md)  
  
  
