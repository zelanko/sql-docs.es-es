---
title: Pantalla de inicio de Data Quality Client | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.clienthome.f1
ms.assetid: 7c6ec469-bc7d-4d19-8e21-11dcf8ade108
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 8d12e45d2f2b7ee3d3f06cf8820495e40cf9fbd3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "70154481"
---
# <a name="data-quality-client-home-screen"></a>Página de inicio del cliente de calidad de datos
  Utilice esta pantalla para obtener acceso a las interfaces de usuario de cada uno de los tres grupos principales de tareas de [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS): administración de bases de conocimiento, proyectos de calidad de datos y administración.  
  
## <a name="options"></a>Opciones  
  
### <a name="knowledge-base-management"></a>Administración de bases de conocimiento  
 Una base de conocimiento de DQS es un repositorio de metadatos que DQS utiliza para mejorar la calidad de los datos. Estos metadatos los crean tanto la plataforma DQS en un proceso de detección de conocimiento asistido por PC como el administrador de datos en un proceso interactivo de administración de dominios.  
  
 **Nueva base de conocimiento**  
 Inicie el proceso de crear una base de conocimiento desde el principio o basándose en los metadatos de una base de conocimiento existente. Este comando abre una página en la que puede identificar la base de conocimiento, basarla en una base de conocimiento existente, seleccionar la actividad que se desee de la base de conocimiento y, posteriormente, crear la base de conocimiento.  
  
 **Abrir base de conocimiento**  
 Abra una base de conocimiento de forma que pueda administrar sus dominios, llevar a cabo la detección del conocimiento o generar directivas de búsqueda de coincidencias. Si hace clic en el botón **Abrir base de conocimiento** , aparecerá la página de **Abrir base de conocimiento** que muestra una lista de las bases de conocimiento existentes con sus propiedades, estado actual, base de conocimiento y detalles de los dominios. Seleccione una base de conocimiento y ábrala desde **Abrir base de conocimiento**.  
  
 **Base de conocimiento reciente**  
 En la lista de la pantalla, abra una base de conocimiento que ya esté creada. Si no está bloquea, haga clic en la flecha derecha y seleccione la actividad en la que desea iniciar la base de conocimiento (administración de dominios, detección del conocimiento o directiva de búsqueda de coincidencias).  
  
 Puede abrir una base de conocimiento bloqueada y modificarla, únicamente si usted la bloqueó. Si es así, se abrirá la base de conocimiento en el estado en que se encontraba cuando se cerró, el cual se indica entre paréntesis. Si una base de conocimiento está bloqueada y no fue usted quien lo hizo, solo la podrá abrir en modo de solo lectura.  
  
### <a name="data-quality-projects"></a>Proyectos de calidad de datos  
 Un proyecto de calidad de datos es el proceso en el que DQS realiza la limpieza de datos o búsqueda de coincidencia de datos, tanto mediante la corrección de datos asistida por PC como mediante la limpieza interactiva de los datos.  
  
 **Nuevo proyecto de calidad de datos**  
 Inicie el proyecto de creación de un nuevo proyecto. Este comando abre una página en la que puede identificar el proyecto, asociarlo a una base de conocimiento, mostrar detalles de la base de conocimiento, seleccionar la actividad deseada para el proyecto y, posteriormente, crear el proyecto.  
  
 **Abrir un proyecto de calidad de datos**  
 Abra un proyecto de forma que pueda realizar la limpieza de datos o la búsqueda de coincidencia de datos. Si hace clic en el botón de **Abrir proyecto de calidad de datos** , aparecerá la página **Abrir proyecto de calidad de datos** que muestra una lista de los proyectos existentes con sus propiedades, estado actual, base de conocimiento y detalles de los dominios y reglas de la directiva de búsqueda de coincidencias. Seleccione un proyecto y ábralo desde **Abrir proyecto de calidad de datos**.  
  
 **Proyecto de calidad de datos reciente**  
 En la lista de la pantalla, seleccione un proyecto que ya se haya creado. Puede abrir un proyecto bloqueado solo si fue usted quien lo bloqueó. Si es así, se abrirá el proyecto en el estado en que se encontraba cuando se cerró, el cual se indica entre paréntesis. Si el proyecto estaba terminado, se abrirá en el paso de exportación de actividad.  
  
### <a name="administration"></a>Administración  
 La administración de DQS permite supervisar, configurar y mantener DQS.  
  
 **Supervisión de actividades**  
 Muestra una vista con el estado de todas las actividades (actuales y pasadas) relacionadas con el servidor [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]que está conectado. Los tipos de actividades supervisadas incluyen la administración del conocimiento, un proyecto de calidad de datos y la corrección de datos basada en SSIS.  
  
 **Configuración**  
 Muestra las propiedades de configuración de las cuentas de servicio de datos de referencia (a través de Azure Marketplace y directamente a los servicios de datos de referencia), la configuración general (limpieza interactiva, coincidencia y generación de perfiles) y la configuración de la gravedad del registro.  
  
## <a name="see-also"></a>Consulte también  
 [Bases de conocimiento y dominios de DQS](../../2014/data-quality-services/dqs-knowledge-bases-and-domains.md)   
 [Proyectos de calidad de datos &#40;DQS&#41;](../../2014/data-quality-services/data-quality-projects-dqs.md)   
 [dqs, administración](../../2014/data-quality-services/dqs-administration.md)  
  
  
