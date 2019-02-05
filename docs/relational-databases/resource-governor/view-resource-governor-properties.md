---
title: Ver las propiedades del regulador de recursos | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
f1_keywords:
- sql13.swb.rg.properties.f1
helpviewer_keywords:
- Resource Governor, properties
ms.assetid: de3510df-f792-4a9d-80fa-f198fd36cdc8
author: julieMSFT
ms.author: jrasnick
manager: craigg
ms.openlocfilehash: ed9959bf001855e869262c9f91f2821bf7c59744
ms.sourcegitcommit: cebfa2610ea36e3c5ad510c214590035ecb499c2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/04/2019
ms.locfileid: "55689908"
---
# <a name="view-resource-governor-properties"></a>Ver las propiedades del regulador de recursos
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Puede crear o configurar entidades del regulador de recursos, por ejemplo grupos de recursos de servidor y grupos de cargas de trabajo, utilizando la página Propiedades del regulador de recursos de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 ##  <a name="BeforeYouBegin"></a> Temas relacionados 
 Además de ver las propiedades de las entidades del regulador de recursos, puede realizar varias tareas de configuración mediante la página **Propiedades del regulador de recursos** . Para obtener más información, vea estos temas:  
  
-   [Habilitar el regulador de recursos](../../relational-databases/resource-governor/enable-resource-governor.md)  
  
-   [Deshabilitar el regulador de recursos](../../relational-databases/resource-governor/disable-resource-governor.md)  
  
-   [Crear un grupo de recursos de servidor](../../relational-databases/resource-governor/create-a-resource-pool.md)  
  
-   [Crear un grupo de cargas de trabajo](../../relational-databases/resource-governor/create-a-workload-group.md)  
  
-   [Cambiar la configuración del grupo de recursos de servidor](../../relational-databases/resource-governor/change-resource-pool-settings.md)  
  
-   [Cambiar la configuración del grupo de cargas de trabajo](../../relational-databases/resource-governor/change-workload-group-settings.md)  
  
-   [Mover un grupo de cargas de trabajo](../../relational-databases/resource-governor/move-a-workload-group.md)  
  
 Cuando haga clic en **Aceptar** después de agregar, eliminar o mover un grupo de cargas de trabajo o un grupo de recursos de servidor, se ejecuta la instrucción ALTER RESOURCE GOVERNOR RECONFIGURE.  
  
 Si la operación de creación o cambio de configuración sobre el grupo de recursos de servidor o el grupo de cargas de trabajo produce un error, aparecerá un informe de error debajo del título de la página de propiedades. Para ver un mensaje de error más detallado, haga clic en la flecha abajo que aparece en el mensaje de error.  
  
 Es posible determinar si existe una configuración pendiente consultando la vista de administración dinámica [sys.dm_resource_governor_configuration](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-configuration-transact-sql.md) para obtener el estado actual de is_configuration_pending.  
  
##  <a name="Permissions"></a> Permissions  
 Para ver las propiedades del regulador de recursos se requiere el permiso VIEW SERVER STATER. Las tareas de configuración del regulador de recursos requieren el permiso CONTROL SERVER.  
  
##  <a name="ViewRGProp"></a> Página Propiedades del regulador de recursos  
 **Para ver las propiedades del regulador de recursos con la página Propiedades del regulador de recursos en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], abra el Explorador de objetos y expanda de forma recursiva el nodo **Administración** hasta el nodo **Regulador de recursos**.  
  
2.  Haga clic con el botón derecho en **Regulador de recursos** y, luego, haga clic en **Propiedades**. De este modo se abre la página **Propiedades del regulador de recursos** .  
  
