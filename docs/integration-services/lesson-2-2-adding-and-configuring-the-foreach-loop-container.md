---
title: 'Paso 2: Agregar y configurar el contenedor de bucles Para cada uno | Microsoft Docs'
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: tutorial
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 88a973cc-0f23-4ecf-adb6-5b06279c2df6
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 80a4fa426a322346de99aafef393e75a67e7e82a
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="lesson-2-2---adding-and-configuring-the-foreach-loop-container"></a>Lección 2-2: Agregar y configurar el contenedor de bucles Para cada uno
En esta tarea, agregará la capacidad de buscar en una carpeta de archivos planos y aplicará la misma transformación de flujo de datos utilizada en la lección 1 a cada uno de dichos archivos planos. Para ello, agregará y configurará un contenedor de bucles Foreach para el flujo de control.  
  
El contenedor de bucles Foreach que agregue debe poder conectarse a cada uno de los archivos planos de la carpeta. Puesto que todos los archivos de la carpeta tienen el mismo formato, el contenedor de bucles Foreach puede utilizar el mismo administrador de conexiones de archivos planos para conectarse a cada uno de estos archivos. El administrador de conexiones de archivos planos que el contenedor utilizará es el mismo administrador de conexiones de archivos planos que creó en la lección 1.  
  
Actualmente, el administrador de conexiones de archivos planos de la lección 1 se conecta a un único archivo plano específico. Para conectarse de forma iterativa a cada uno de los archivos planos de la carpeta, deberá configurar el contenedor de bucles Foreach y el administrador de conexiones de archivos planos de este modo:  
  
-   **Contenedor de bucles Foreach:** Asignará el valor enumerado del contenedor a una variable de paquete definida por el usuario. El contenedor usará esta variable definida por el usuario para modificar de forma dinámica la propiedad **ConnectionString** del administrador de conexiones de archivos planos y conectar de forma iterativa cada uno de los archivos planos de la carpeta.  
  
-   **Administrador de conexiones de archivos planos:** Modificará el administrador de conexiones creado en la lección 1 mediante una variable definida por el usuario para rellenar la propiedad **ConnectionString** del administrador de conexiones.  
  
En los procedimientos de esta tarea se muestra cómo crear y modificar el contenedor de bucles Foreach para utilizar una variable de paquete definida por el usuario y agregar la tarea de flujo de datos al bucle. Aprenderá a modificar el administrador de conexiones de archivos planos para utilizar una variable definida por el usuario en la siguiente tarea.  
  
Una vez realizadas estas modificaciones en el paquete, cuando éste se ejecute, el contenedor de bucles Foreach se iterará en la colección de archivos de la carpeta Datos de ejemplo. Cada vez que se encuentre un archivo que coincida con los criterios, el contenedor de bucles Foreach rellenará la variable definida por el usuario con el nombre de archivo, asignará la variable definida por el usuario a la propiedad **ConnectionString** del administrador de conexiones de archivos planos Sample Currency Data y, después, ejecutará el flujo de datos en ese archivo. Por consiguiente, en cada iteración del bucle Foreach la tarea de flujo de datos utilizará un archivo plano distinto.  
  
> [!NOTE]  
> Puesto que [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] separa el flujo de control del flujo de datos, los bucles que agregue al flujo de control no precisarán ninguna modificación en el flujo de datos. Por consiguiente, no es necesario modificar el flujo de datos creado en la lección 1.  
  
### <a name="to-add-a-foreach-loop-container"></a>Para agregar un contenedor de bucles Foreach  
  
1.  En **SQL Server Data Tools**, haga clic en la pestaña **Flujo de control** .  
  
2.  En el **Cuadro de herramientas de SSIS**, expanda **Contenedores**y arrastre un **Contenedor de bucles Foreach** a la superficie de diseño de la pestaña **Flujo de control** .  
  
3.  Haga clic con el botón derecho en el **Contenedor de bucles Foreach** que acaba de agregar y seleccione **Editar**.  
  
4.  En el cuadro de diálogo **Editor de bucles Foreach** , en la página **General** , en **Nombre**, escriba **Foreach File in Folder**. Haga clic en **Aceptar**.  
  
5.  Haga clic con el botón derecho en el contenedor de bucles Foreach, haga clic en **Propiedades**y, en la ventana Propiedades, compruebe que la propiedad **LocaleID** esté establecida en **Inglés (Estados Unidos)**.  
  
### <a name="to-configure-the-enumerator-for-the-foreach-loop-container"></a>Para configurar el enumerador para el contenedor de bucles Foreach  
  
1.  Haga doble clic en Foreach File in Folder para volver a abrir el **Editor de bucles Foreach**.  
  
2.  Haga clic en **Colección**.  
  
3.  En la página **Colección** , seleccione **Enumerador de archivos Foreach**.  
  
4.  En el grupo **Configuración de enumerador** , haga clic en **Examinar**.  
  
5.  En el cuadro de diálogo **Buscar carpeta** , busque la carpeta del equipo que contenga los archivos Currency_*.txt.  
  
    Estos datos de ejemplo se incluyen con los paquetes de lecciones de [!INCLUDE[ssIS](../includes/ssis-md.md)] . Para descargar los datos de ejemplo y los paquetes de lecciones, haga lo siguiente.  
  
    1.  Navegue a los [ejemplos del producto Integration Services](http://go.microsoft.com/fwlink/?LinkId=275027). 
  
    2.  Haga clic en la pestaña **DOWNLOADS** .  
  
    3.  Haga clic en vínculo del archivo [SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip](http://msftisprodsamples.codeplex.com/downloads/get/596031)  
  
6.  En el cuadro **Archivos**, escriba **Currency_\*.txt**.  
  
### <a name="to-map-the-enumerator-to-a-user-defined-variable"></a>Para asignar el enumerador a una variable definida por el usuario  
  
1.  Haga clic en **Asignaciones de variables**.  
  
2.  En la página **Asignaciones de variables**, en la columna **Variable**, haga clic en la celda vacía y seleccione **\<Nueva variable...>**.  
  
3.  En el cuadro de diálogo **Agregar variable** , en **Nombre**, escriba **varFileName**.  
  
    > [!IMPORTANT]  
    > Los nombres de variables distinguen entre mayúsculas y minúsculas.  
  
4.  Haga clic en **Aceptar**.  
  
5.  Haga clic de nuevo en **Aceptar** para salir del cuadro de diálogo **Editor de bucles Foreach** .  
  
### <a name="to-add-the-data-flow-task-to-the-loop"></a>Para agregar la tarea de flujo de datos al bucle  
  
-   Arrastre la tarea Flujo de datos **Extract Sample Currency Data** al contenedor de bucles Foreach que ahora se denomina **Foreach File in Folder**.  
  
## <a name="next-lesson-task"></a>Tarea de la siguiente lección  
[Paso 3: Modificar el Administrador de conexiones de archivos planos](../integration-services/lesson-2-3-modifying-the-flat-file-connection-manager.md)  
  
## <a name="see-also"></a>Ver también  
[configurar un contenedor de bucles Foreach](http://msdn.microsoft.com/library/519c6f96-5e1f-47d2-b96a-d49946948c25)  
[Usar variables en paquetes](http://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)  
  
  
  
