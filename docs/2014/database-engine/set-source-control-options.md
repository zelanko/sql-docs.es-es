---
title: Establecer opciones de Control de código fuente | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Source_Control.Visual_SourceSafe
- VS.ToolsOptionsPages.Source_Control.General
- VS.ToolsOptionsPages.Source_Control.Environment
helpviewer_keywords:
- source controls [SQL Server Management Studio], options
ms.assetid: b2c6ca00-46f0-4f86-b067-07bae779c147
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0a654932689785d96aaff049551faf19494c311a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62843754"
---
# <a name="set-source-control-options"></a>Establecer las opciones de control de código fuente
  Antes de aprovechar las características de control de código fuente integradas en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], es necesario configurar las opciones de control de código fuente de los diversos entornos en los que trabaje.  
  
 Configurar opciones de control de código fuente mediante la **opciones** cuadro de diálogo para configurar uno o varios roles de control de código fuente. Un rol se compone de una descripción general de la configuración en la que se utiliza [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] y las opciones de control de código fuente asociadas a esa configuración.  
  
 Por ejemplo, si es desarrollador de software de bases de datos independiente, normalmente no crea conflictos con otros usuarios al conservar los archivos desprotegidos después de haberlos protegido. En consecuencia, [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] define un rol de desarrollador de software independiente. Para este rol, [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] selecciona automáticamente el **mantener elementos desprotegidos cuando se protejan** opción.  
  
 Puesto que puede definir y personalizar roles, puede trabajar en diversas configuraciones de desarrollo sin necesidad de volver a configurar completamente el control de código fuente cada vez que pasa de una configuración a otra.  
  
### <a name="to-set-source-control-options"></a>Para establecer las opciones de control de código fuente  
  
1.  En el menú **Herramientas** , haga clic en **Opciones**.  
  
2.  En el **opciones** cuadro de diálogo, expanda **Control de código fuente**y, a continuación, haga clic en el **selección de complemento** página.  
  
     **Complemento de control de código fuente actual**  
     Seleccione en esta lista el control de código fuente que desee utilizar. El cliente del producto de control de código fuente deberá estar instalado en este equipo para que aparezca en la lista. Si no hay ningún cliente de control de código fuente instalado en el equipo, la única selección disponible será Ninguno. Si ha instalado Microsoft Source Safe, los siguientes complementos se mostrarán a continuación:  
  
    -   Microsoft Visual SourceSafe  
  
    -   Microsoft Visual SourceSafe (Internet)  
  
