---
title: Autorizar el acceso a objetos y operaciones (Analysis Services) | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 88290b9598ffdbbcfc90a738654a9485107da464
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34024042"
---
# <a name="authorizing-access-to-objects-and-operations-analysis-services"></a>Cómo autorizar el acceso a objetos y operaciones (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  El acceso de los usuarios que no sean administradores a los cubos, dimensiones y modelos de minería de datos de una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] se obtiene mediante la pertenencia a uno o varios roles de base de datos. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Los administradores crean estos roles de base de datos, conceden permisos de Lectura o de Lectura y escritura en objetos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y luego asignan usuarios y grupos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows a cada rol.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] establece los permisos efectivos para un usuario o grupo específico de Windows al combinar los permisos que están asociados con cada rol de base de datos al que el usuario o grupo pertenece. En consecuencia, si un rol de base de datos no concede a un usuario o grupo permiso para ver una dimensión, medida o atributo y otro rol diferente sí lo hace, el usuario o grupo tendrá permiso para ver el objeto.  
  
> [!IMPORTANT]  
>  Los miembros del rol de administrador de servidor de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y los miembros del rol de base de datos que tienen los permisos de Control total (administrador) tienen acceso a todos los datos y metadatos de la base de datos, y no necesitan permisos adicionales para ver objetos específicos. Además, a los miembros del rol de servidor de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no se les puede denegar el acceso a ningún objeto de ninguna base de datos. Además, a los miembros de un rol de base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que tenga los permisos de Control total (administrador) no se les puede denegar el acceso a ningún objeto de dicha base de datos. Se pueden autorizar operaciones administrativas especializadas, como el procesamiento, a través de roles independientes con menos permisos. Vea [Otorgar permisos de procesamiento &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-process-permissions-analysis-services.md) para obtener más información.  
  
## <a name="list-roles-defined-for-your-database"></a>Lista de roles definidos para la base de datos  
 Los administradores pueden ejecutar una simple consulta DMV en SQL Server Management Studio para obtener una lista de todos los roles definidos en el servidor.  
  
1.  En SSMS, haga clic con el botón derecho en una base de datos y seleccione **Nueva consulta** | **MDX**.  
  
2.  Escriba la siguiente consulta y presione F5 para ejecutar:  
  
    ```  
    Select * from $SYSTEM.DBSCHEMA_CATALOGS  
    ```  
  
     Los resultados incluyen el nombre de la base de datos, una descripción, el nombre de los roles y la fecha de la última modificación. Con esta información como punto de partida, puede ir a bases de datos individuales para comprobar la pertenencia y los permisos de un rol concreto.  
  
## <a name="top-down-overview-of-analysis-services-authorization"></a>Introducción general descendente a las autorizaciones en Analysis Services  
 Esta sección trata sobre el flujo de trabajo básico para configurar permisos.  
  
 **Paso 1: Administración de servidores**  
  
 El primer paso es decidir quién tendrá derechos de administrador en el nivel de servidor. Durante la instalación, el administrador local que instala SQL Server debe especificar una o varias cuentas de Windows como el administrador de servidor de Analysis Services. Los administradores de servidor cuentan con todos los permisos posibles para un servidor, lo cual incluye los permisos para ver, modificar y eliminar cualquier objeto del servidor o para ver los datos asociados. Una vez se ha completado la instalación, los administradores de servidor pueden agregar o quitar cuentas para cambiar la pertenencia de este rol. Vea [Conceder permisos de administrador de servidor (Analysis Services)](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md) para obtener más información sobre este nivel de permisos.  
  
 **Paso 2: Administración de bases de datos**  
  
 A continuación, después de crearse una solución tabular o multidimensional, se implementa en el servidor como base de datos. Un administrador de servidor puede delegar tareas de administración de base de datos; para ello, debe definir un rol que tenga permisos de Control total para la base de datos relevante. Los miembros que pertenecen a este rol pueden procesar o consultar objetos en la base de datos, así como crear roles adicionales para obtener acceso a cubos, dimensiones y otros objetos de la base de datos. Vea [Otorgar permisos de base de datos &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-database-permissions-analysis-services.md) para obtener más información.  
  
 **Paso 3: Permitir el acceso de cubos o modelos para las cargas de trabajo de procesamiento y consulta**  
  
 De forma predeterminada, solo los administradores del servidor y la base de datos tienen acceso a los cubos o los modelos tabulares. Con el fin de que estas estructuras de datos se encuentren disponibles para otras personas de la organización, se deben hacer otras asignaciones de rol que hagan corresponder cuentas de usuario y grupo de Windows a cubos o modelos, junto con los permisos que especifiquen privilegios de **Read** . Vea [Otorgar permisos para cubos o modelos &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md) para obtener más información.  
  
 Las tareas de procesamiento se pueden aislar de otras funciones administrativas, de forma que los administradores de servidor y de base de datos puedan delegar esta tarea a otras personas o bien, configurar un procesamiento desatendido mediante la especificación de cuentas de servicio que ejecuten software de programación. Vea [Otorgar permisos de procesamiento &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-process-permissions-analysis-services.md) para obtener más información.  
  