3.  Para las obtener descripciones de los campos de la página, vea [Propiedades del regulador de recursos](#RGProp).  
  
4.  Para guardar los cambios, haga clic en **Aceptar**.  
  
##  <a name="RGProp"></a> Resource Governor properties  
 **Nombre de la función de clasificador**  
 Especifique la función clasificadora seleccionándola en la lista.  
  
 **Habilitar el regulador de recursos**  
 Habilite o deshabilite el regulador de recursos seleccionando o desactivando la casilla.  
  
 **Grupos de recursos de servidor**  
 Cree o cambie la configuración del grupo de recursos y del grupo de recursos externos con la cuadrícula que se proporciona. Esta cuadrícula se rellena con información acerca de los grupos internos y predeterminados predefinidos. Seleccione un grupo con el que trabajar haciendo clic en la primera columna de la fila para el grupo de recursos. Para crear un grupo de recursos, haga clic en la fila que viene precedida por un asterisco (**&#42;**).  
  
 **Nombre**  
 Especifique el nombre del grupo de recursos de servidor.  
  
 **% de tiempo mínimo de CPU**  
 Especifique el ancho banda de la CPU promedio garantizado para todas las solicitudes en el grupo de recursos de servidor cuando hay contención de CPU. El rango es de 0 a 100.  
  
 **% de tiempo máximo de CPU**  
 Especifique el promedio máximo de ancho banda de CPU que recibirán todas las solicitudes en este grupo de recursos de servidor cuando hay contención de CPU. El rango es de 0 a 100. El valor predeterminado es 100.  
  
 **% mínimo de memoria**  
 Especifique la cantidad mínima de memoria reservada para este grupo de recursos de servidor que no se puede compartir con otros grupos de recursos de servidor. El rango es de 0 a 100.  
  
 **% máximo de memoria**  
 Especifique la memoria total del servidor que puede ser utilizada por las solicitudes en este grupo de recursos de servidor. El rango es de 0 a 100. El valor predeterminado es 100.  
  
 Para obtener más información, vea [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md) y [CREATE EXTERNAL RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-resource-pool-transact-sql.md).  
  
 **Grupos de cargas de trabajo de grupo de recursos de servidor**  
 Cree o cambie la configuración del grupo de cargas de trabajo utilizando la cuadrícula que se proporciona. Esta cuadrícula se rellena con información acerca de los grupos internos y predeterminados predefinidos. Seleccione un grupo con el que trabajar haciendo clic en la primera columna de la fila para el grupo de recursos. Para crear un grupo de cargas de trabajo, haga clic en la fila que viene precedida por un asterisco (**&#42;**).  
  
 **Nombre**  
 Especifique el nombre del grupo de cargas de trabajo  
  
 **Importancia**  
 Especifique la importancia relativa de una solicitud en el grupo de cargas de trabajo. Las opciones disponibles son Baja, Media, y Alta.  
  
 **Solicitudes máximas**  
 Especifique el número máximo de solicitudes simultáneas que pueden ejecutarse en el grupo de cargas de trabajo. Debe ser 0 o un entero positivo.  
  
 **Tiempo de CPU (seg)**  
 Especifique la cantidad máxima de tiempo de CPU que una solicitud puede usar. Debe ser 0 o un entero positivo. Si es 0, el tiempo es ilimitado.  
  
 **% de concesión de memoria**  
 Especifique la cantidad máxima de memoria que una única solicitud puede tomar del grupo. El rango es de 0 a 100.  
  
 **Tiempo de espera de concesión (s)**  
 Especifique el tiempo máximo que una consulta puede esperar hasta que esté disponible un recurso antes de que se produzca un error en la consulta. Debe ser 0 o un entero positivo.  
  
 **Grado de paralelismo**  
 Especifique el grado máximo de paralelismo (DOP) para las solicitudes paralelas. El rango es de 0 a 64.  
  
 Para obtener más información, vea [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md).  
  
## <a name="view-resource-governor-properties-using-transact-sql"></a>Ver las propiedades del regulador de recursos con Transact-SQL  
 **Ver las propiedades del regulador de recursos mediante Transact-SQL**  
  
1.  Para ver las definiciones de las entidades del regulador de recursos, use las [Vistas de catálogo del regulador de recursos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/resource-governor-catalog-views-transact-sql.md).  
  
2.  Para ver la configuración actual de las entidades del regulador de recursos, use las [Vistas de administración dinámica relacionadas con el regulador de recursos &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md).  
  
## <a name="more-information"></a>Más información
 [Regulador de recursos](../../relational-databases/resource-governor/resource-governor.md)   
 [Habilitar el regulador de recursos](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [Grupo de recursos de servidor del regulador de recursos](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [Grupos de cargas de trabajo del regulador de recursos](../../relational-databases/resource-governor/resource-governor-workload-group.md)   
 [Función clasificadora del regulador de recursos](../../relational-databases/resource-governor/resource-governor-classifier-function.md)  
  
  
