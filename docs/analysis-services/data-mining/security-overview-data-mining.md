---
title: "Información general sobre seguridad (minería de datos) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: security [Analysis Services - data mining], about security
ms.assetid: 387bde00-bcf3-4612-b27b-f9f608dbf71e
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 1292f8fc828d938d59bd9ceafe8cbc467da8e02d
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="security-overview-data-mining"></a>Información general de Seguridad (minería de datos)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]El proceso de protección [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] se produce en varios niveles. Debe proteger cada instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y sus orígenes de datos para asegurarse de que solo los usuarios autorizados tengan permisos de lectura o lectura/escritura para las dimensiones, los modelos de minería de datos y los orígenes de datos seleccionados. También debe proteger los orígenes de datos subyacentes para evitar que usuarios no autorizados puedan poner en riesgo información empresarial confidencial. El proceso de protección de una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] se describe en los temas siguientes.  
  
##  <a name="bkmk_Architecture"></a> Arquitectura de seguridad  
 Consulte los siguientes recursos para obtener información acerca de la arquitectura de seguridad básica de una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], incluida la forma en que [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] utiliza la autenticación de Windows [!INCLUDE[msCoName](../../includes/msconame-md.md)] para autenticar el acceso de los usuarios.  
  
-   [Roles de seguridad &#40;Analysis Services - Datos multidimensionales&#41;](../../analysis-services/multidimensional-models/olap-logical/security-roles-analysis-services-multidimensional-data.md)  
  
-   [Propiedades de seguridad](../../analysis-services/server-properties/security-properties.md)  
  
-   [Configurar las cuentas de servicio &#40;Analysis Services&#41;](../../analysis-services/instances/configure-service-accounts-analysis-services.md)  
  
-   [Cómo autorizar el acceso a objetos y operaciones &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)  
  
##  <a name="bkmk_Logon"></a> Configurar la cuenta de inicio de sesión para Analysis Services  
 Debe seleccionar una cuenta de inicio de sesión adecuada para [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y especificar los permisos para la cuenta. Debe asegurarse de que la cuenta de inicio de sesión de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] solo tenga los permisos necesarios para realizar determinadas tareas, así como los permisos adecuados para los orígenes de datos subyacentes.  
  
 En la minería de datos, para generar y procesar los modelos se necesita un conjunto de permisos diferente del necesario para ver o consultar los modelos. Realizar predicciones con un modelo es un tipo de consulta y no requiere permisos administrativos.  
  
##  <a name="bkmk_Instance"></a> Proteger una instancia de Analysis Services  
 A continuación, debe proteger el equipo de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , el sistema operativo Windows instalado en el equipo de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , el propio [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y los orígenes de datos que utiliza [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
##  <a name="bkmk_Access"></a> Configurar el acceso a Analysis Services  
 Cuando se configuran y definen los usuarios autorizados de una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], se debe determinar los usuarios que también deben tener permiso para administrar determinados objetos de base de datos, qué usuarios pueden ver la definición de los objetos o examinar los modelos, y qué usuarios pueden tener acceso directamente a los orígenes de datos.  
  
##  <a name="bkmk_DMspecial"></a> Consideraciones especiales para la minería de datos  
 Para que un analista o programador pueda crear y probar modelos de minería de datos, debe proporcionarle permisos administrativos en la base de datos donde se almacenan dichos modelos. En consecuencia, el analista o programador de minería de datos podrá crear o eliminar otros objetos que no estén relacionados con la minería de datos, incluyendo objetos de minería de datos creados con anterioridad y que usan otros analistas o programadores, u objetos OLAP que no estén incluidos en la solución de minería de datos.  
  
 Por ello, al crear una solución para la minería de datos, debe hallar un equilibrio entre las necesidades del analista o programador para desarrollar, probar y ajustar los modelos, y las necesidades de otros usuarios, tomando las medidas adecuadas para proteger los objetos de base de datos existentes. Un posible enfoque consiste en crear una base de datos independiente dedicada a la minería de datos, o crear bases de datos independientes para cada analista.  
  
 Aunque la creación de modelos requiere el nivel más alto de permisos, puede controlar el acceso del usuario a los modelos de minería de datos para otras operaciones, como el procesamiento, la exploración o la consulta, usando la seguridad basada en roles. Cuando se crea un rol, se establecen permisos específicos de los objetos de minería de datos. Cualquier usuario que sea miembro de un rol tiene automáticamente todos los permisos asociados a ese rol.  
  
 Además, los modelos de minería de datos a menudo hacen referencia a orígenes de datos que contienen información confidencial. Si la estructura y el modelo de minería de datos se han configurado para permitir a los usuarios obtener detalles del modelo para los datos de la estructura, debe tomar las precauciones necesarias para enmascarar la información confidencial o limitar el número de usuarios que tienen acceso a los datos subyacentes.  
  
 Si usa los paquetes de Integration Services para limpiar los datos, actualizar los modelos de minería de datos o realizar predicciones, debe asegurarse de que el servicio Integration Services tiene los permisos adecuados en la base de datos donde se almacena el modelo y en los datos de origen.  
  
## <a name="see-also"></a>Vea también  
 [Roles y permisos &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/roles-and-permissions-analysis-services.md)  
  
  