> [!NOTE]  
>  Los usuarios no necesitan ningún permiso para las tablas relacionales en la base de datos relacional subyacente desde la que [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] carga sus datos y no necesitan ningún permiso en el nivel de archivo para el equipo en el que se está ejecutando la instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 **Paso 4 (opcional): Permitir o denegar el acceso a objetos interiores del cubo**  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ofrece configuración de seguridad para establecer permisos sobre objetos individuales, incluidos los miembros de la dimensión y células de un modelo de datos. Para obtener más información, vea [Conceder acceso personalizado a datos de dimensión &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-dimension-data-analysis-services.md) y [Otorgar acceso personalizado a los datos de las celdas &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-custom-access-to-cell-data-analysis-services.md).  
  
 También puede modificar permisos de acuerdo a la identidad del usuario. Por lo general, esta acción se denomina seguridad dinámica y se implementa con la función [UserName &#40;MDX&#41;](../../mdx/username-mdx.md).  
  
## <a name="best-practices"></a>Procedimientos recomendados  
 Para administrar con más eficacia los permisos, se recomienda un enfoque similar al siguiente:  
  
1.  Cree roles según la función (por ejemplo, dbadmin, cubedeveloper, processadmin), de forma que independientemente de quien ostente el rol, pueda ver rápidamente lo que permite hacer dicho rol. Según se dijo anteriormente, se pueden definir los roles en la definición del modelo, de forma que esos roles se mantienen en implementaciones posteriores de la solución.  
  
2.  Cree el correspondiente grupo de seguridad de Windows en Active Directory y, posteriormente, conserve este grupo de seguridad en Active Directory para garantizar que contiene las cuentas individuales apropiadas. De esta forma, la responsabilidad de la pertenencia a grupos de seguridad recaerá sobre especialistas en seguridad que ya tienen amplia experiencia con las herramientas y procesos que se usan para el mantenimiento de las cuentas en la organización.  
  
3.  Genere scripts en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] de forma que pueda replicar rápidamente las asignaciones de roles en cualquier ubicación donde se vuelva a implementar el modelo a partir de sus archivos de origen en un servidor. Vea [Otorgar permisos para cubos o modelos &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-cube-or-model-permissions-analysis-services.md) para obtener información sobre cómo generar rápidamente un script.  
  
4.  Adopte una convención de nomenclatura que refleje el ámbito y la pertenencia del rol. Los nombres de rol solo se ven en las herramientas de diseño y de administración, por tanto, use una convención de nomenclatura que tenga sentido para los especialistas en seguridad de cubos. Por ejemplo, **processadmin-windowsgroup1** indica acceso de lectura y derechos de procesamiento para las personas de la organización cuyas cuentas de usuario de Windows individuales pertenezcan al grupo de seguridad **windowsgroup1** .  
  
     Si incluye información sobre la cuenta le resultará útil para llevar un seguimiento de las cuentas que se usan en los diversos roles. Dado que los roles se van sumando unos a otros, los roles combinados asociados a **windowsgroup1** componen el conjunto efectivo de permisos para las personas que pertenecen a ese grupo de seguridad.  
  
5.  Los desarrolladores de cubos necesitarán permisos de Control total para los modelos y bases de datos en desarrollo, pero únicamente necesitarán permisos de Lectura una vez que se haya incorporado una base de datos en un servidor de producción. Recuerde crear definiciones y asignaciones de rol para todos los escenarios, lo cual incluye implementaciones de desarrollo, prueba y producción.  
  
 Si aplica un enfoque como este, minimizará los cambios en las definiciones de rol y las pertenencias a roles del modelo, y además aportará visibilidad a las asignaciones de rol, lo cual facilita la implementación y mantenimiento de los permisos para los cubos.  
  
## <a name="see-also"></a>Vea también  
 [Conceder permisos de administrador de servidor (Analysis Services)](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md)   
 [Roles y permisos &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/roles-and-permissions-analysis-services.md)   
 [Metodologías de autenticación admitidas por Analysis Services](../../analysis-services/instances/authentication-methodologies-supported-by-analysis-services.md)  
  
  
