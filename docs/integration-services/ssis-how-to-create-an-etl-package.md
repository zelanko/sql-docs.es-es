---
title: 'Tutorial de SSIS: Crear un paquete ETL sencillo | Microsoft Docs'
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: SQL Server 2016
helpviewer_keywords:
- SSIS, tutorials
- packages [Integration Services], tutorials
- Integration Services, tutorials
- SQL Server Integration Services, tutorials
- logs [Integration Services], tutorials
- walkthroughs [Integration Services]
ms.assetid: d6d5bb1f-4cb1-4605-9cd6-f60b858382c4
caps.latest.revision: "38"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 1196fdf3fe4e37faa0da98a0cd44c3de3e0d46e7
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="ssis-how-to-create-an-etl-package"></a>Tutorial de SSIS: Crear un paquete ETL sencillo

 > Para obtener contenido relacionado con versiones anteriores de SQL Server, vea [Tutorial de SSIS: Crear un paquete ETL sencillo](https://msdn.microsoft.com/library/ms169917(SQL.120).aspx).

[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] (SSIS) es una plataforma que permite generar soluciones de integración de datos de alto rendimiento, entre las que se incluyen paquetes de extracción, transformación y carga de datos (ETL) para el almacenamiento de datos. SSIS incluye herramientas gráficas y asistentes para generar y depurar paquetes; tareas para realizar funciones de flujo de datos tales como operaciones de FTP; ejecución de instrucciones SQL y envío de mensajes de correo electrónico; orígenes y destinos de datos para extraer y cargar datos; transformaciones para limpiar, agregar, combinar y copiar datos; un servicio de administración, el servicio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] para administrar la ejecución y almacenamiento de paquetes; e interfaces de programación de aplicaciones (API) para programar el modelo de objetos de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
En este tutorial, aprenderá a usar el Diseñador de [!INCLUDE[ssIS](../includes/ssis-md.md)] para crear un paquete de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] sencillo. El paquete que cree toma los datos de un archivo plano, formatea de nuevo lo datos y luego inserta dichos datos en una tabla de hechos. En las lecciones siguientes, el paquete se expande para mostrar la creación de bucles, configuraciones de paquete, registro y flujo de errores.  
  
Al instalar los datos de ejemplo usados en el tutorial, también se instalan las versiones completadas de los paquetes que cree en cada lección del tutorial. Si utiliza los paquetes completados, puede saltarse lecciones y empezar el tutorial en una lección posterior si lo desea. Si este tutorial constituye la primera vez que trabaja con paquetes o el nuevo entorno de desarrollo, se recomienda empezar por la lección 1.  
  
## <a name="what-you-learn"></a>Lo que aprenderá  
La mejor forma de familiarizarse con las nuevas herramientas, los controles y las características disponibles en [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] es usándolas. En este tutorial se indican los pasos necesarios en el Diseñador de [!INCLUDE[ssIS](../includes/ssis-md.md)] para crear un paquete ETL sencillo que incluye bucles, configuraciones, lógica de flujo de errores y registro.  
  
## <a name="requirements"></a>Requisitos  
Este tutorial está concebido para los usuarios familiarizados con las operaciones básicas de una base de datos, pero que no conocen con detalle las nuevas características disponibles en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
Para utilizar este tutorial, el sistema debe tener instalados los siguientes componentes:  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con la base de datos **AdventureWorksDW2012** . Con el objeto de mejorar la seguridad, las bases de datos de ejemplo no se instalan de forma predeterminada. Para descargar la base de datos **AdventureWorksDW2012** , vea [Adventure Works para SQL Server 2012](http://go.microsoft.com/fwlink/?LinkId=275026).  
  
    > [!IMPORTANT]  
    > Cuando adjunte la base de datos (archivo \*.mdf), [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] busca un archivo .ldf de forma predeterminada. Quite manualmente el archivo .ldf antes de hacer clic en Aceptar en el cuadro de diálogo **Adjuntar bases de datos**.  
    >   
    > Para obtener más información acerca de cómo adjuntar bases de datos, vea [Attach a Database](../relational-databases/databases/attach-a-database.md).  
  
-   Datos de ejemplo. Los datos de ejemplo se incluyen con los paquetes de lecciones de [!INCLUDE[ssIS](../includes/ssis-md.md)] . Haga lo siguiente para descargar los datos de ejemplo y los paquetes de lecciones.  
  
    1.  Navegue a los [ejemplos del producto Integration Services](http://go.microsoft.com/fwlink/?LinkId=275027)  
  
    2.  Haga clic en la pestaña **DOWNLOADS** .  
  
    3.  Haga clic en el archivo SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip.  
  
## <a name="lessons-in-this-tutorial"></a>Lecciones de este tutorial  
[Lección 1: Crear un proyecto y un paquete básico con SSIS](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md)  
En esta lección, creará un paquete ETL sencillo que extrae datos de un único archivo plano, transforma los datos con transformaciones de búsqueda y, por último, carga los resultados en un destino de tabla de hechos.  
  
[Lección 2: Agregar bucles con SSIS](../integration-services/lesson-2-adding-looping-with-ssis.md)  
En esta lección, expandirá el paquete que ha creado en la lección 1 para beneficiarse de las nuevas características de bucles para extraer varios archivos planos en un único proceso de flujo de datos.  
  
[Lección 3: Agregar registro con SSIS](../integration-services/lesson-3-add-logging-with-ssis.md)  
En esta lección, expandirá el paquete que creó en la lección 2 para beneficiarse de las nuevas características de registro.  
  
[Lección 4: Agregar redirección de flujo de errores con SSIS](../integration-services/lesson-4-add-error-flow-redirection-with-ssis.md)  
En esta lección, expandirá el paquete que creó en la lección 3 para beneficiarse de las nuevas configuraciones de salida de error.  
  
[Lección 5: Agregar configuraciones de paquete para el modelo de implementación de paquetes](../integration-services/lesson-5-add-ssis-package-configurations-for-the-package-deployment-model.md)  
En esta lección, expandirá el paquete que creó en la lección 4 para beneficiarse de las nuevas opciones de configuración del paquete.  
  
[Lección 6: Uso de parámetros con el modelo de implementación de proyectos en SSIS](../integration-services/lesson-6-using-parameters-with-the-project-deployment-model-in-ssis.md)  
En esta lección, expandirá el paquete que creó en la lección 5 para beneficiarse del uso de los nuevos parámetros con el modelo de implementación del proyecto.  
  
  
  
