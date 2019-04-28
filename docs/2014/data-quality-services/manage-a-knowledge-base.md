---
title: Administrar una base de conocimiento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 27f306f4-d67c-47f5-b35c-4260cc5d36e3
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: c787a9383bcec3c7d7614cc5823e6c9b4320cd2f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62792466"
---
# <a name="manage-a-knowledge-base"></a>Administrar una base de conocimiento
  En este tema se describe cómo realizar funciones de administración en una base de conocimiento de [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Puede eliminar una base de conocimiento, desbloquearla, descartar los cambios realizados en ella, cambiarle el nombre y mostrar sus propiedades.  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Prerequisites"></a> Requisitos previos  
 Para administrar una base de conocimiento, previamente esta debe haberse creado y estar publicada (si la ha creado otra persona) o cerrada (si la ha creado usted).  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Para abrir una base de conocimiento, debe disponer del rol dqs_kb_editor o dqs_administrator en la base de datos DQS_MAIN.  
  
##  <a name="Manage"></a> Administrar una base de conocimiento  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ejecute la aplicación Data Quality Client](../../2014/data-quality-services/run-the-data-quality-client-application.md).  
  
2.  En la página de inicio de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , haga clic en **Abrir base de conocimiento**.  
  
3.  Haga clic con el botón secundario en una base de conocimiento de la tabla de bases de conocimiento.  
  
4.  En el menú contextual, puede hacer lo siguiente:  
  
    1.  **Abrir**: Haga clic aquí para abrir la base de conocimiento de la actividad seleccionada en el panel **Seleccione la actividad**.  
  
    2.  **Desbloquear**: Puede desbloquear la base de conocimiento si es el usuario que estaba trabajando en la base de conocimiento en uno de los pasos de administración de dominios, detección de conocimiento y la actividad de directiva de coincidencia y lo ha cerrado. Si desbloquea la base de conocimiento, otra persona podrá abrirla y trabajar con ella. Este comando no está disponible si la base de conocimiento no se encuentra en un estado de una actividad. Para obtener más información, vea [Open a Knowledge Base](../../2014/data-quality-services/open-a-knowledge-base.md).  
  
    3.  **Descartar trabajo**: Haga clic aquí si la base de conocimiento en un estado de la que se está trabajando, tal como se muestra con una entrada en el campo estado de la tabla. Este comando no está disponible si la base de conocimiento no se encuentra en un estado de una actividad, ni tampoco si está bloqueada. Para obtener más información, vea [Open a Knowledge Base](../../2014/data-quality-services/open-a-knowledge-base.md).  
  
    4.  **Cambiar nombre**: Haga clic para editar la base de conocimiento que se hecho en el campo de Base de conocimiento de la tabla. Cambie el nombre y, a continuación, haga clic en esa base de conocimiento y haga clic de nuevo en el campo para aceptar el cambio de nombre.  
  
    5.  **Eliminar**: Haga clic para quitar la base de conocimiento de la base de datos DQS_MAIN de [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)].  
  
    6.  **Propiedades**: Haga clic para mostrar las propiedades de la base de datos en una presentación de solo lectura.  
  
        1.  **Base de conocimiento de origen**: la base de conocimiento en la que está basada esta base de datos. Esto es opcional.  
  
        2.  **Estado**: Indica si la base de conocimiento se encuentra en el estado **Trabajando** y si está en una actividad específica de administración de conocimiento, según se determinó cuando se cerró por última vez. El estado puede ser **Trabajando**, en el que la base de conocimiento se abre en una sesión de administración de conocimiento, pero no en una actividad específica, o **Trabajando** más una actividad de administración de conocimiento, en el que la base de conocimiento se abre en una sesión de administración de conocimiento y en una actividad específica.  
  
        3.  **Está bloqueado**: **True** si la base de conocimiento está bloqueada, **False** en caso contrario.  
  
        4.  **Incluye contenido sin publicar**: True si la base de conocimiento incluye contenido que no se ha guardado mediante la publicación, False en caso contrario  
  
        5.  **Bloqueada por**: el nombre del usuario que cerró la base de conocimiento, bloqueándola.  
  
        6.  **Fecha de bloqueo**: la fecha en la que se bloqueó.  
  
        7.  **Creada por**: el nombre del usuario que creó la base de conocimiento, junto con la red a la que pertenece el usuario.  
  
        8.  **Fecha de creación**: la fecha en la que se creó.  
  
##  <a name="FollowUp"></a> Seguimiento: Después de administrar una Base de conocimiento  
 Después de administrar una base de conocimiento, el paso siguiente dependerá de la acción que haya realizado en ella:  
  
-   Si abrió la base de conocimiento, continuará en la actividad que seleccionó.  
  
-   Si la desbloqueó, otras personas podrán abrirla y trabajar en ella, en el estado indicado.  
  
-   Si descartó los cambios realizados en ella, la base de conocimiento estará disponible en el estado publicado por última vez.  
  
-   Si la cambió de nombre, tendrá que abrirla de nuevo para poder trabajar en ella.  
  
-   Si la eliminó, deberá seleccionar otra base de conocimiento en la que trabajar, o crear una nueva.  
  
  