3.  Establezca las credenciales de inicio de sesión de cada rol de control de código fuente que desee usar. Esta página solo está disponible si está instalado un complemento de control de código fuente.  
  
     **Descripción del rol**  
     La selección de uno de estos roles hace que las opciones de control de código fuente correspondientes se seleccionen automáticamente.  
  
    |Rol|Descripción|  
    |----------|-----------------|  
    |**Visual SourceSafe**|Especifica que desea usar la configuración más utilizada por [!INCLUDE[msCoName](../includes/msconame-md.md)] usuarios de Visual SourceSafe.|  
    |**Desarrollador independiente**|Especifica que el usuario está realizando su trabajo de forma independiente.|  
    |**Custom**|Especifica que el usuario ha modificado la configuración de un rol.|  
  
     **Realice las actualizaciones de estado en segundo plano**  
     Actualiza automáticamente los iconos de señal del control de código fuente en el Explorador de soluciones cuando cambia el estado de un elemento. Si se producen retrasos al realizar operaciones que consumen muchos recursos del servidor, en especial cuando abre una solución o un proyecto desde el control de código fuente, la desactivación de esta casilla puede mejorar el rendimiento.  
  
     **Id. de inicio de sesión**  
     Especifica el nombre de usuario que se va a utilizar para iniciar la sesión en el proveedor del control de código fuente. Si se admite el proveedor de control de código fuente, este nombre se rellena automáticamente en el **inicio de sesión** cuadro de diálogo para llegar a su servidor de control de código fuente. Para activar esta opción, utilice el programa de administrador del proveedor del control de código fuente para deshabilitar los inicios de sesión automáticos y reinicie [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
     **Avanzadas**  
     Muestra opciones adicionales para agregar elementos al control de código fuente. Estas opciones dependen del proveedor del control de código fuente. En el programa del control de código fuente dispone de ayuda para estas opciones.  
  
4.  Seleccione el **entorno** página.  
  
5.  En el **configuración del entorno de Control de código fuente** , seleccione el rol en el que desea establecer opciones de control de código fuente.  
  
     [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] activa automáticamente las opciones de control de código fuente del rol que ha seleccionado. Si desactiva alguna de las opciones predeterminadas, la **configuración del entorno de Control de código fuente** cuadro muestra la **personalizado** opción para indicar que ha personalizado el rol seleccionado originalmente.  
  
     **Configuración del entorno de Control de código fuente**  
     Especifica el rol que se desea utilizar. [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] define los siguientes roles.  
  
    |Rol|Descripción|  
    |----------|-----------------|  
    |**Visual SourceSafe**|Especifica que desea usar la configuración más utilizada por [!INCLUDE[msCoName](../includes/msconame-md.md)] usuarios de Visual SourceSafe.|  
    |**Desarrollador independiente**|Especifica que el usuario está realizando su trabajo de forma independiente.|  
    |**Custom**|Especifica que el usuario ha modificado la configuración de un rol.|  
  
     La selección de uno de estos roles hace que las opciones de control de código fuente correspondientes se seleccionen automáticamente.  
  
     **Mantener elementos desprotegidos cuando se protejan**  
     Especifica que cuando el usuario proteja elementos para actualizar el almacén de control de código fuente, los elementos deben permanecer desprotegidos para el usuario. Si desea cambiar esta opción para una inserción en específico, haga clic en el **opciones** flecha en el **proteger** cuadro de diálogo y, a continuación, desactive la **Mantener desprotegido** casilla de verificación.  
  
     **Elementos protegidos**  
     Muestra una lista de opciones que especifican cómo [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] debería comportarse al intentar editar un elemento que no está desprotegido. Las tablas siguientes describen las opciones disponibles.  
  
     **Al guardar**  
  
    |Acción|Descripción|  
    |------------|-----------------|  
    |**Preguntar para desproteger**|Muestra el **desproteger** cuadro de diálogo.|  
    |**Desproteger automáticamente**|Desprotege el elemento sin mostrar el **desproteger** cuadro de diálogo. Ésta es la opción predeterminada.|  
    |**Guardar como**|Guarda como un nuevo archivo.|  
  
     **Edición**  
  
    |Acción|Descripción|  
    |------------|-----------------|  
    |**Preguntar para desproteger**|Muestra el **desproteger** cuadro de diálogo.|  
    |**Solicitar desprotecciones exclusivas**|Muestra el **desproteger** cuadro de diálogo.|  
    |**Desproteger automáticamente**|Desprotege el elemento sin mostrar el **desproteger** cuadro de diálogo. Ésta es la opción predeterminada.|  
    |**No hacer nada**|No desprotege el archivo.|  
  
     **Permitir que los elementos protegidos se puedan editar**  
     Especifica que los elementos que están protegidos puedan editarse en la memoria. Si selecciona esta casilla, un **editar** botón aparece en la **desproteger** cuadro de diálogo cuando se intenta editar un elemento protegido. Después de hacer clic en este botón, podrá editar el elemento. Si intenta guardar el elemento, deberá desprotegerlo o guardarlo en una ubicación distinta.  
  
     **Restablecer**  
     Restablece los cuadros de diálogo de confirmación de control de código fuente a sus valores predeterminados. Por ejemplo, si ha seleccionado la **no volver a mostrar este cuadro de diálogo** casilla de verificación en un cuadro de diálogo de control de código fuente, seleccione el **restablecer** opción revierte dicha acción.  
  
## <a name="see-also"></a>Vea también  
 [Fundamentos del Control de código fuente](../../2014/database-engine/source-control-basics.md)   
 [Cambio de conexiones de Control de código fuente](../../2014/database-engine/change-source-control-connections.md)   
 [Excluir archivos desde el control de código fuente](../../2014/database-engine/exclude-files-from-source-control.md)  
  
  
