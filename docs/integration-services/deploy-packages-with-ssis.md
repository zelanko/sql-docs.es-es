---
title: Implementar paquetes de SSIS | Documentos de Microsoft
ms.custom: 
ms.date: 11/16/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
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
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: a6aeda8e785fcaabef253a8256b5f6f7a842a324
ms.openlocfilehash: ced8482c76d970ccd2c146fff04d63279082b1c9
ms.contentlocale: es-es
ms.lasthandoff: 09/21/2017

---
# <a name="deploy-packages-with-ssis"></a>Implementar paquetes con SSIS
[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] proporciona herramientas que permiten implementar paquetes en otro equipo. Las herramientas de implementación también administran las dependencias, como configuraciones y archivos que necesita el paquete. En este tutorial, aprenderá a usar estas herramientas para instalar paquetes y sus dependencias en un equipo de destino.    
    
Primero, realizará tareas para preparar la implementación. Creará un nuevo proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] y agregará paquetes y archivos de datos existentes al proyecto. No creará nuevos paquetes desde el principio; solamente trabajará con paquetes completados creados exclusivamente para este tutorial. En este tutorial no modificará la funcionalidad de los paquetes; no obstante, después de agregar los paquetes al proyecto, puede resultar útil abrirlos en el Diseñador de [!INCLUDE[ssIS](../includes/ssis-md.md)] y revisar el contenido de cada paquete. Mediante el examen de los paquetes, conocerá las dependencias de los paquetes como los archivos de registro y otras características interesantes de los mismos.    
    
Antes de llevar a cabo la implementación, también actualizará los paquetes para utilizar configuraciones. Las configuraciones permiten la actualización de las propiedades de los paquetes y los objetos de paquete en tiempo de ejecución. En este tutorial utilizará configuraciones para actualizar las cadenas de conexión de archivos de registro y de texto, y las ubicaciones de los archivos XML y XSD que usa el paquete. Para obtener más información, consulte [Configuraciones de paquetes](../integration-services/packages/package-configurations.md) y [Crear configuraciones de paquetes](../integration-services/packages/create-package-configurations.md).    
    
Después de comprobar que los paquetes funcionan correctamente en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], creará el paquete de implementación que se usará para instalar los paquetes. El paquete de implementación contendrá los archivos de paquete y otros elementos que ha agregado al proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , las dependencias del paquete que [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] incluye automáticamente y la utilidad de implementación que ha generado. Para más información, consulte [Create a Deployment Utility](../integration-services/packages/create-a-deployment-utility.md).    
    
A continuación, copiará el paquete de implementación en el equipo de destino y ejecutará el Asistente para la instalación de paquetes para instalar los paquetes y las dependencias de paquete. Los paquetes se instalarán en la base de datos msdb de SQL Server, y los archivos auxiliares y de ayuda se instalarán en el sistema de archivos. Puesto que los paquetes implementados utilizan configuraciones, actualizará la configuración para que use nuevos valores que permitirán que los paquetes se ejecuten correctamente en el nuevo entorno.    
    
Por último, ejecutará los paquetes en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] con la Utilidad de ejecución de paquetes.    
    
El objetivo de este tutorial es simular la complejidad de los problemas reales de implementación que puede encontrarse. No obstante, si no puede implementar los paquetes en otro equipo, puede seguir este tutorial instalando los paquetes en la base de datos msdb en una instancia local de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]y, a continuación, ejecutar los paquetes desde [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] en la misma instancia.    
    
## <a name="what-you-will-learn"></a>Aprendizaje    
La mejor forma de familiarizarse con las nuevas herramientas, los controles y las características disponibles en [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] es usándolas. Este tutorial le guía por los pasos para crear un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] y, a continuación, agregar los paquetes y otros archivos necesarios al proyecto. Después de completar el proyecto, creará un paquete de implementación, copiará el paquete al equipo de destino e instalará los paquetes en él.    
    
## <a name="requirements"></a>Requisitos    
Este tutorial está concebido para los usuarios familiarizados con las operaciones básicas del sistema de archivos, pero que no conocen con detalle las nuevas características disponibles en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]. Para comprender mejor los conceptos básicos de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que usará en este tutorial, puede resultarle útil completar primero el siguiente tutorial de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] : [Tutorial de SSIS: Crear un paquete ETL sencillo](../integration-services/ssis-how-to-create-an-etl-package.md).    
    
**Equipo de origen.** El equipo en el que creará el paquete de implementación **debe tener instalados los siguientes componentes:**
- SQL Server  
- Datos de ejemplo, paquetes completados, configuraciones y un archivo Léame. Estos archivos se instalan conjuntamente si descarga [Adventure Works 2014 Sample Databases](https://msftdbprodsamples.codeplex.com/releases/view/125550)(Bases de datos de ejemplo de Adventure Works 2014).     
> **Nota** asegúrese de que tiene permiso para crear y quitar tablas en AdventureWorks u otros datos que use.         
    
-   [SQL Server Data Tools (SSDT)](/sql-docs/docs/ssdt/download-sql-server-data-tools-ssdt).    
    
**Equipo de destino.** El equipo en el que implementará los paquetes **debe tener instalados los siguientes componentes:**    
    
- SQL Server
- Datos de ejemplo, paquetes completados, configuraciones y un archivo Léame. Estos archivos se instalan conjuntamente si descarga [Adventure Works 2014 Sample Databases](https://msftdbprodsamples.codeplex.com/releases/view/125550)(Bases de datos de ejemplo de Adventure Works 2014). 
    
- [SQL Server Management Studio](/sql-docs/docs/ssms/download-sql-server-management-studio-ssms).    
    
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].    
    
-   Debe tener permiso para crear y quitar tablas en AdventureWorks para y ejecutar paquetes en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].    
    
-   Debe tener permiso de lectura y de escritura para la tabla sysssispackages en la base de datos del sistema msdb de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .    
    
Si planea implementar paquetes en el mismo equipo en el que va a crear el paquete de implementación, ese equipo debe cumplir los requisitos de los equipos de origen y destino.    
    
**Tiempo estimado para completar este tutorial:** 2 horas    
    
## <a name="lessons-in-this-tutorial"></a>Lecciones de este tutorial    
[Lección 1: Preparar la creación del paquete de implementación](../integration-services/lesson-1-preparing-to-create-the-deployment-bundle.md)    
En esta lección, se preparará para implementar una solución ETL creando un nuevo proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] y agregando los paquetes y otros archivos necesarios al proyecto.    
    
[Lección 2: Crear el paquete de implementación en SSIS](../integration-services/lesson-2-create-the-deployment-bundle-in-ssis.md)    
En esta lección, generará una utilidad de implementación y comprobará que el paquete de implementación incluye los archivos necesarios.    
    
[Lección 3: Instalar los paquetes de SSIS](../integration-services/lesson-3-install-ssis-packages.md)    
En esta lección, copiará el paquete de implementación en el equipo de destino, instalará los paquetes y, a continuación, los ejecutará.    
    


