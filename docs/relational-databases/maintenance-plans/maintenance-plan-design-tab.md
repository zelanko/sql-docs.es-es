---
title: Plan de mantenimiento (pestaña Diseño) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql13.swb.maint.maintplanproperties.optimizations.f1
- sql13.swb.maint.planeditor.f1
- sql13.swb.maint.subplaneditor.f1
ms.assetid: 6d20d4d4-5b3f-454a-8a05-f0aac803c5ad
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: e10313d27d7760d05ed79e1fa5d5cd1944009778
ms.sourcegitcommit: 6c9d35d03c1c349bc82b9ed0878041d976b703c6
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/06/2018
ms.locfileid: "51215963"
---
# <a name="maintenance-plan-design-tab"></a>Plan de mantenimiento (pestaña Diseño)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Use el **Plan de mantenimiento (pestaña Diseño)** para especificar las propiedades de un plan de mantenimiento y sus subplanes. Arrastre las tareas del cuadro de herramientas al diseñador de planes. Haga clic con el botón secundario en grupos de tareas para crear rutas de ejecución bifurcadas. Los planes de mantenimiento se guardan como paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que se ejecutan mediante trabajos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="options"></a>Opciones  
 **Agregar subplán**  
 Agrega un subplán que puede configurar.  
  
 **Propiedades del subplán**  
 Muestra el cuadro de diálogo **Propiedades del subplan** . Seleccione un subplán en la cuadrícula y haga clic en este icono para escribir un nombre, descripción y programación para el subplán. También puede hacer doble clic en el subplan en la cuadrícula para mostrar el cuadro de diálogo **Propiedades del subplan** . Los nombres de subplán tienen un límite de 128 caracteres y las descripciones de 512 caracteres.  
  
 **Eliminar subplán seleccionado**  
 Elimina el subplán seleccionado.  
  
 **Programación del subplán**  
 Muestra el cuadro de diálogo **Propiedades de programación del trabajo** . Seleccione un subplán en la cuadrícula y haga clic en este icono para configurar una programación para el subplán.  
  
 **Quitar programación**  
 Quita una programación del subplán seleccionado.  
  
 **Administrar conexiones**  
 Muestra el cuadro de diálogo **Administrar conexiones** . Se utiliza para agregar conexiones adicionales de instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al plan de mantenimiento. Las tareas de mantenimiento del editor de subplanes pueden usar cualquiera de estas conexiones. Cuando se ejecuta, el plan de mantenimiento establece una conexión, desde el servidor del plan de mantenimiento, con los servidores [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especificados, mediante el uso de credenciales de conexión.  
  
 **Informes y registro**  
 Muestra el cuadro de diálogo **Informes y registro** , que se usa para administrar informes relacionados con la actividad del plan de mantenimiento y para configurar el registro en el servidor local o remoto.  
  
 **Servidores**  
 Muestra el cuadro de diálogo **Servidores** , que se usa para seleccionar los servidores en los que se ejecutarán las tareas del subplan. Esta opción está habilitada solo en servidores maestros en entornos multiservidor. Para obtener más información, vea [Crear un entorno multiservidor](../../ssms/agent/create-a-multiserver-environment.md).  
  
 **Nombre**  
 Muestra el nombre del plan de mantenimiento. En los nuevos planes de mantenimiento, el nombre se especifica en un cuadro de diálogo antes de que se abra el diseñador de planes de mantenimiento. Para cambiar el nombre de un plan de mantenimiento, haga clic con el botón derecho en el plan en el Explorador de objetos y, luego, haga clic en **Cambiar nombre**.  
  
 **Descripción**  
 Vea o especifique una descripción para el plan de mantenimiento. La longitud máxima de una descripción es de 512 caracteres.  
  
 **Superficie del diseñador**  
 Diseña y mantiene los planes de mantenimiento. Utilice la superficie del diseñador para agregar o eliminar tareas de mantenimiento a un plan, especificar los vínculos de precedencia entre las tareas e indicar la bifurcación y el paralelismo de tareas.  
  
 Un vínculo de precedencia entre dos tareas establece una relación entre ellas. La segunda tarea (la *tarea dependiente*) solo se ejecuta si el resultado de la ejecución de la primera tarea (la *tarea precedente*) coincide con el criterio especificado. Por lo general, el resultado de la ejecución es **Correcto**, **Error**o **Conclusión**. La superficie del diseñador del plan de mantenimiento se basa en la superficie del diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] . Para obtener más información, vea [Restricciones de precedencia](../../integration-services/control-flow/precedence-constraints.md).  
  
 Como ejemplo, un tarea Desfragmentar índice puede especificarse para que solo se ejecute si ha finalizado correctamente una tarea Comprobar la integridad de la base de datos. La característica de vinculación de precedencia de la tarea también permite que el plan pueda hacer frente a condiciones de error. Por ejemplo, si la tarea Comprobar la integridad de la base de datos genera errores, una tarea Notificar al operador podría informar a un usuario u operador sobre la existencia del error.  
  
 Especificar las tareas que se van a ejecutar después del error de una tarea predecesora es un ejemplo de *bifurcación de tareas*.  
  
 Indicar que dos o más tareas empiezan simultáneamente, por ejemplo, después de la finalización correcta de una tarea predecesora, es un ejemplo de especificación de *paralelismo de tareas*. Todas las tareas sin restricciones se iniciarán y se ejecutarán en paralelo. Use restricciones para retrasar tareas y así las primeras tareas terminarán antes.  
  
 Después de que una tarea de mantenimiento se coloque en la superficie de diseño, sus propiedades pueden editarse cuando sea necesario. Por ejemplo, la base de datos específica de la que se va a hacer copia de seguridad en una tarea Copia de seguridad de la base de datos se especifica después de que la tarea se haya agregado al plan. Las tareas de la superficie de diseño que no se han configurado correctamente contienen un icono rojo con una x blanca.  
  
 Para agregar una tarea de mantenimiento a un plan, arrastre el icono de la tarea desde el cuadro de herramientas **Tareas de plan de mantenimiento** hasta la superficie de diseño del plan o haga doble clic en la tarea en el cuadro de herramientas, con lo que se agrega esa tarea a la superficie del diseñador activa en ese momento. Si el cuadro de herramientas **Tareas del plan de mantenimiento** no está visible, elija **Cuadro de herramientas** en el menú [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] **de** . Expanda el nodo **Tareas del plan de mantenimiento** en el panel **Cuadro de herramientas** .  
  
 Para eliminar una tarea de un plan, seleccione la tarea en la superficie del diseñador y pulse la tecla **SUPR** o haga clic con el botón derecho en la tarea y luego haga clic en **Eliminar**.  
  
 Para especificar los vínculos de precedencia entre dos tareas, arrastre primero las tareas a la superficie de diseño y, a continuación, haga clic en la tarea que tiene lugar en primer lugar (la tarea precedente) y arrastre la flecha a la tarea dependiente. Cuando se ha establecido un vínculo de precedencia, el diseñador muestra una flecha de vinculación entre las dos tareas; la tarea precedente apunta a la tarea dependiente. De forma predeterminada, cuando un vínculo se establece por primera vez, la restricción del vínculo se establece de modo que la tarea dependiente solo se ejecuta si el resultado de la ejecución de la tarea precedente es **Correcto**.  
  
 Para cambiar las propiedades de un vínculo de precedencia, haga doble clic en el vínculo para iniciar el **Editor de restricciones de precedencia**. Este editor ofrece muchas opciones para especificar las condiciones lógicas que determinan si la tarea dependiente se ejecuta. Por ejemplo, el **resultado de la ejecución** puede establecerse en **Error**, en cuyo caso la tarea dependiente solo se ejecuta si la tarea precedente genera un error. Para cambiar la propiedad del resultado de la ejecución de un vínculo a **Correcto**, **Error**o **Conclusión**, también puede hacer clic con el botón derecho en el vínculo y luego seleccionar la opción deseada en el menú contextual.  
  
 Para especificar la bifurcación de tareas, cree primero los vínculos de precedencia entre dos tareas. Luego, coloque otra tarea dependiente en la superficie de diseño que se ejecute si se obtiene un resultado diferente a la primera tarea dependiente. Haga clic en la tarea predecesora y arrastre la segunda flecha de la tarea precedente a la tarea dependiente. Para cambiar el resultado de la ejecución (**Correcto**, **Error**, **Conclusión**) que hace que una tarea dependiente se ejecute, haga doble clic en la flecha de vínculo y modifique el campo **Resultado de ejecución** . Como alternativa, haga clic con el botón secundario en el vínculo y seleccione el valor deseado del resultado de la ejecución en el menú contextual.  
  
 Para especificar el paralelismo de la tarea, vincule dos o más tareas dependientes a una sola tarea precedente. Modifique las propiedades de los vínculos de precedencia, de forma que los vínculos que apuntan a las tareas dependientes que se ejecutan en paralelo tengan el mismo valor en los campos del resultado de la ejecución.  
  
