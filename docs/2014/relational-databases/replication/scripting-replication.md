---
title: Crear script para la replicación | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- scripts [SQL Server replication], replication objects
- merge replication scripting [SQL Server replication]
- replication [SQL Server], scripting
- snapshot replication [SQL Server], scripting
- scripts [SQL Server replication]
- transactional replication, scripting
ms.assetid: e50fac44-54c0-470c-a4ea-9c111fa4322b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 55407c52c5fb7bf0c9537eaf8fb7a7d31d2675e1
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63250517"
---
# <a name="scripting-replication"></a>Crear script para la replicación
  Todos los componentes de replicación de una topología deben convertirse en script como parte de un plan de recuperación de desastres y, además, los scripts también pueden utilizarse para automatizar tareas repetitivas. Un script  contiene los procedimientos almacenados del sistema Transact-SQL necesarios para implementar los componentes de replicación a los que se refieren los scripts, como una publicación o una suscripción. Los scripts se pueden crear en un asistente (como el Asistente para nueva publicación) o en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] después de crear un componente. Puede ver, modificar y ejecutar el script mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o **sqlcmd**. Los scripts se pueden almacenar con los archivos de copia de seguridad para utilizarlas en el caso de que se deba volver a configurar una topología de replicación.  
  
 Si se producen cambios en alguna propiedad, es necesario volver a generar el script de un componente. Si utiliza procedimientos almacenados personalizados con la replicación transaccional, debe guardar una copia de cada procedimiento con los scripts; la copia se debe actualizar si el procedimiento cambia (los procedimientos se actualizan normalmente como consecuencia de cambios de esquema o cambios en los requisitos de la aplicación. Para obtener más información sobre los procedimientos personalizados, vea [Especificar cómo se propagan los cambios para los artículos transaccionales](transactional/transactional-articles-specify-how-changes-are-propagated.md).  
  
 Para las publicaciones de combinación que utilizan filtros con parámetros, los scripts de publicación contienen las llamadas al procedimiento almacenado para crear particiones de datos. El script proporciona una referencia para las particiones creadas y una forma de volver a crear una o más divisiones en caso necesario.  
  
## <a name="example-of-automating-a-task-with-scripts"></a>Ejemplo de automatización de una tarea con scripts  
 En el ejemplo [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)]se implementa la replicación de mezcla para distribuir datos al personal de ventas que no trabaja en la oficina central. Un representante de ventas descarga todos los datos que pertenecen a los clientes de su zona utilizando suscripciones de extracción. Cuando trabaja sin conexión, el representante de ventas actualiza los datos e incluye clientes y pedidos nuevos. Como [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] dispone de más de 50 representantes de ventas en diferentes zonas, llevaría mucho tiempo crear las diferentes suscripciones necesarias en cada uno de los suscriptores con el Asistente para nuevas suscripciones. En su lugar, el administrador de la replicación puede seguir estos pasos:  
  
1.  Establezca las publicaciones de combinación necesarias con particiones basadas en el representante de ventas o en su zona.  
  
2.  Cree una suscripción de extracción para un suscriptor.  
  
3.  Genere un script basado en esa suscripción de extracción.  
  
4.  Modifique el script, cambiando valores como el nombre del suscriptor.  
  
5.  Ejecute el script en varios suscriptores para generar las suscripciones de extracción requeridas.  
  
## <a name="script-replication-objects"></a>Generar script de objetos de replicación  
 Genere script de objetos de replicación desde los asistentes de replicación o desde la carpeta **Replicación** de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Si genera script desde los asistentes, puede elegir crear objetos y generar script, o solo generar script.  
  
> [!IMPORTANT]  
>  Todas las contraseñas se generan como NULL. Cuando sea posible, pida a los usuarios que proporcionen credenciales de seguridad en tiempo de ejecución. Si almacena credenciales en un archivo de script, debe proteger el archivo para evitar el acceso no autorizado.  
  
 Para obtener más información sobre el uso de los asistentes de replicación, vea:  
  
-   [Configurar la publicación y la distribución](configure-publishing-and-distribution.md)  
  
-   [Create a Publication](publish/create-a-publication.md) (Creación de una publicación)  
  
-   [Create a Push Subscription](create-a-push-subscription.md) (Creación de una suscripción de inserción)  
  
-   [Crear una suscripción de extracción](create-a-pull-subscription.md)  
  
#### <a name="to-script-an-object-from-a-replication-wizard"></a>Para generar el script de un objeto desde un asistente de replicación  
  
1.  En la página **Acciones del asistente** de un asistente, active la casilla adecuada para el asistente:  
  
    -   **Generar un archivo de script con pasos para crear una publicación**  
  
    -   **Generar un archivo de script con pasos para crear las suscripciones**  
  
    -   **Generar un archivo de script con pasos para configurar la distribución**  
  
2.  En la página **Propiedades del archivo de script** especifique las opciones.  
  
3.  Finalice el asistente.  
  
#### <a name="to-script-an-object-from-management-studio"></a>Para generar script de un objeto en Management Studio  
  
1.  Conéctese al distribuidor, publicador o suscriptor en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]y, a continuación, expanda el nodo de servidor.  
  
2.  Expanda la carpeta **Replicación** y, a continuación, expanda la carpeta **Publicaciones locales** o **Suscripciones locales** .  
  
3.  Haga clic con el botón secundario en una publicación o suscripción y, a continuación, haga clic en **Generar scripts**.  
  
4.  Especifique las opciones en el cuadro de diálogo **Generar script SQL - \<ReplicationObject>** .  
  
5.  Haga clic en **Script a archivo**.  
  
6.  Escriba un nombre de archivo en el cuadro de diálogo **Ubicación del archivo de script** y, a continuación, haga clic en **Guardar**. Se muestra un mensaje de estado.  
  
7.  Haga clic en **Aceptar**y, a continuación, en **Cerrar**.  
  
#### <a name="to-script-multiple-objects-from-management-studio"></a>Para generar script de varios objetos desde Management Studio  
  
1.  Conéctese al distribuidor, publicador o suscriptor en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]y, a continuación, expanda el nodo de servidor.  
  
2.  Haga clic con el botón secundario en la carpeta **Replicación** y, a continuación, en **Generar scripts**.  
  
3.  Especifique las opciones en el cuadro de diálogo **Generar script SQL** .  
  
4.  Haga clic en **Script a archivo**.  
  
5.  Escriba un nombre de archivo en el cuadro de diálogo **Ubicación del archivo de script** y, a continuación, haga clic en **Guardar**. Se muestra un mensaje de estado.  
  
6.  Haga clic en **Aceptar** y, a continuación, en **Cerrar**.  
  
  
