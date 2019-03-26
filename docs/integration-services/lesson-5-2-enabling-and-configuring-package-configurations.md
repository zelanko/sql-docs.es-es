---
title: 'Paso 2: Habilitar y configurar configuraciones de paquetes | Microsoft Docs'
ms.custom: ''
ms.date: 01/08/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 005218ab-8dd5-48e9-a185-6bc60cd43a7a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b65e44de58e2aeea21485b1a2875fa7f00349dc5
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/20/2019
ms.locfileid: "58271689"
---
# <a name="lesson-5-2-enable-and-configure-package-configurations"></a>Lección 5-2: Habilitar y configurar configuraciones de paquetes

En esta tarea se convierte el proyecto al modelo de implementación de paquetes y se habilitan las configuraciones de paquetes mediante el Asistente para configuración de paquetes. Este asistente se usa para generar un archivo de configuración XML que contiene parámetros de configuración para la propiedad **Directory** del contenedor de bucles Foreach. El valor de la propiedad **Directory** se proporciona a través de una nueva variable de nivel de paquete que puede actualizarse en tiempo de ejecución. También se rellena una nueva carpeta de datos de ejemplo que se usa para las pruebas.  
  
## <a name="create-a-package-level-variable-mapped-to-the-directory-property"></a>Crear una variable de nivel de paquete asignada a la propiedad Directory  
  
1.  Seleccione el fondo de la pestaña **Flujo de control** del Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)]. Esta selección establece el ámbito de la variable que se crea en el paquete.  
  
2.  En el menú [!INCLUDE[ssIS](../includes/ssis-md.md)] , seleccione **Variables**.  
  
3.  En la ventana **Variables**, seleccione el icono **Agregar variable**.  
  
4.  En el cuadro **Nombre**, escriba **varFolderName**.  
  
    > [!IMPORTANT]  
    > Los nombres de variables distinguen entre mayúsculas y minúsculas.  
  
5.  Compruebe que en el cuadro **Ámbito** se muestra el nombre del paquete, **Lección 5**.  
  
6.  Establezca el valor del cuadro **Tipo de datos** de la variable `varFolderName` en **String**.  
  
7.  Vuelva a la pestaña **Flujo de control** y haga doble clic en el contenedor **Foreach File in Folder** .  
  
8.  En la página **Colección** del **Editor de bucles Foreach**, seleccione **Expresiones** y luego el botón de puntos suspensivos **(…)**.  
  
9. En el **Editor de expresiones de propiedad**, seleccione la lista **Propiedad** y luego **Directory**.  
  
10. En el cuadro **Expresión**, seleccione el botón de puntos suspensivos **(…)**.  
  
11. En el **Generador de expresiones**, expanda la carpeta **Variables y parámetros** y arrastre la variable **User::varFolderName** al cuadro **Expresión**.  
  
12. Seleccione **Aceptar** para salir del **Generador de expresiones**.  
  
13. Seleccione **Aceptar** para salir del **Editor de expresiones de propiedad**.  
  
14. Seleccione **Aceptar** para salir del **Editor de bucles Foreach**.  
  
## <a name="enable-package-configurations"></a>Habilitar configuraciones de paquetes  
  
1.  En el menú **Proyecto**, seleccione **Convertir al modelo de implementación de paquetes**.  
  
2.  Seleccione **Aceptar** en el mensaje de advertencia y, una vez completada la conversión, seleccione **Aceptar** en el cuadro de diálogo **Convertir al modelo de implementación de paquetes**.  
  
3.  Seleccione el fondo de la pestaña **Flujo de control** del Diseñador [!INCLUDE[ssIS](../includes/ssis-md.md)].  
  
4.  En el menú **SSIS**, seleccione **Configuraciones de paquetes**.  
  
5.  En el cuadro de diálogo **Organizador de configuraciones de paquetes**, seleccione **Habilitar configuraciones de paquetes** y luego **Agregar**.  
  
6.  En la página de inicio del **Asistente para configuración de paquetes**, seleccione **Siguiente**.  
  
7.  En la página **Seleccionar tipo de configuración** , compruebe que el **Tipo de configuración** está establecido en **Archivo de configuración XML**.  
  
8.  En la página **Seleccionar tipo de configuración**, seleccione **Examinar**.  
  
9. El cuadro de diálogo **Seleccionar ubicación del archivo de configuración** se abre en la carpeta del proyecto.  
  
10. En el cuadro de diálogo **Seleccionar ubicación del archivo de configuración**, en **Nombre de archivo**, escriba **SSISTutorial** y seleccione **Guardar**.  
  
11. En la página **Seleccionar tipo de configuración**, seleccione **Siguiente**.
  
12. En la página **Seleccionar propiedades para la exportación**, en el panel **Objetos**, expanda **Variables**, **varFolderName** y **Propiedades** y luego seleccione **Valor**.  
  
13. En la página **Seleccionar propiedades para la exportación**, seleccione **Siguiente**.  
  
14. En la página **Finalización del asistente**, escriba un nombre para la configuración, por ejemplo, **Configuración del directorio del Tutorial de SSIS**. El nombre de configuración se muestra en el cuadro de diálogo **Organizador de configuraciones de paquetes**.  
  
15. Seleccione **Finalizar**.  
  
16. Seleccione **Cerrar**.  
  
17. El asistente crea un archivo de configuración, denominado **SSISTutorial.dtsConfig**, que contiene parámetros de configuración para el **Valor** de la variable que, a su vez, establece la propiedad **Directory** del enumerador.  
  
    > [!NOTE]  
    > Generalmente, un archivo de configuración contiene información compleja sobre las propiedades del paquete, pero en este tutorial la única información de configuración debería ser la siguiente:

    ```
    <Configuration 
        ConfiguredType="Property"  
        Path="\Package.Variables[User::varFolderName].Properties[Value]" 
        ValueType="String">  
      <ConfiguredValue></ConfiguredValue>  
    </Configuration>
    ```
  
## <a name="create-and-populate-a-new-sample-data-folder"></a>Crear y rellenar una carpeta de nuevos datos de ejemplo  
  
1.  En el Explorador de Windows, en el nivel raíz de la unidad (por ejemplo, **C:\\**), cree una carpeta denominada **Nuevos datos de ejemplo**.  
  
2.  Busque los archivos de ejemplo en su equipo y copie tres de los archivos de la carpeta.  
  
3.  En la carpeta **Nuevos datos de ejemplo** , pegue los archivos copiados.  
  
## <a name="go-to-next-task"></a>Ir a la tarea siguiente  
[Paso 3: Modificar el valor de configuración de la propiedad Directory](../integration-services/lesson-5-3-modifying-the-directory-property-configuration-value.md)  
  
