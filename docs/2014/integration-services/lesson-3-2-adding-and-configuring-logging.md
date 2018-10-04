---
title: 'Paso 2: Agregar y configurar el registro | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 56105f3f-e500-4669-8c8e-acf434527727
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5fdbbc852790446560b127411120709f05f513bc
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48128304"
---
# <a name="step-2-adding-and-configuring-logging"></a>Paso 2: Agregar y configurar el registro
  En esta tarea, habilitará el registro del flujo de datos del paquete Lesson 3.dtsx. A continuación, configurará un proveedor de registro de archivos de texto para registrar los eventos PipelineExecutionPlan y PipelineExecuteTrees. El proveedor de registro de archivos de texto crea registros que pueden verse y transportarse con facilidad. La sencillez de estos archivos de registro hace que sean especialmente útiles durante la fase de prueba básica de un paquete. También puede ver las entradas del archivo de registro en la ventana Registrar eventos del Diseñador de [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
### <a name="to-add-logging-to-the-package"></a>Para agregar el registro al paquete  
  
1.  En el menú **SSIS** , haga clic en **Registro**.  
  
2.  En el cuadro de diálogo **Configurar registros de SSIS** , asegúrese de que en el panel **Contenedores** el objeto situado en la posición superior, que representa el paquete de la lección 3, está seleccionado.  
  
3.  En la pestaña **Proveedores y registros** , en el cuadro **Tipo de proveedor** , seleccione **Proveedor de registro SSIS para archivos de texto**y haga clic en **Agregar**.  
  
     Integration Services agrega un nuevo proveedor de registro para archivos de texto al paquete con el nombre predeterminado **Proveedor de registro SSIS para archivos de texto**. Ahora puede configurar el nuevo proveedor de registro.  
  
4.  En el **nombre** columna, escriba `Lesson 3 Log File`.  
  
5.  Si lo desea, modifique el campo **Descripción**.  
  
6.  En el **configuración** columna, haga clic en  **\<nueva conexión >** para especificar el destino al que se escribe la información del registro.  
  
     En el cuadro de diálogo **Editor del administrador de conexiones de archivos** , en **Tipo de uso**, seleccione **Crear archivo**y, a continuación, haga clic en **Examinar**. De forma predeterminada, el cuadro de diálogo **Seleccionar archivo** abre la carpeta del proyecto, pero puede guardar la información de registro en cualquier ubicación.  
  
7.  En el **Seleccionar archivo** cuadro de diálogo el **nombre de archivo** cuadro, escriba `TutorialLog.log`y haga clic en **abierto**.  
  
8.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Editor del administrador de conexiones de archivos** .  
  
9. En el panel **Contenedores** , expanda todos los nodos de la jerarquía del contenedor de paquetes y, a continuación, desactive todas las casillas, incluida **Extract Sample Currency Data** . Ahora, active la casilla **Extract Sample Currency Data** para obtener solo los eventos de este nodo.  
  
    > [!IMPORTANT]  
    >  Si la casilla **Extract Sample Currency Data** está atenuada en lugar de activada, la tarea usa la configuración de registro del contenedor primario y no se pueden habilitar los eventos de registro específicos de la tarea.  
  
10. En la columna **Eventos** de la pestaña **Detalles** , seleccione los eventos **PipelineExecutionPlan** y **PipelineExecutionTrees** .  
  
11. Haga clic en **Avanzadas** para revisar los detalles que el proveedor de registro escribirá en el registro para cada evento. De forma predeterminada, todas las categorías de información se seleccionan automáticamente para los eventos que se especifiquen.  
  
12. Haga clic en **Básicas** para ocultar las categorías de información.  
  
13. En el **proveedores y registros** ficha la **nombre** columna, seleccione `Lesson 3 Log File`. Una vez que haya creado un proveedor de registro para el paquete, si lo desea, puede anular su selección para desactivar temporalmente el registro, sin tener que eliminar un proveedor de registro y crearlo de nuevo.  
  
14. Haga clic en **Aceptar**.  
  
## <a name="next-steps"></a>Pasos siguientes  
 [Paso 3: Probar el paquete del tutorial de la lección 3](../integration-services/lesson-3-3-testing-the-lesson-3-tutorial-package.md)  
  
  
