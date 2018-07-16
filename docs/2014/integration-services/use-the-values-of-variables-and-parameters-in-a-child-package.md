---
title: Use los valores de Variables y parámetros de un paquete secundario | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- variables [Integration Services], passing between packages
- configurations [Integration Services]
- packages [Integration Services], configurations
- variables [Integration Services], adding
ms.assetid: 9b939edb-4e17-48e5-8428-855beb10049c
caps.latest.revision: 18
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f1c522a87bfd20608d1e42080ad9ff3d3ae10973
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37287521"
---
# <a name="use-the-values-of-variables-and-parameters-in-a-child-package"></a>Usar los valores de variables y parámetros en un paquete secundario
  Este procedimiento describe cómo crear una configuración de paquete que utiliza el tipo de configuración de variables primarias. Este tipo de configuración habilita un paquete secundario que se ejecuta desde un paquete primario para tener acceso a una variable del elemento primario.  
  
> [!NOTE]  
>  También puede pasar valores a un paquete secundario configurando la Tarea Ejecutar paquete para asignar variables o parámetros del paquete primario, o parámetros del proyecto, a parámetros del paquete secundario. Para más información, consulte [Execute Package Task](control-flow/execute-package-task.md).  
  
 No es necesario crear la variable en el paquete primario antes de crear la configuración de paquete en el paquete secundario. Puede agregar la variable al paquete primario en cualquier momento, pero debe utilizar el nombre exacto de la variable primaria en la configuración del paquete. Sin embargo, antes de que pueda crear una configuración de variable primaria, debe existir una variable en el paquete secundario que la configuración pueda actualizar. Para obtener más información sobre cómo agregar y configurar variables, vea [Agregar, eliminar, cambiar el ámbito de la variable definida por el usuario en un paquete](../../2014/integration-services/add-delete-change-scope-of-user-defined-variable-in-a-package.md).  
  
 El ámbito de la variable del paquete primario que se utiliza en una configuración de variable primaria se puede establecer en la tarea Ejecutar paquete, el contenedor que contiene la tarea o el paquete. Si se definen varias variables con el mismo nombre en un paquete, se utiliza la variable que está más próxima en ámbito de la tarea Ejecutar paquete. El ámbito más cercano a la tarea Ejecutar paquete es la tarea propiamente dicha.  
  
### <a name="to-add-a-variable-to-a-parent-package"></a>Para agregar una variable a un paquete primario  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete al que desea agregar una variable para pasar a un paquete secundario.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  En el diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] , siga uno de estos procedimientos para definir el ámbito de la variable:  
  
    -   Para establecer el ámbito en el paquete, haga clic en cualquier lugar de la superficie de diseño de la pestaña **Flujo de control** .  
  
    -   Para establecer el ámbito en un contenedor primario de la tarea Ejecutar paquete, haga clic en el contenedor.  
  
    -   Para establecer el ámbito a la tarea Ejecutar paquete, haga clic en ella.  
  
4.  Agregue y configure una variable.  
  
    > [!NOTE]  
    >  Seleccione un tipo de datos que sea compatible con los datos que almacenará la variable.  
  
5.  Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados**, en el menú **Archivo**.  
  
### <a name="to-add-a-variable-to-a-child-package"></a>Para agregar una variable a un paquete secundario  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contiene el paquete al que desea agregar una configuración de variable primaria.  
  
2.  En el Explorador de soluciones, haga doble clic en el paquete para abrirlo.  
  
3.  En el Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] , para establecer el ámbito en el paquete, haga clic en cualquier lugar de la superficie de diseño de la pestaña **Flujo de control** .  
  
4.  Agregue y configure una variable.  
  
    > [!NOTE]  
    >  Seleccione un tipo de datos que sea compatible con los datos que almacenará la variable.  
  
5.  Para guardar el paquete actualizado, haga clic en **Guardar los elementos seleccionados**, en el menú **Archivo**.  
  
### <a name="to-add-a-parent-package-configuration-to-a-child-package"></a>Para agregar una configuración de paquete primario a un paquete secundario  
  
1.  Si el paquete secundario todavía no está abierto, ábralo en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
2.  Haga clic en cualquier punto de la superficie de diseño de la pestaña **Flujo de control** .  
  
3.  En el menú **SSIS** , haga clic en **Configuraciones de paquetes**.  
  
4.  En el cuadro de diálogo **Organizador de configuraciones de paquetes** , seleccione **Habilitar configuraciones de paquetes**y haga clic en **Agregar**.  
  
5.  En la página de bienvenida del Asistente para la configuración de paquetes, haga clic en **Siguiente**.  
  
6.  En la página Seleccionar tipo de configuración, en la lista **Tipo de configuración** , seleccione **Variable de paquete primario** y realice una de las siguientes acciones:  
  
    -   Seleccione **Especificar valores de configuración directamente**y luego, en el cuadro **Variable primaria** , proporcione el nombre de la variable del paquete primario que se utilizará en la configuración.  
  
        > [!IMPORTANT]  
        >  Los nombres de variables distinguen entre mayúsculas y minúsculas.  
  
    -   Seleccione **La ubicación de configuración se almacena en una variable de entorno** y luego, en la **lista Variable de entorno**, seleccione la variable de entorno que contenga el nombre de la variable.  
  
7.  Haga clic en **Siguiente**.  
  
8.  En la página Seleccionar propiedad de destino, expanda el nodo **Variable** y expanda el nodo **Propiedades** de la variable para configurarla, y luego haga clic en la propiedad que establecerá la configuración.  
  
9. Haga clic en **Siguiente**.  
  
10. En la página Finalización del asistente, también puede modificar el nombre predeterminado de la configuración y revisar la información de configuración.  
  
11. Haga clic en **Finalizar** para completar el asistente y volver al cuadro de diálogo **Organizador de configuraciones de paquetes** .  
  
12. En el cuadro de diálogo **Organizador de configuraciones de paquetes** , el cuadro **Configuración** muestra la nueva configuración.  
  
13. Haga clic en **Cerrar**.  
  
## <a name="see-also"></a>Vea también  
 [Configuraciones de paquetes](../../2014/integration-services/package-configurations.md)   
 [Crear configuraciones de paquetes](../../2014/integration-services/create-package-configurations.md)   
 [Servicios de integración &#40;SSIS&#41; Variables](integration-services-ssis-variables.md)   
 [Usar variables en paquetes](../../2014/integration-services/use-variables-in-packages.md)  
  
  
