---
title: Proyectos de calidad de datos (DQS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: a43fc9c0-19b6-414a-8661-4c7c55e0c03e
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 8f4fbe5a3990348edc2e8b3716ca869c4166e145
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56043286"
---
# <a name="data-quality-projects-dqs"></a>Proyectos de calidad de datos (DQS)
  Un proyecto de calidad de datos de [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) utiliza una base de conocimiento para mejorar la calidad de los datos de origen mediante la realización de actividades de *limpieza de datos* y *búsqueda de coincidencias de datos* , y la posterior exportación de los datos resultantes a una base de datos de SQL Server o a un archivo .csv. Puede crear un proyecto de calidad de datos como un proyecto de limpieza o como un proyecto de búsqueda de coincidencias para realizar las actividades respectivas. Los proyectos de limpieza y de búsqueda de coincidencias se pueden ejecutar usando la misma base de conocimiento, ya que el conocimiento de estos procesos se puede generar en la misma base de conocimiento.  
  
 Un proyecto de calidad de datos tiene las ventajas siguientes:  
  
-   Permite realizar la limpieza de datos en los datos de origen utilizando el conocimiento de una base de conocimiento de DQS.  
  
-   Permite realizar la búsqueda de coincidencias de datos en los datos de origen utilizando la directiva de coincidencia de una base de conocimiento.  
  
-   Proporciona un asistente que le guiará durante las actividades de limpieza y búsqueda de coincidencias, y le permitirá exportar los datos al lugar de su elección: una base de datos de SQL Server o un archivo .csv. El administrador de datos puede utilizar el proyecto de calidad de datos para ejecutar y controlar los pasos de las actividades de limpieza (tanto la asistida por PC como la interactiva) y búsqueda de coincidencias.  
  
##  <a name="Cleansing"></a> Proyecto de calidad de datos: Actividad de limpieza  
 Un proyecto de calidad de datos de limpieza permite limpiar los datos de origen basándose en una base de conocimiento. La actividad de limpieza de datos de DQS es un proceso de dos pasos:  
  
1.  Un proceso de limpieza de datos *asistido por PC* que analiza los datos de origen comparándolos con el conocimiento de la base de conocimiento y propone cambios. DQS organiza los datos procesados por categorías (sugerido, nuevo, no válido, corregido y correcto) y los muestra al usuario para su procesamiento posterior.  
  
2.  Un proceso de limpieza *interactivo* que permite al administrador de datos aprobar, rechazar o modificar los datos propuestos por el proceso de limpieza de datos asistido por PC.  
  
 Para obtener información detallada acerca de la actividad de limpieza en un proyecto de calidad de datos, vea [Data Cleansing](../../2014/data-quality-services/data-cleansing.md).  
  
##  <a name="Matching"></a> Proyecto de calidad de datos: Actividad de coincidencia  
 Un proyecto de calidad de datos de búsqueda de coincidencias permite realizar la actividad de búsqueda de coincidencias basándose en la directiva de coincidencia de una base de conocimiento para evitar la duplicación de datos; para ello, se identifican las coincidencias exactas o aproximadas, lo que permite quitar los datos duplicados. Se recomienda limpiar los datos antes de ejecutar en ellos la actividad de búsqueda de coincidencias. Para ello:  
  
1.  Cree un proyecto de calidad de los datos, seleccione la actividad **Limpieza** , complete la actividad de limpieza de datos con los datos de origen y, a continuación expórtelos a una tabla de una base de datos de SQL Server.  
  
2.  Cree otro proyecto de calidad de datos utilizando una base de conocimiento que contenga una directiva de coincidencia, seleccione la actividad **Coincidencia** y, a continuación, en la página **Asignación** , seleccione la base de datos y la tabla donde exportó los datos que limpió en el paso 1.  
  
3.  Complete la actividad de búsqueda de coincidencias con los datos limpios.  
  
 Para obtener información detallada acerca de la actividad de búsqueda de coincidencias en un proyecto de calidad de datos, vea [Data Matching](../../2014/data-quality-services/data-matching.md).  
  
##  <a name="ProfilingNotification"></a> Generación de perfiles de datos y notificaciones  
 Mientras ejecuta las actividades de búsqueda de coincidencias y limpieza en un proyecto de calidad de datos, puede ver estadísticas e información en tiempo real de los datos que DQS está procesando. El proceso de generación de perfiles de datos le ayuda a evaluar la eficacia de los procesos de limpieza y búsqueda de coincidencias, y le permite determinar en qué medida le han ayudado estos procesos a mejorar la calidad de los datos. El proceso de generación de perfiles de DQS proporciona dos dimensiones de calidad de datos: *integridad* (la medida en que los datos están presentes) y *precisión* (la medida en que los datos se pueden utilizar para su uso previsto). Además, en función de la información de los perfiles de datos, el usuario verá notificaciones sobre las medidas que puede tomar para mejorar las operaciones de limpieza de datos y búsqueda de coincidencias de datos. Para obtener información detallada acerca de las notificaciones y la generación de perfiles de datos, vea [Data Profiling and Notifications in DQS](../../2014/data-quality-services/data-profiling-and-notifications-in-dqs.md).  
  
## <a name="related-tasks"></a>Related Tasks  
  
|Descripción de la tarea|Tema|  
|----------------------|-----------|  
|Describe cómo crear un proyecto de calidad de datos.|[Crear un proyecto de calidad de datos](../../2014/data-quality-services/create-a-data-quality-project.md)|  
|Describe cómo administrar (abrir, desbloquear, cambiar el nombre y eliminar) un proyecto de calidad de datos.|[Administrar &#40;abrir, desbloquear, cambiar el nombre y eliminar&#41; un proyecto de calidad de datos](../../2014/data-quality-services/manage-open-unlock-rename-and-delete-a-data-quality-project.md)|  
|Describe cómo abrir un proyecto de Integration Services en [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)].|[Abrir proyectos de Integration Services en Data Quality Client](../../2014/data-quality-services/open-integration-services-projects-in-data-quality-client.md)|  
  
## <a name="see-also"></a>Vea también  
 [Bases de conocimiento y dominios de DQS](../../2014/data-quality-services/dqs-knowledge-bases-and-domains.md)  
  
  
