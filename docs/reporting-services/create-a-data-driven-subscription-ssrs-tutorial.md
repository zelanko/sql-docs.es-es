---
title: Crear una suscripción controlada por datos (Tutorial de SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 05/26/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: reporting-services
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- subscriptions [Reporting Services], tutorials
- walkthroughs [Reporting Services]
- data-driven subscriptions
ms.assetid: 79ab0572-43e9-4dc4-9b5a-cd8b627b8274
caps.latest.revision: 50
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: da6c81701af24b495e84cb26dc3a6581d00ba1f6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="create-a-data-driven-subscription-ssrs-tutorial"></a>Crear una suscripción controlada por datos (Tutorial de SSRS)
En este tutorial de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] se explican los conceptos relacionados con las suscripciones controladas por datos mediante un ejemplo sencillo en el que se crea una suscripción controlada por datos para generar y guardar la salida de informe filtrado en un recurso compartido de archivos. 
[!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] Las suscripciones controladas por datos permiten personalizar y automatizar la distribución de un informe en función de datos dinámicos de suscriptores. Las suscripciones controladas por datos están destinadas a los escenarios siguientes:  
  
-   La distribución de informes a un grupo grande de destinatarios cuya pertenencia al grupo puede cambiar de una distribución a otra. Por ejemplo, enviar por correo electrónico un informe mensual a todos los clientes actuales.  
  
-   La distribución de informes a un grupo específico de destinatarios basado en criterios predefinidos. Por ejemplo, enviar un informe de rendimiento de ventas a todos los directores de ventas de una organización.
+ La automatización de la generación de informes en una amplia variedad de formatos, como .xlsx y .pdf.  
  
## <a name="what-you-will-learn"></a>Aprendizaje  
 El tutorial está compuesto por tres lecciones:  
 Lección | Comentarios
 ------- | --------------
 [Lección 1: Crear una base de datos de suscriptor de ejemplo](../reporting-services/lesson-1-creating-a-sample-subscriber-database.md) | En esta lección creará una base de datos local de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] de tablas que contiene la información del suscriptor, los números de pedido de información que se usan para el filtrado y los formatos de los archivos de salida.
[Lección 2: Modificar las propiedades del origen de datos de informe](../reporting-services/lesson-2-modifying-the-report-data-source-properties.md) |En esta lección, configurará un origen de datos de informe para que el informe pueda ejecutarse en modo desatendido según una programación. El procesamiento desatendido requiere las credenciales almacenadas. Además, modificará el conjunto de datos de informe para que incluya un parámetro proporcionado por los datos del suscriptor. Este parámetro se usa para filtrar los datos del informe en función del número de pedido.
 [Lección 3: Definir una suscripción controlada por datos](../reporting-services/lesson-3-defining-a-data-driven-subscription.md) | En esta lección, creará una suscripción controlada por datos. Esta lección le guía a través de cada página del Asistente para suscripciones controladas por datos.

 En el siguiente diagrama se muestra el flujo de trabajo básico del tutorial.

Paso  |Description 
---------|---------
(1)     |  La configuración de la suscripción toma nota del informe de origen, la programación y la asignación de campos en la base de datos de suscriptor.        
(2)     | La tabla OrderInfo contiene cuatro números de pedido que se usan para el filtrado, uno por archivo. La tabla también contiene los formatos de archivo de los informes generados.
(3)     | La información de la base de datos Adventureworks se filtra y se devuelve en el informe. 
(4)     | Los informes se crean en los formatos de archivo especificados en la tabla Orderinfo.

 
 
   ![ssrs_tutorial_datadriven_flow](../reporting-services/media/ssrs-tutorial-datadriven-flow.png) 
  
## <a name="requirements"></a>Requisitos  
Normalmente, los administradores del servidor de informes se ocupan de crear y mantener las suscripciones controladas por datos. Los pasos para crear suscripciones controladas por datos requieren crear consultas, estar familiarizado con los orígenes de datos que contienen datos de suscriptores y tener permisos elevados en un servidor de informes.  
  
En el tutorial se usan el informe *Pedido de venta* creado en el tutorial [Crear un informe de tabla básico &#40;Tutorial de SSRS&#41;](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md) y los datos de la base de datos de ejemplo **AdventureWorks2014**.  
  
Para utilizar este tutorial, debe tener el software siguiente instalado en el equipo:  
  
-   Una edición de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que admita suscripciones controladas por datos. Para obtener más información, vea [Ediciones y componentes de SQL Server 2016](../sql-server/editions-and-components-of-sql-server-2016.md).  
  
-   El servidor de informes debe ejecutarse en modo nativo. La interfaz de usuario descrita en este tutorial se basa en un servidor de informes en modo nativo. Las suscripciones se admiten en los servidores de informes de modo de SharePoint pero la interfaz de usuario será diferente a la que se describe en este tutorial.  
  
-   Se debe ejecutar el servicio del Agente SQL Server.  
  
-   Un informe que contenga parámetros. En este tutorial, se supone que usa el informe de ejemplo `Sales Orders` que creó con el tutorial [Crear un informe de tabla básico &#40;Tutorial de SSRS&#41;](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md).  
  
-   La base de datos de ejemplo **AdventureWorks2014** , que proporciona datos para el informe de ejemplo.  
  
-   Una asignación de roles de [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] que incluye la tarea Administrar todas las suscripciones en el informe de ejemplo. Esta tarea es necesaria para definir una suscripción controlada por datos. Si es administrador del equipo, la asignación de roles predeterminada para los administradores locales le proporciona los permisos necesarios para crear suscripciones controladas por datos. Para obtener más información, consulte [Conceder permisos en un servidor de informes en modo nativo](../reporting-services/security/granting-permissions-on-a-native-mode-report-server.md).  
  
-   Una carpeta compartida para la que tenga permisos de escritura. La carpeta compartida debe estar accesible a través de una conexión de red.  
  
**Tiempo estimado para completar este tutorial:** 30 minutos. Otros 30 minutos si no ha completado el tutorial de informe básico.  
  
## <a name="see-also"></a>Ver también  
[Suscripciones controladas por datos](../reporting-services/subscriptions/data-driven-subscriptions.md)  
[Crear un informe de tabla básico &#40;Tutorial de SSRS&#41;](../reporting-services/create-a-basic-table-report-ssrs-tutorial.md)
 

