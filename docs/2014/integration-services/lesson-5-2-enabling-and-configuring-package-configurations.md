---
title: 'Paso 2: Habilitar y configurar las configuraciones de paquetes | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 005218ab-8dd5-48e9-a185-6bc60cd43a7a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: fa75b3a71832eaba4064de5a9dd90e73236e8177
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62891074"
---
# <a name="step-2-enabling-and-configuring-package-configurations"></a>Paso 2: Habilitación y configuración de configuraciones de paquete
  En esta tarea, convertirá el proyecto al modelo de implementación de paquetes y habilitará las configuraciones de paquetes mediante el Asistente para configuración de paquetes. Utilizará este asistente para generar un archivo de configuración XML que contiene parámetros de configuración para la propiedad `Directory` del contenedor de bucles Foreach. El valor de la propiedad Directory se proporciona a través de una variable nueva de nivel de paquete que puede actualizarse durante la ejecución. Además, rellenará una carpeta nueva de datos de ejemplo que utilizará durante las pruebas.  
  
### <a name="to-create-a-new-package-level-variable-mapped-to-the-directory-property"></a>Para crear una variable nueva de nivel de paquete asignada a la propiedad Directory  
  
1.  Haga clic en el fondo de la pestaña **Flujo de control** del Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)] . De este modo se establece en el paquete el ámbito de la variable que se va a crear.  
  
2.  En el menú [!INCLUDE[ssIS](../includes/ssis-md.md)] , seleccione **Variables**.  
  
3.  En la ventana **Variables** , haga clic en el icono Agregar variable.  
  
4.  En el cuadro **Nombre** , escriba **varFolderName**.  
  
    > [!IMPORTANT]  
    >  Los nombres de variables distinguen entre mayúsculas y minúsculas.  
  
5.  Compruebe que en el cuadro **Ámbito** se muestra el nombre del paquete (Lección 5).  
  
6.  Establezca el valor del cuadro **Tipo de datos** de la variable `varFolderName` en **String**.  
  
7.  Vuelva a la pestaña **Flujo de control** y haga doble clic en el contenedor **Foreach File in Folder** .  
  
8.  En la página **Colección** del **Editor de bucles Foreach**, haga clic en **Expresiones** y, después, haga clic en el botón de puntos suspensivos **(…)**.  
  
9. En el **Editor de expresiones de propiedad**, haga clic en el **propiedad** lista y seleccione `Directory`.  
  
10. En el **expresión** cuadro, haga clic en el botón de puntos suspensivos **(...)** .  
  
11. En el **Generador de expresiones**, expanda la carpeta Variables y arrastre la variable **User:varFolderName** al cuadro **Expresión** .  
  
12. Haga clic en **Aceptar** para salir del **Generador de expresiones**.  
  
13. Haga clic en **Aceptar** para salir del **Editor de expresiones de propiedad**.  
  
14. Haga clic en **Aceptar** para salir del **Editor de bucles Foreach**.  
  
### <a name="to-enable-package-configurations"></a>Para habilitar las configuraciones de paquetes  
  
1.  En el menú **Proyecto**, haga clic en **Convertir al modelo de implementación de paquetes**.  
  
2.  Haga clic en **Aceptar** en el mensaje de advertencia y, una vez completada la conversión, haga clic en **Aceptar** en el cuadro de diálogo **Convertir al modelo de implementación de paquetes** .  
  
3.  Haga clic en el fondo de la pestaña **Flujo de control** del Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)].  
  
4.  En el menú **SSIS** , haga clic en **Configuraciones de paquetes**.  
  
5.  En el cuadro de diálogo **Organizador de configuraciones de paquetes** , seleccione **Habilitar configuraciones de paquetes**y, después, haga clic en **Agregar**.  
  
6.  En la página de bienvenida del Asistente para la configuración de paquetes, haga clic en **Siguiente**.  
  
7.  En la página **Seleccionar tipo de configuración** , compruebe que el **Tipo de configuración** está establecido en **Archivo de configuración XML**.  
  
8.  En la página **Seleccionar tipo de configuración** , haga clic en **Examinar**.  
  
9. De forma predeterminada, el cuadro de diálogo **Seleccionar ubicación del archivo de configuración** se abrirá en la carpeta del proyecto.  
  
10. En el cuadro de diálogo **Seleccionar ubicación del archivo de configuración** , escriba **SSISTutorial** en **Nombre de archivo**y haga clic en **Guardar**.  
  
11. En la página **Seleccionar tipo de configuración** , haga clic en **Siguiente**.  
  
12. En la página **Seleccionar propiedades para la exportación** , en el panel **Objetos** , expanda **Variables**, luego **varFolderName**y **Propiedades**y, después, seleccione **Valor**.  
  
13. En la página **Seleccionar propiedades para la exportación** , haga clic en **Siguiente**.  
  
14. En la página **Finalización del asistente** , escriba un nombre para la configuración, por ejemplo, **Configuración del directorio del Tutorial de SSIS**. Este es el nombre de configuración que se muestra en el cuadro de diálogo **Organizador de configuraciones de paquetes** .  
  
15. Haga clic en **Finalizar**.  
  
16. Haga clic en **Cerrar**.  
  
17. El asistente crea un archivo de configuración, denominado SSISTutorial.dtsConfig, que contiene los valores de configuración para el `value` de la variable que a su vez establece el `Directory` propiedad del enumerador.  
  
    > [!NOTE]  
    >  Generalmente, un archivo de configuración contiene información compleja sobre las propiedades de un paquete, pero en este tutorial la única información de configuración debería ser  
    > <Configuration ConfiguredType="Property"  
    > Path="\Package.Variables[User::varFolderName].Properties[Value]" ValueType="String"\>  
    >  \<ConfiguredValue>\</ConfiguredValue>  
    > \</ Configuración >.  
  
### <a name="to-create-and-populate-a-new-sample-data-folder"></a>Para crear y rellenar una carpeta nueva de datos de ejemplo  
  
1.  En el Explorador de Windows, en el nivel raíz de la unidad (por ejemplo, C:\\), cree una carpeta nueva denominada `New Sample Data`.  
  
2.  Busque los archivos de ejemplo en su equipo y copie tres de los archivos de la carpeta.  
  
3.  En el `New Sample Data` carpeta, pegue los archivos copiados.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Paso 3: Modificar el valor de configuración de propiedad de directorio](lesson-5-3-modifying-the-directory-property-configuration-value.md)  
  
  
