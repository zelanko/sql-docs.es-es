---
title: 'Tutorial SSIS: Implementar paquetes | Microsoft Docs'
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- deployment tutorial [Integration Services]
- deploying packages [Integration Services]
- SSIS, tutorials
- Integration Services, tutorials
- deploying packages [Integration Services], installing
- SQL Server Integration Services, tutorials
- walkthroughs [Integration Services]
- deployment utility [Integration Services]
- deploying packages [Integration Services], configurations
ms.assetid: de18468c-cff3-48f4-99ec-6863610e5886
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 49aff131d55dbc38511fdae0dc930e161904a985
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48188975"
---
# <a name="ssis-tutorial-deploying-packages"></a>Tutorial de SSIS: Implementar paquetes
  [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] proporciona herramientas que permiten implementar paquetes en otro equipo. Las herramientas de implementación también administran las dependencias, como configuraciones y archivos que necesita el paquete. En este tutorial, aprenderá a usar estas herramientas para instalar paquetes y sus dependencias en un equipo de destino.  
  
 Primero, realizará tareas para preparar la implementación. Creará un nuevo proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] y agregará paquetes y archivos de datos existentes al proyecto. No creará nuevos paquetes desde el principio; solamente trabajará con paquetes completados creados exclusivamente para este tutorial. En este tutorial no modificará la funcionalidad de los paquetes; no obstante, después de agregar los paquetes al proyecto, puede resultar útil abrirlos en el Diseñador de [!INCLUDE[ssIS](../includes/ssis-md.md)] y revisar el contenido de cada paquete. Mediante el examen de los paquetes, conocerá las dependencias de los paquetes como los archivos de registro y otras características interesantes de los mismos.  
  
 Antes de llevar a cabo la implementación, también actualizará los paquetes para utilizar configuraciones. Las configuraciones permiten la actualización de las propiedades de los paquetes y los objetos de paquete en tiempo de ejecución. En este tutorial utilizará configuraciones para actualizar las cadenas de conexión de archivos de registro y de texto, y las ubicaciones de los archivos XML y XSD que usa el paquete. Para obtener más información, consulte [Configuraciones de paquetes](../../2014/integration-services/package-configurations.md) y [Crear configuraciones de paquetes](../../2014/integration-services/create-package-configurations.md).  
  
 Después de comprobar que los paquetes funcionan correctamente en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], creará el paquete de implementación que se usará para instalar los paquetes. El paquete de implementación contendrá los archivos de paquete y otros elementos que ha agregado al proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , las dependencias del paquete que [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] incluye automáticamente y la utilidad de implementación que ha generado. Para más información, consulte [Create a Deployment Utility](../../2014/integration-services/create-a-deployment-utility.md).  
  
 A continuación, copiará el paquete de implementación en el equipo de destino y ejecutará el Asistente para la instalación de paquetes para instalar los paquetes y las dependencias de paquete. Los paquetes se instalarán en la base de datos msdb de SQL Server, y los archivos auxiliares y de ayuda se instalarán en el sistema de archivos. Puesto que los paquetes implementados utilizan configuraciones, actualizará la configuración para que use nuevos valores que permitirán que los paquetes se ejecuten correctamente en el nuevo entorno.  
  
 Por último, ejecutará los paquetes en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] con la Utilidad de ejecución de paquetes.  
  
 El objetivo de este tutorial es simular la complejidad de los problemas reales de implementación que puede encontrarse. No obstante, si no puede implementar los paquetes en otro equipo, puede seguir este tutorial instalando los paquetes en la base de datos msdb en una instancia local de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]y, a continuación, ejecutar los paquetes desde [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] en la misma instancia.  
  
## <a name="what-you-will-learn"></a>Aprendizaje  
 La mejor forma de familiarizarse con las nuevas herramientas, los controles y las características disponibles en [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] es usándolas. Este tutorial le guía por los pasos para crear un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] y, a continuación, agregar los paquetes y otros archivos necesarios al proyecto. Después de completar el proyecto, creará un paquete de implementación, copiará el paquete al equipo de destino e instalará los paquetes en él.  
  
## <a name="requirements"></a>Requisitos  
 Este tutorial está concebido para los usuarios familiarizados con las operaciones básicas del sistema de archivos, pero que no conocen con detalle las nuevas características disponibles en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Para comprender mejor básica [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] conceptos que utilizará en este tutorial, puede resultarle útil completar primero el siguiente [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] tutoriales: [ejecutar la importación de SQL Server y el Asistente para exportación de](import-export-data/start-the-sql-server-import-and-export-wizard.md) y [ Tutorial SSIS: Crear un paquete ETL sencillo](../integration-services/ssis-how-to-create-an-etl-package.md).  
  
 **Equipo de origen.** El equipo en el que creará el paquete de implementación debe tener instalados los siguientes componentes:  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con la base de datos AdventureWorks. Con el objeto de mejorar la seguridad, las bases de datos de ejemplo no se instalan de forma predeterminada. Puede descargar la base de datos de ejemplo de [CodePlex](http://msftdbprodsamples.codeplex.com/releases/view/125550).  
  
-   Debe tener permiso para crear y quitar tablas en AdventureWorks.  
  
-   Este tutorial también necesita datos de ejemplo, paquetes completados, configuraciones y un archivo Léame. Los archivos para estos elementos se instalan junto con los ejemplos. Si no encuentra estos datos, regrese al procedimiento anterior y complete la instalación según se indica.  
  
-   El entorno de Business Intelligence Development Studio, [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
 **Equipo de destino.** El equipo en el que implementará los paquetes debe tener instalados los siguientes componentes:  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con la base de datos AdventureWorks.  
  
-   [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]   
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
-   Debe tener permiso para crear y quitar tablas en AdventureWorks y ejecutar paquetes en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
-   Tiene que leer y escribir permisos en la tabla sysssispackages de la msdb[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] base de datos del sistema.  
  
 Si planea implementar paquetes en el mismo equipo en el que va a crear el paquete de implementación, ese equipo debe cumplir los requisitos de los equipos de origen y destino.  
  
 **Tiempo estimado para completar este tutorial:** 2 horas  
  
## <a name="lessons-in-this-tutorial"></a>Lecciones de este tutorial  
 [Lección 1: Preparar la creación del paquete de implementación](../integration-services/lesson-1-preparing-to-create-the-deployment-bundle.md)  
 En esta lección, se preparará para implementar una solución ETL creando un nuevo proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] y agregando los paquetes y otros archivos necesarios al proyecto.  
  
 [Lección 2: Crear el paquete de implementación](../integration-services/lesson-2-create-the-deployment-bundle-in-ssis.md)  
 En esta lección, generará una utilidad de implementación y comprobará que el paquete de implementación incluye los archivos necesarios.  
  
 [Lección 3: Instalar paquetes](../integration-services/lesson-3-install-ssis-package.md)  
 En esta lección, copiará el paquete de implementación en el equipo de destino, instalará los paquetes y, a continuación, los ejecutará.  
  
![Icono de Integration Services (pequeño)](media/dts-16.gif "icono de Integration Services (pequeño)")**mantenerse actualizado con Integration Services** <br /> Para obtener las descargas, artículos, ejemplos y vídeos más recientes de Microsoft, así como soluciones seleccionadas de la comunidad, visite la página de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en MSDN:<br /><br /> [Visite la página de Integration Services en MSDN](http://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para recibir notificaciones automáticas de estas actualizaciones, suscríbase a las fuentes RSS disponibles en la página.  
  
  
