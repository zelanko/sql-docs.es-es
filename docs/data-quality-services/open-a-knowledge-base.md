---
title: Abrir una base de conocimiento
ms.date: 06/04/2013
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql13.dqs.kb.openkb.f1
ms.assetid: a5f010a5-b762-41c9-881b-bf0c192dca83
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 91f5e7effe54b9955537d90d639a820b5428a5c3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "75246011"
---
# <a name="open-a-knowledge-base"></a>Abrir una base de conocimiento

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  En este tema se describe cómo abrir una base de conocimiento existente en [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) y cómo prepararla para la administración de dominios, la detección de conocimiento o la adición de una directiva de coincidencia.  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> Requisitos previos  
 Para abrir una base de conocimiento, previamente esta debe haberse creado y estar publicada (si la ha creado otra persona) o cerrada (si la ha creado usted).  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permisos  
 Para abrir una base de conocimiento, debe disponer del rol dqs_kb_editor o dqs_administrator en la base de datos DQS_MAIN.  
  
##  <a name="open-a-knowledge-base"></a><a name="Open"></a>Abrir una base de conocimiento  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)][Ejecute la aplicación Data Quality Client](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  En la página de inicio de [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , haga clic en **Abrir base de conocimiento**.  
  
3.  Seleccione una base de conocimiento en la tabla. Los dominios y las reglas de coincidencia de la base de conocimiento se mostrarán en el panel derecho de la página.  
  
    > [!NOTE]  
    >  Para realizar operaciones en una base de conocimiento, haga clic en ella con el botón secundario dentro de la tabla. Puede abrir la base de conocimiento, guardarla con otro nombre, desbloquearla, descartar los cambios realizados, cambiar su nombre o mostrar sus propiedades.  
  
4.  En **Seleccione la actividad**, seleccione la actividad que desea realizar en la base de conocimiento:  
  
    -   Seleccione **Administración de dominios** para tener acceso a las pantallas que se utilizan para modificar los dominios de la base de conocimiento.  
  
    -   Seleccione **Detección de conocimiento** para iniciar el asistente que se usa para analizar una muestra de datos y rellenar los dominios de la base de conocimiento con los resultados.  
  
    -   Seleccione **Directiva de coincidencia** para crear una directiva de coincidencia y agregarla a la base de conocimiento.  
  
5.  Haga clic en **Abrir**.  
  
    > [!NOTE]  
    >  Para abrir la base de conocimiento, también puede hacer clic en ella con el botón secundario y seleccionar Abrir. Otros comandos del menú contextual permiten guardarla con otro nombre, desbloquearla, descartar los cambios realizados, cambiar su nombre o mostrar sus propiedades.  
  
    > [!NOTE]  
    >  Si no puede abrir la base de conocimiento porque está bloqueada, vea la sección siguiente.  
  
## <a name="open-a-recent-knowledge-base"></a>Abrir una base de conocimiento reciente  
 En la lista **Base de conocimiento reciente** de la página de inicio de DQS se muestran las cinco últimas bases de conocimiento que se han abierto. Esto le da la posibilidad de abrir una base de conocimiento en la que ha trabajado recientemente sin necesidad de pasar por la página **Abrir base de conocimiento** .  
  
-   Para abrir una base de conocimiento de la lista que no esté bloqueada, haga clic en la flecha derecha de la base de conocimiento y seleccione la actividad que desea abrir.  
  
-   Para abrir una base de conocimiento de la lista que ha bloqueado usted, haga clic en ella; la base de conocimiento se abrirá en la actividad y en la página indicadas entre paréntesis.  
  
-   Para abrir una base de conocimiento de la lista que ha bloqueado otra persona, póngase en contacto con dicha persona y pídale que la desbloquee.  
  