## <a name="additional-features-available-from-the-shortcut-menu"></a>Características adicionales disponibles en el menú contextual  
 Para ver las opciones adicionales, seleccione una o más tareas en la superficie de diseño y, a continuación, haga clic con el botón secundario para abrir el menú contextual. Además de las opciones típicas **Cortar**, **Copiar**, **Pegar**, **Eliminar**y **Seleccionar todo**, están disponibles las siguientes opciones especiales para algunas tareas.  
  
 **Agregar anotación**  
 Agrega una nota descriptiva al área de diseño.  
  
 **Editar**  
 Abre el cuadro de diálogo de propiedades de la tarea.  
  
 **Deshabilitar**  
 De esta manera, la tarea no está disponible temporalmente.  
  
 **Habilitar**  
 Restaura una tarea deshabilitada.  
  
 **Grupo**  
 Crea un grupo que contiene una o más tareas.  
  
 **Desagrupar**  
 Quita tareas de un grupo.  
  
 **Ajustar tamaño automáticamente**  
 Establece el tamaño óptimo de cada tarea.  
  
 **Contraer**  
 Oculta las tareas de un grupo.  
  
 **Expandir**  
 Muestra las tareas de un grupo que se habían ocultado mediante **Contraer**.  
  
 **Zoom**  
 Cambia el tamaño de las tareas en el área de diseño.  
  
## <a name="see-also"></a>Ver también  
 [Planes de mantenimiento](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [Crear un plan de mantenimiento](../../relational-databases/maintenance-plans/create-a-maintenance-plan.md)  
  
  
