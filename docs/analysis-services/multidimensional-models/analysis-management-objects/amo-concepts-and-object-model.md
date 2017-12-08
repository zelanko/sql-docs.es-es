---
title: Modelo de objetos y conceptos de AMO | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- AMO, classes
- Analysis Management Objects, classes
- objects [Analysis Management Objects]
- AMO, objects
- classes [AMO]
- AMO
- Analysis Management Objects
- Analysis Management Objects, objects
ms.assetid: 3b0cdf8e-46d5-4dfe-8b2c-233c27e1473e
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4943e1ff3c3c18814993a85bd108bb473e644726
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="amo-concepts-and-object-model"></a>Modelo de objetos y conceptos de AMO
  Este tema proporciona una definición de Analysis Management Objects (AMO), cómo AMO está relacionada con otras herramientas y bibliotecas suministradas en la arquitectura de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]y una explicación conceptual de todos los objetos principales de AMO.  
  
 AMO es una colección completa de clases de administración de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] que se puede usar mediante programación, bajo el espacio de nombres de <xref:Microsoft.AnalysisServices>, en un entorno administrado. Las clases se incluyen en el archivo AnalysisServices.dll, que normalmente se encuentra donde el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] el programa de instalación instala los archivos, en la carpeta \100\SDK\Assemblies\\. Para usar clases de AMO, incluya una referencia a este ensamblado en sus proyectos.  
  
 Mediante AMO puede crear, modificar y eliminar objetos tales como cubos, dimensiones, estructuras de minería de datos, y [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] las bases de datos; sobre todos estos objetos, se pueden realizar acciones de la aplicación en .NET Framework. Además, puede procesar y actualizar la información almacenada en las bases de datos de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
 Con AMO no se pueden consultar datos. Para consultar los datos, use [desarrollar con ADOMD.NET](../../../analysis-services/multidimensional-models/adomd-net/developing-with-adomd-net.md).  
  
 Este tema contiene las siguientes secciones:  
  
 [AMO en la arquitectura de Analysis Services](#AMOintheAnalysisServicesArchitecture)  
  
 [Arquitectura AMO](#AMOArchitecture)  
  
 [A través de AMO](#bkmk_UsingAMO)  
  
 [Automatizar tareas administrativas con AMO](#AutomatingAdministrativeTaskswithAMO)  
  
##  <a name="AMOintheAnalysisServicesArchitecture"></a>AMO en la arquitectura de Analysis Services  
 Por diseño, AMO está pensado únicamente para administrar objetos, no para consultar datos. Si el usuario necesita consulta [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] datos desde una aplicación cliente, debe usar la aplicación cliente [desarrollar con ADOMD.NET](../../../analysis-services/multidimensional-models/adomd-net/developing-with-adomd-net.md).  
  
##  <a name="AMOArchitecture"></a>Arquitectura AMO  
 AMO es una biblioteca completa de clases diseñada para administrar una instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] desde una aplicación de cliente en código administrado en la versión 2.0 de .NET Framework.  
  
 La biblioteca de clases AMO está diseñada como una jerarquía de clases, donde se deben crear instancias de ciertas clases antes que otras para poder utilizarlas en su código. También se pueden crear en su código instancias de clases auxiliares en cualquier momento, aunque probablemente habrá creado una o más instancias de las clases de jerarquía antes de usar cualquiera de las clases auxiliares.  
  
 La ilustración siguiente es una vista de alto nivel de la jerarquía AMO que incluye las clases principales. La ilustración muestra la posición de las clases entre sus contenedores y sus elementos del mismo nivel. <xref:Microsoft.AnalysisServices.Dimension> pertenece a <xref:Microsoft.AnalysisServices.Database> y <xref:Microsoft.AnalysisServices.Server>, y se puede crear al mismo tiempo como <xref:Microsoft.AnalysisServices.DataSource> y <xref:Microsoft.AnalysisServices.MiningStructure>. Se deben crear instancias de ciertas clases del mismo nivel antes de poder usar otras. Por ejemplo, tiene que crear una instancia de <xref:Microsoft.AnalysisServices.DataSource> antes de agregar un nuevo <xref:Microsoft.AnalysisServices.Dimension> o <xref:Microsoft.AnalysisServices.MiningStructure>.  
  
 ![Vista de alto nivel de las clases AMO](../../../analysis-services/multidimensional-models/analysis-management-objects/media/amo-highlevelview-majorobjectshighlighted.gif "AMO clases de vista de alto nivel")  
  
 A *objeto principal* es una clase que representa un objeto completo como una entidad completa y no como parte de otro objeto. Los objetos principales incluyen <xref:Microsoft.AnalysisServices.Server>, <xref:Microsoft.AnalysisServices.Cube>, <xref:Microsoft.AnalysisServices.Dimension> y <xref:Microsoft.AnalysisServices.MiningStructure>, porque éstas son entidades por sí solas. Sin embargo, <xref:Microsoft.AnalysisServices.Level> no es un objeto principal porque es una parte constituyente de <xref:Microsoft.AnalysisServices.Dimension>. Los objetos principales se pueden crear, eliminar, modificar o procesar independientemente de otros objetos. Los objetos secundarios son objetos que únicamente se pueden crear como parte de la creación de un objeto principal primario. Los objetos secundarios normalmente se crean en la creación del objeto principal. Los valores de los objetos secundarios se deberían definir en el momento de su creación, porque no hay ninguna creación predeterminada para objetos secundarios.  
  
 La ilustración siguiente muestra los objetos principales que contiene un objeto <xref:Microsoft.AnalysisServices.Server>.  
  
 ![Objetos principales de AMO resaltados](../../../analysis-services/multidimensional-models/analysis-management-objects/media/amo-majorobjects.gif "objetos principales de AMO resaltados")  
  
 ![Principales objetos de AMO resaltados (2)](../../../analysis-services/multidimensional-models/analysis-management-objects/media/amo-majorobjects-02.gif "principales objetos de AMO resaltados (2)")  
  
 Al programar con AMO, la asociación entre clases y clases contenidas usa atributos de tipo de colección, por ejemplo <xref:Microsoft.AnalysisServices.Server> y <xref:Microsoft.AnalysisServices.Dimension>. Para trabajar con una instancia de una clase contenida, adquiera en primer lugar una referencia a un objeto de colección que contenga o pueda tener la clase contenida. Después, encuentre el objeto concreto que está buscando en la colección y, a continuación, obtendrá una referencia al objeto para empezar a trabajar con él.  
  
### <a name="amo-classes"></a>Clases AMO  
 AMO es una biblioteca de clases diseñada para administrar una instancia de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] de una aplicación cliente. La biblioteca AMO se puede considerar como grupos de objetos relacionados de forma lógica que se utilizan para lograr una tarea específica. Las clases AMO se pueden clasificar de la manera siguiente:  
  
|Conjunto de clases|Finalidad|  
|---------------|-------------|  
|[Clases fundamentales de AMO](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-fundamental-classes.md)|Clases necesarias para trabajar con cualquier otro conjunto de clases.|  
|[Clases de OLAP en AMO](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-olap-classes.md)|Clases que permiten administrar objetos OLAP en [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Clases de minería de datos de AMO](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-data-mining-classes.md)|Clases que permiten administrar objetos de minería de datos en [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Clases de seguridad de AMO](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-security-classes.md)|Clases que permiten controlar el acceso a otros objetos y mantener la seguridad.|  
|[Otras clases y métodos de AMO](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-other-classes-and-methods.md)|Clases y métodos que sirven de ayuda a los administradores de OLAP o de la minería de datos para completar sus tareas cotidianas.|  
  
##  <a name="bkmk_UsingAMO"></a>A través de AMO  
 AMO es especialmente útil a la hora de automatizar tareas repetitivas, por ejemplo al crear nuevas particiones en un grupo de medida basado en nuevos datos de la tabla de hechos, o al volver a entrenar un modelo de minería de datos basado en nuevos datos. Normalmente, estas tareas que crean nuevos objetos se realizan por meses, semanas o trimestres y la aplicación puede denominar a los nuevos objetos con facilidad, a partir de los nuevos datos.  
  
##### <a name="analysis-services-administrators"></a>Administradores de Analysis Services  
 Los administradores de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] pueden usar AMO para automatizar el procesamiento de bases de datos de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Para diseñar e implementar las bases de datos de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], debería utilizar [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)].  
  
