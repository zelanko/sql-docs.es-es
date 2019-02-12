---
title: Crear una suscripción controlada por datos (Tutorial de SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], tutorials
- walkthroughs [Reporting Services]
- data-driven subscriptions
ms.assetid: 79ab0572-43e9-4dc4-9b5a-cd8b627b8274
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: f4122aa579766d80cfac6600753d4a8f8a672ae9
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56017917"
---
# <a name="create-a-data-driven-subscription-ssrs-tutorial"></a>Crear una suscripción controlada por datos (Tutorial de SSRS)
  [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] proporciona suscripciones controladas por datos para que pueda personalizar la distribución de un informe basándose en datos dinámicos de suscriptores. Las suscripciones controladas por datos están destinadas a los escenarios siguientes:  
  
-   La distribución de informes a un grupo grande de destinatarios cuya pertenencia al grupo puede cambiar de una distribución a otra. Por ejemplo, la distribución de un informe mensual a todos los clientes actuales.  
  
-   La distribución de informes a un grupo específico de destinatarios basado en criterios predefinidos. Por ejemplo, el envío de un informe de rendimiento de ventas a los diez principales directores de ventas de la organización.  
  
## <a name="what-you-will-learn"></a>Aprendizaje  
 En este tutorial se muestra cómo utilizar suscripciones controladas por datos mediante un sencillo ejemplo que ilustra los conceptos.  
  
 El tutorial está compuesto por tres lecciones:  
  
 [Lección 1: Creación de una base de datos de suscriptor de ejemplo](lesson-1-creating-a-sample-subscriber-database.md)  
 En esta lección aprenderá a crear una base de datos local de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] con información de suscriptores.  
  
 [Lección 2: Modificar las propiedades del origen de datos de informe](lesson-2-modifying-the-report-data-source-properties.md)  
 En esta lección aprenderá a modificar propiedades del origen de datos de informe de manera que el informe pueda ejecutarse en modo desatendido. El procesamiento desatendido requiere las credenciales almacenadas. Además, modificará el conjunto de datos de informe para que incluya un parámetro proporcionado por los datos del suscriptor.  
  
 [Lección 3: Definir una suscripción controlada por datos](lesson-3-defining-a-data-driven-subscription.md)  
 En esta lección aprenderá a definir una suscripción controlada por datos. Esta lección le guía a través de cada página del Asistente para suscripciones controladas por datos.  
  
## <a name="requirements"></a>Requisitos  
 Normalmente, los administradores del servidor de informes se ocupan de crear y mantener las suscripciones controladas por datos. La posibilidad de crear suscripciones controladas por datos requiere tener conocimientos de creación de consultas, estar familiarizado con los orígenes de datos que contienen datos de suscriptores y tener permisos superiores en un servidor de informes.  
  
 El tutorial usará el informe creado en el tutorial [crear un informe de tabla básico &#40;Tutorial de SSRS&#41; ](create-a-basic-table-report-ssrs-tutorial.md) y los datos de [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)]  
  
 Para usar este tutorial, debe tener el software siguiente instalado en el sistema:  
  
-   Una edición de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que admita suscripciones controladas por datos. Para obtener más información, consulte [ediciones y componentes de SQL Server 2014](../sql-server/editions-and-components-of-sql-server-2016.md).  
  
-   El servidor de informes debe ejecutarse en modo nativo. La interfaz de usuario descrita en este tutorial se basa en un servidor de informes en modo nativo. Las suscripciones se admiten en los servidores de informes de modo de SharePoint pero la interfaz de usuario será diferente a la que se describe en este tutorial.  
  
-   Se debe ejecutar el servicio del Agente SQL Server.  
  
-   Un informe que contenga parámetros. En este tutorial, se supone que usa el informe de ejemplo `Sales Orders` que creó con el tutorial [Crear un informe de tabla básico &#40;Tutorial de SSRS&#41;](create-a-basic-table-report-ssrs-tutorial.md).  
  
-   La base de datos de ejemplo [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)], que proporciona datos para el informe de ejemplo.  
  
-   Una asignación de roles que incluye la tarea Administrar todas las suscripciones en el informe de ejemplo. Esta tarea es necesaria para definir una suscripción controlada por datos. Si es administrador del equipo, la asignación de roles predeterminada para los administradores locales le proporciona los permisos necesarios para crear suscripciones controladas por datos. Para obtener más información, consulte [Conceder permisos en un servidor de informes en modo nativo](security/granting-permissions-on-a-native-mode-report-server.md).  
  
-   Una carpeta compartida para la que tenga permisos de escritura. La carpeta compartida debe estar accesible a través de una conexión de red.  
  
 **Tiempo estimado para completar este tutorial:** 30 minutos. Otros 30 minutos si no ha completado el tutorial de informe básico.  
  
## <a name="see-also"></a>Vea también  
 [Data-Driven Subscriptions](subscriptions/data-driven-subscriptions.md)   
 [Crear un informe de tabla básico &#40;Tutorial de SSRS&#41;](create-a-basic-table-report-ssrs-tutorial.md)  
  
  
