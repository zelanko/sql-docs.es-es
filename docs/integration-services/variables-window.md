---
title: Ventana Variables | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.reviewer: 
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.variables.f1
- sql13.dts.designer.variableoptionswindow.f1
helpviewer_keywords: Variables Window dialog box
ms.assetid: f405e5ce-ef69-4c58-8c7d-a3d44dfe9ab0
caps.latest.revision: "53"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 79b8887bd738bc5b91ad35febadbc528968881cb
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="variables-window"></a>Ventana Variables
  Use la ventana **Variables** para crear y modificar variables definidas por el usuario y ver variables del sistema.  
  
 De forma predeterminada, la ventana **variables** se encuentra debajo del área **Administradores de conexiones** en el Diseñador SSIS, en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Si no ve la ventana **variables** , haga clic en **variables** en el menú **SSIS** para mostrar la ventana.  
  
 También puede ver la ventana **Variables** si asigna el comando View.Variables a una combinación de teclas que desee en la página **Teclado** del cuadro de diálogo **Opciones** .  
  
> [!NOTE]  
>  Los valores de las propiedades **Nombre** y **Espacio de nombres** deben empezar con una letra, como se define en el Estándar Unicode 2.0, o un carácter de subrayado (_). Los caracteres siguientes pueden ser letras o números, tal como se define en el Estándar Unicode 2.0, o el carácter de subrayado (\_).  
  
## <a name="options"></a>Opciones  
 **Agregar variable**  
 Agrega una variable definida por el usuario.  
  
 **Mover variable**  
 Haga clic en una variable de la lista y luego en **Mover variable** para cambiar el ámbito de la variable. En el cuadro de diálogo **Seleccionar nuevo ámbito** , seleccione el paquete o un contenedor, una tarea o un controlador de eventos en el paquete, para cambiar el ámbito de la variable.  
  
 Para más información sobre el ámbito de las variables, vea [Variables de Integration Services &#40;SSIS&#41;](../integration-services/integration-services-ssis-variables.md).  
  
 **Eliminar variable**  
 Seleccione una variable en la lista y, luego, haga clic en **Eliminar variable**.  
  
 **Opciones de cuadrícula**  
 Haga clic para abrir el cuadro de diálogo **Opciones de la cuadrícula de variables** , donde puede cambiar la selección de la columna y aplicar filtros a la ventana **Variables** . Para más información, consulte [Opciones de la cuadrícula de variables](../integration-services/variable-grid-options.md).  
  
 **Nombre**  
 Escriba el nombre de la variable. Puede actualizar el nombre de la variable para las variables definidas por el usuario.  
  
 **Ámbito**  
 Presenta el ámbito de la variable. La variable tiene el ámbito de todo el paquete o el ámbito de un contenedor o una tarea. El ámbito de la variable debe ser suficiente como para que ésta sea visible para cualquier otra tarea u otro componente que necesite leer o establecer su valor.  
  
 Puede cambiar el ámbito haciendo clic en la variable y haciendo clic en **Mover variable** en la ventana **Variables** .  
  
 **Tipo de datos**  
 Presenta el tipo de datos de la variable. Puede seleccionar un tipo de dato de la lista para variables definidas por el usuario.  
  
> [!NOTE]  
>  Si asigna una expresión variable, no puede cambiar el tipo de datos.  
  
 **Value**  
 Presenta el valor de la variable. Puede actualizar el valor de la variable para variables definidas por el usuario. Este valor puede ser un literal o una expresión y el valor puede ser una cadena de varias líneas. Para asignar una expresión variable, haga clic en el botón de la elipse que se encuentra junto a la columna **Expresión** en la ventana **Variables** .  
  
 **Espacio de nombres**  
 Presenta el nombre del espacio de nombres. Las variables definidas por el usuario se crean inicialmente en el espacio de nombres **Usuario** , pero puede cambiar el nombre del espacio de nombres en el campo **Espacio de nombres** . Para mostrar esta columna, haga clic en **Opciones de cuadrícula**.  
  
 **Raise Change Event**  
 Indica si se activa un evento **OnVariableValueChanged** cuando un valor cambia. Puede actualizar el valor de la variable para variables definidas por el usuario y el sistema. De manera predeterminada, la ventana **Variables** no muestra esta columna. Para mostrar esta columna, haga clic en **Opciones de cuadrícula**.  
  
 **Description**  
 Vea la descripción de la variable. Puede cambiar la descripción para variables definidas por el usuario. De manera predeterminada, la ventana **Variables** no muestra esta columna. Para mostrar esta columna, haga clic en **Opciones de cuadrícula**.  
  
 **Expresión**  
 Vea la expresión asignada a la variable. Para asignar una expresión, haga clic en el botón de la elipse.  
  
 Si asigna una expresión a una variable, un marcador especial de icono se muestra junto a la variable. Este marcador de icono especial también aparece junto a los administradores de conexiones y las tareas con expresiones establecidas.  

## <a name="variable-grid-options-dialog-box"></a>Cuadro de diálogo Opciones de la cuadrícula de variables
 Utilice el cuadro de diálogo **Opciones de la cuadrícula de variables** para seleccionar las columnas que se mostrarán en la ventana **Variables** y seleccionar los filtros para aplicarlos a la lista de variables. Para más información sobre las propiedades de variable correspondientes, vea [Variables de Integration Services &#40;SSIS&#41;](../integration-services/integration-services-ssis-variables.md).  
  
### <a name="options-for-filter"></a>Opciones del filtro  
 **Mostrar variables del sistema**  
 Seleccione para mostrar variables del sistema en la ventana de **Variables** . Las variables del sistema están predefinidas. Las variables del sistema no se pueden agregar ni eliminar. Puede modificar la configuración de propiedades de **RaiseChangedEvent** .  
  
 Esta lista está codificada en color. Las variables del sistema son grises y las definidas por el usuario son negras.  
  
 **Mostrar variables de todos los ámbitos**  
 Seleccione mostrar las variables en el ámbito del paquete y, en el ámbito de los contenedores, tareas y controladores de eventos en el paquete. Desactive esta opción para mostrar solo variables en el ámbito del paquete y en el ámbito de un contenedor, una tarea o un controlador de eventos seleccionada.  
  
 Para más información sobre el ámbito de las variables, vea [Variables de Integration Services &#40;SSIS&#41;](../integration-services/integration-services-ssis-variables.md).  
  
### <a name="options-for-columns"></a>Opciones de las columnas  
 Seleccione las columnas que desea que aparezcan en la ventana **Variables** .  
  
-   **Ámbito**  
  
-   **Data type**  
  
-   **Value**  
  
-   **Espacio de nombres**  
  
-   **Desencadenar el evento cuando cambie el valor de la variable**  
  
-   **Description**  
  
-   **Expresión**  
  
## <a name="see-also"></a>Vea también  
 [Variables de Integration Services &#40;SSIS&#41;](../integration-services/integration-services-ssis-variables.md)   
 [Usar variables en paquetes](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)   
 [Expresiones de Integration Services &#40;SSIS&#41;](../integration-services/expressions/integration-services-ssis-expressions.md)   
 [Generar archivos de volcado para la ejecución de paquetes](../integration-services/troubleshooting/generating-dump-files-for-package-execution.md)  
  
  