##  <a name="follow-up-after-opening-a-knowledge-base"></a><a name="FollowUp"></a>Seguimiento: después de abrir una base de conocimiento  
 Después de abrir una base de conocimiento, esta adquiere el estado indicado en la columna Estado de la tabla de bases de conocimiento. Para las actividades de detección de conocimiento y directiva de coincidencia, la base de conocimiento se abre en una página específica del asistente. Para la actividad de administración de dominios, la base de conocimiento se abre en la página Administración de dominios. Para más información sobre los estados, vea [Realizar la detección de conocimiento](../data-quality-services/perform-knowledge-discovery.md), [Administrar un dominio](../data-quality-services/managing-a-domain.md) o [Crear una directiva de coincidencia](../data-quality-services/create-a-matching-policy.md).  
  
##  <a name="if-the-knowledge-base-is-locked"></a><a name="Locked"></a>Si la base de conocimiento está bloqueada  
 El icono de candado en la primera columna indica si la base de conocimiento está bloqueada. Cuando una base de conocimiento está bloqueada, su nombre aparece en color rojo. Si un usuario específico está modificando una base de conocimiento a través de una actividad, la base de conocimiento se marca como bloqueada. En una base de conocimiento bloqueada no puede trabajar un segundo usuario. Si el usuario que está trabajando en la base de conocimiento desea desbloquearla, solo tiene que hacer clic en ella con el botón secundario dentro de la tabla de la página Abrir base de conocimiento y, a continuación, seleccionar **Desbloquear**, o bien, publicarla. Cuando el cursor se sitúa en una base de conocimiento bloqueada, DQS muestra una sugerencia que indica quién la bloqueó y cuándo lo hizo.  
  
##  <a name="state-of-a-knowledge-base"></a><a name="State"></a>Estado de una base de conocimiento  
 El campo Estado indica en qué fase de una actividad se encuentra la base de conocimiento. Si abre la base de conocimiento, se abrirá en esa fase.  
  
-   >vacío: el campo Estado está vacío para una base de conocimiento si la base de conocimiento se ha publicado haciendo clic en **publicar** en la actividad administración de dominios y en **sí: publicar la base de conocimiento y salir**. ** \< **  
  
-   **En el trabajo**: el trabajo de la base de conocimiento se ha guardado haciendo clic en **publicar** en la actividad administración de dominios y haciendo clic en **no-guardar el trabajo en la base de conocimiento y salir**.  
  
-   **Administración de dominios**: se han especificado datos para un dominio de la base de conocimiento, pero esta no se ha publicado y el trabajo permanece en la actividad Administración de dominios. La actividad Detección de conocimiento no está disponible. Esto sucede si se hace clic en **Cerrar** en la pantalla **Administración de dominios** .  
  
-   **Detección de conocimiento: asignar**: la base de conocimiento se cerró en la página **Administración de la base de conocimiento: Asignación** . La base de conocimiento está bloqueada y las actividades de administración de dominios y búsqueda de coincidencias no están disponibles.  
  
-   **Detección de conocimiento: detectar**: la base de conocimiento se cerró en la página **Administración de la base de conocimiento: Detectar** . La base de conocimiento está bloqueada y la actividad Administración de dominios no está disponible.  
  
-   **Administración de valores de detección**: la base de conocimiento se cerró en la página Administración de la **base de conocimiento: administrar términos del dominio** . La base de conocimiento está bloqueada y la actividad Administración de dominios no está disponible.  
  
-   Directiva de coincidencia: directiva **de**coincidencia: la base de conocimiento se cerró en la página Directiva de coincidencia **de directivas de** coincidencia. La base de conocimiento está bloqueada y las actividades de detección de conocimiento y administración de dominios no están disponibles.  
  
-   **Coincidencia de la Directiva: resultados de coincidencia**: la base de conocimiento se cerró en la página **de resultados de búsqueda de coincidencias de la Directiva de coincidencia** . La base de conocimiento está bloqueada y las actividades de detección de conocimiento y administración de dominios no están disponibles.  
  
  