##### <a name="developers"></a>Desarrolladores  
 Los desarrolladores de software pueden usar AMO para desarrollar interfaces administrativas para conjuntos de usuarios especificados. Estas interfaces pueden restringir el acceso a los objetos [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] y limitar a los usuarios a ciertas tareas. Por ejemplo, con AMO podría crear una aplicación de copia de seguridad para permitir que un usuario pueda ver todos los objetos de la base de datos, seleccionar cualquiera de las bases de datos y realizar una copia de seguridad de la misma en cualquier conjunto de dispositivos especificado.  
  
 Los desarrolladores de software también pueden incrustar la lógica de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] en sus aplicaciones. Para esto, pueden crear cubos, dimensiones, estructuras de minería de datos y modelos de minería de datos basados en datos proporcionados por el usuario u otros factores.  
  
##### <a name="olap-advanced-users"></a>Usuarios avanzados OLAP  
 Los usuarios avanzados OLAP normalmente son analistas de datos u otros usuarios de datos con experiencia que tienen amplios conocimientos en programación y que desean mejorar el análisis de datos mediante un uso más cercano de los objetos de datos. Para aquellos usuarios que necesitan trabajar sin conexión, AMO puede ser muy útil a la hora de automatizar la creación de cubos locales antes de estar sin conexión.  
  
