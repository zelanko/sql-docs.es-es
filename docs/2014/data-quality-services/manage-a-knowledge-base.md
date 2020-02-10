---
title: Administrar una base de conocimiento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 27f306f4-d67c-47f5-b35c-4260cc5d36e3
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 552cd3a091699c42001ab42e64ff875760fe1e53
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "65484172"
---
# <a name="manage-a-knowledge-base"></a>Administrar una base de conocimiento
  En este tema se describe cómo realizar funciones de administración en una base de conocimiento de [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS). Puede eliminar una base de conocimiento, desbloquearla, descartar los cambios realizados en ella, cambiarle el nombre y mostrar sus propiedades.  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Prerequisites"></a> Requisitos previos  
 Para administrar una base de conocimiento, previamente esta debe haberse creado y estar publicada (si la ha creado otra persona) o cerrada (si la ha creado usted).  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Para abrir una base de conocimiento, debe disponer del rol dqs_kb_editor o dqs_administrator en la base de datos DQS_MAIN.  
  
##  <a name="Manage"></a>Administrar una base de conocimiento  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Ejecute la aplicación Data Quality Client](../../2014/data-quality-services/run-the-data-quality-client-application.md).  
  
2.  En la página de inicio de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , haga clic en **Abrir base de conocimiento**.  
  
3.  Haga clic con el botón secundario en una base de conocimiento de la tabla de bases de conocimiento.  
  
4.  En el menú contextual, puede hacer lo siguiente:  
  
    1.  **Abrir**: haga clic en esta opción para abrir la base de conocimiento en la actividad seleccionada en el panel **seleccionar actividad** .  
  
    2.  **Desbloquear**: puede desbloquear la base de conocimiento si es el usuario que estaba trabajando en la base de conocimiento en uno de los pasos de la actividad administración de dominios, detección de conocimiento y Directiva de coincidencia, y la cerró. Si desbloquea la base de conocimiento, otra persona podrá abrirla y trabajar con ella. Este comando no está disponible si la base de conocimiento no se encuentra en un estado de una actividad. Para obtener más información, vea [Open a Knowledge Base](../../2014/data-quality-services/open-a-knowledge-base.md).  
  
    3.  **Descartar trabajo**: haga clic en cuando la base de conocimiento se encuentra en un estado en el que se está trabajando, como se muestra con una entrada en el campo Estado de la tabla. Este comando no está disponible si la base de conocimiento no se encuentra en un estado de una actividad, ni tampoco si está bloqueada. Para obtener más información, vea [Open a Knowledge Base](../../2014/data-quality-services/open-a-knowledge-base.md).  
  
    4.  **Cambiar nombre**: haga clic para que el campo base de conocimiento de la tabla sea editable para la base de conocimiento en la que hizo clic con el botón secundario. Cambie el nombre y, a continuación, haga clic en esa base de conocimiento y haga clic de nuevo en el campo para aceptar el cambio de nombre.  
  
    5.  **Eliminar**: haga clic aquí para quitar la base de conocimiento de la [!INCLUDE[ssDQSServer](../includes/ssdqsserver-md.md)]base de datos DQS_MAIN en.  
  
    6.  **Propiedades**: haga clic aquí para mostrar las propiedades de la base de datos en una presentación de solo lectura.  
  
        1.  **Base de conocimiento de origen**: la base de conocimiento en la que se basó esta base de datos. Esto es opcional.  
  
        2.  **Estado**: indica si la base de conocimiento está **en el trabajo** y si está en una actividad específica de administración de conocimiento, tal y como se determinó cuando se cerró por última vez. El estado puede ser **Trabajando**, en el que la base de conocimiento se abre en una sesión de administración de conocimiento, pero no en una actividad específica, o **Trabajando** más una actividad de administración de conocimiento, en el que la base de conocimiento se abre en una sesión de administración de conocimiento y en una actividad específica.  
  
        3.  **Está bloqueada**: **true** si la base de conocimiento está bloqueada, **false** en caso contrario.  
  
        4.  **Contiene contenido sin publicar**: true si la base de conocimiento incluye contenido que no se ha guardado mediante la publicación, false en caso contrario.  
  
        5.  **Bloqueado por**: el nombre del usuario que cerró la base de conocimiento y lo bloquea.  
  
        6.  **Fecha de bloqueo**: fecha de bloqueo  
  
        7.  **Creado por**: el nombre del usuario que creó la base de conocimiento, con la red a la que pertenece.  
  
        8.  **Fecha de creación**: fecha de creación  
  
##  <a name="FollowUp"></a>Seguimiento: después de administrar una base de conocimiento  
 Después de administrar una base de conocimiento, el paso siguiente dependerá de la acción que haya realizado en ella:  
  
-   Si abrió la base de conocimiento, continuará en la actividad que seleccionó.  
  
-   Si la desbloqueó, otras personas podrán abrirla y trabajar en ella, en el estado indicado.  
  
-   Si descartó los cambios realizados en ella, la base de conocimiento estará disponible en el estado publicado por última vez.  
  
-   Si la cambió de nombre, tendrá que abrirla de nuevo para poder trabajar en ella.  
  
-   Si la eliminó, deberá seleccionar otra base de conocimiento en la que trabajar, o crear una nueva.  
  
  
