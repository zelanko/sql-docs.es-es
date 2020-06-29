---
title: Ventana Variables | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.variables.f1
helpviewer_keywords:
- Variables Window dialog box
ms.assetid: f405e5ce-ef69-4c58-8c7d-a3d44dfe9ab0
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 62daceac93eda76f2d81ea0fdce00a3c5fa7e97f
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85420152"
---
# <a name="variables-window"></a>Ventana Variables
  Use la ventana **Variables** para crear y modificar variables definidas por el usuario y ver variables del sistema.  
  
 De forma predeterminada, la ventana **variables** se encuentra debajo del área **Administradores de conexiones** en el Diseñador SSIS, en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Si no ve la ventana **variables**, haga clic en **Variables** en el menú **SSIS** para mostrar la ventana.  
  
 También puede ver la ventana **Variables** si asigna el comando View.Variables a una combinación de teclas que desee en la página **Teclado** del cuadro de diálogo **Opciones** .  
  
> [!NOTE]
>  Los valores de las propiedades `Name` y `Namespace` deben empezar con una letra, como se define en el Estándar Unicode 2.0, o un carácter de subrayado (_). Los caracteres siguientes pueden ser letras o números, tal como se define en el Estándar Unicode 2.0, o el carácter de subrayado (\_).  
  
## <a name="options"></a>Opciones  
 **Agregar variable**  
 Agrega una variable definida por el usuario.  
  
 **Mover variable**  
 Haga clic en una variable de la lista y luego en **Mover variable** para cambiar el ámbito de la variable. En el cuadro de diálogo **Seleccionar nuevo ámbito** , seleccione el paquete o un contenedor, una tarea o un controlador de eventos en el paquete, para cambiar el ámbito de la variable.  
  
 Para más información sobre el ámbito de las variables, vea [Variables de Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md).  
  
 **Eliminar variable**  
 Seleccione una variable en la lista y, luego, haga clic en **Eliminar variable**.  
  
 **Opciones de cuadrícula**  
 Haga clic para abrir el cuadro de diálogo **Opciones de la cuadrícula de variables** , donde puede cambiar la selección de la columna y aplicar filtros a la ventana **Variables** . Para más información, consulte [Opciones de la cuadrícula de variables](../../2014/integration-services/variable-grid-options.md).  
  
 `Name`  
 Escriba el nombre de la variable. Puede actualizar el nombre de la variable para las variables definidas por el usuario.  
  
 **Ámbito**  
 Presenta el ámbito de la variable. La variable tiene el ámbito de todo el paquete o el ámbito de un contenedor o una tarea. El ámbito de la variable debe ser suficiente como para que ésta sea visible para cualquier otra tarea u otro componente que necesite leer o establecer su valor.  
  
 Puede cambiar el ámbito haciendo clic en la variable y haciendo clic en **Mover variable** en la ventana **Variables** .  
  
 **Tipo de datos**  
 Presenta el tipo de datos de la variable. Puede seleccionar un tipo de dato de la lista para variables definidas por el usuario.  
  
> [!NOTE]  
>  Si asigna una expresión variable, no puede cambiar el tipo de datos.  
  
 **Valor**  
 Presenta el valor de la variable. Puede actualizar el valor de la variable para variables definidas por el usuario. Este valor puede ser un literal o una expresión y el valor puede ser una cadena de varias líneas. Para asignar una expresión variable, haga clic en el botón de la elipse que se encuentra junto a la columna **Expresión** en la ventana **Variables** .  
  
 `Namespace`  
 Presenta el nombre del espacio de nombres. Las variables definidas por el usuario se crean Inicialmente en el espacio de nombres del **usuario** , pero puede cambiar el nombre del espacio de nombres en el `Namespace` campo. Para mostrar esta columna, haga clic en **Opciones de cuadrícula**.  
  
 **Raise Change Event**  
 Indica si se activa un evento `OnVariableValueChanged` cuando un valor cambia. Puede actualizar el valor de la variable para variables definidas por el usuario y el sistema. De manera predeterminada, la ventana **Variables** no muestra esta columna. Para mostrar esta columna, haga clic en **Opciones de cuadrícula**.  
  
 **Descripción**  
 Vea la descripción de la variable. Puede cambiar la descripción para variables definidas por el usuario. De manera predeterminada, la ventana **Variables** no muestra esta columna. Para mostrar esta columna, haga clic en **Opciones de cuadrícula**.  
  
 **Expression**  
 Vea la expresión asignada a la variable. Para asignar una expresión, haga clic en el botón de la elipse.  
  
 Si asigna una expresión a una variable, un marcador especial de icono se muestra junto a la variable. Este marcador de icono especial también aparece junto a los administradores de conexiones y las tareas con expresiones establecidas.  
  
## <a name="see-also"></a>Consulte también  
 [Integration Services &#40;&#41; variables de SSIS](integration-services-ssis-variables.md)   
 [Usar variables en paquetes](../../2014/integration-services/use-variables-in-packages.md)   
 [Integration Services &#40;expresiones de&#41; SSIS](expressions/integration-services-ssis-expressions.md)   
 [Generar archivos de volcado para la ejecución de paquetes](troubleshooting/generating-dump-files-for-package-execution.md)  
  
  