##### <a name="data-mining-advanced-users"></a>Usuarios avanzados de minería de datos  
 Para los usuarios avanzados de minería de datos, AMO es muy útil si se tienen conjuntos grandes de modelos que hay que volver a entrenar periódicamente.  
  
##  <a name="AutomatingAdministrativeTaskswithAMO"></a>Automatizar tareas administrativas con AMO  
 Mediante [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], la mayoría de las tareas repetitivas se diseñan, implementan y mantienen mejor que si se programan como una aplicación en cualquier lenguaje de su elección. Sin embargo, para tareas repetitivas que no se pueden automatizar mediante [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], se puede usar AMO. AMO también es útil cuando se desea programar una aplicación especializada de Business Intelligence mediante [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
##### <a name="automatic-object-management"></a>Administración automática de objeto  
 Con AMO es muy sencillo crear, actualizar o eliminar objetos [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] (por ejemplo <xref:Microsoft.AnalysisServices.Database>, <xref:Microsoft.AnalysisServices.Dimension>, <xref:Microsoft.AnalysisServices.Cube>, minería de datos <xref:Microsoft.AnalysisServices.MiningStructure> y <xref:Microsoft.AnalysisServices.MiningModel> o <xref:Microsoft.AnalysisServices.Role>) a partir de entradas de usuario o de nuevos datos adquiridos. AMO es ideal para aplicaciones de instalación que tienen que implementar una solución desarrollada de un fabricante de software independiente a un cliente final. La aplicación de instalación puede comprobar si existe una versión anterior y actualizar la estructura, quitar objetos que ya no son útiles y crear otros nuevos. Si no hay ninguna versión anterior, entonces puede crear todo desde el principio.  
  
 AMO puede ser eficaz para crear nuevas particiones basadas en nuevos datos y puede quitar particiones anteriores que se hayan excedido del ámbito del proyecto. Por ejemplo, para una solución de análisis financiero que funciona con los datos de los últimos 36 meses, en cuanto se reciben los datos de un nuevo mes, se puede quitar el mes antiguo 37. Para optimizar el rendimiento, las nuevas agregaciones se pueden diseñar en función del uso y aplicación de los últimos 12 meses.  
  
##### <a name="automatic-object-processing"></a>Procesamiento de objetos automático  
 El procesamiento de objetos y la disponibilidad actualizada se pueden lograr mediante AMO como respuesta a ciertos eventos más allá de los datos de flujo normal y de las tareas programadas que usan [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)].  
  
##### <a name="automatic-security-management"></a>Administración de seguridad automática  
 La administración de seguridad se puede automatizar para incluir nuevos usuarios a los roles y permisos, o bien para quitar a otros usuarios en cuanto expira su tiempo. Se pueden crear nuevas interfaces para simplificar la administración de seguridad para los administradores de seguridad. Esto puede resultar más sencillo que mediante [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)].  
  
##### <a name="automatic-backup-management"></a>Administración de copia de seguridad automática  
 La administración de copia de seguridad automática se puede realizar mediante las tareas de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] o creando aplicaciones AMO especializadas que se ejecutan de forma automática. Mediante AMO puede desarrollar interfaces de copia de seguridad para operadores que les servirá de ayuda en su trabajo diario.  
  
##### <a name="tasks-amo-is-not-intended-for"></a>Limitaciones de las tareas AMO  
 AMO no se puede usar para consultar datos. Para consultar datos de [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], incluidos cubos y modelos de minería de datos, use ADOMD.NET de una aplicación de usuario. Para obtener más información, consulte [desarrollar con ADOMD.NET](../../../analysis-services/multidimensional-models/adomd-net/developing-with-adomd-net.md).  
  
  
