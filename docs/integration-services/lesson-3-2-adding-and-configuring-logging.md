---
title: 'Paso 2: Agregar y configurar el registro | Microsoft Docs'
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
ms.topic: get-started-article
applies_to: SQL Server 2016
ms.assetid: 56105f3f-e500-4669-8c8e-acf434527727
caps.latest.revision: "21"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 2a318589eae5c96aed87835bd17bd3defceccf17
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="lesson-3-2---adding-and-configuring-logging"></a>Lección 3-2: Agregar y configurar el registro
En esta tarea, habilitará el registro del flujo de datos del paquete Lesson 3.dtsx. A continuación, configurará un proveedor de registro de archivos de texto para registrar los eventos PipelineExecutionPlan y PipelineExecuteTrees. El proveedor de registro de archivos de texto crea registros que pueden verse y transportarse con facilidad. La sencillez de estos archivos de registro hace que sean especialmente útiles durante la fase de prueba básica de un paquete. También puede ver las entradas del archivo de registro en la ventana Registrar eventos del Diseñador de [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
### <a name="to-add-logging-to-the-package"></a>Para agregar el registro al paquete  
  
1.  En el menú **SSIS** , haga clic en **Registro**.  
  
2.  En el cuadro de diálogo **Configurar registros de SSIS** , asegúrese de que en el panel **Contenedores** el objeto situado en la posición superior, que representa el paquete de la lección 3, está seleccionado.  
  
3.  En la pestaña **Proveedores y registros** , en el cuadro **Tipo de proveedor** , seleccione **Proveedor de registro SSIS para archivos de texto**y haga clic en **Agregar**.  
  
    Integration Services agrega un nuevo proveedor de registro para archivos de texto al paquete con el nombre predeterminado **Proveedor de registro SSIS para archivos de texto**. Ahora puede configurar el nuevo proveedor de registro.  
  
4.  En la columna **Nombre** , escriba **Lesson 3 Log File**.  
  
5.  Si lo desea, modifique el campo **Descripción**.  
  
6.  En la columna **Configuración** haga clic en **<New Connection>** para especificar el destino en el que se escribe la información de registro.  
  
    En el cuadro de diálogo **Editor del administrador de conexiones de archivos** , en **Tipo de uso**, seleccione **Crear archivo**y, a continuación, haga clic en **Examinar**. De forma predeterminada, el cuadro de diálogo **Seleccionar archivo** abre la carpeta del proyecto, pero puede guardar la información de registro en cualquier ubicación.  
  
7.  En el cuadro de diálogo **Seleccionar archivo** , en el cuadro **Nombre de archivo** , escriba **TutorialLog.log**y haga clic en **Abrir**.  
  
8.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **Editor del administrador de conexiones de archivos** .  
  
9. En el panel **Contenedores** , expanda todos los nodos de la jerarquía del contenedor de paquetes y, a continuación, desactive todas las casillas, incluida **Extract Sample Currency Data** . Ahora, active la casilla **Extract Sample Currency Data** para obtener solo los eventos de este nodo.  
  
    > [!IMPORTANT]  
    > Si la casilla **Extract Sample Currency Data** está atenuada en lugar de activada, la tarea usa la configuración de registro del contenedor primario y no se pueden habilitar los eventos de registro específicos de la tarea.  
  
10. En la columna **Eventos** de la pestaña **Detalles** , seleccione los eventos **PipelineExecutionPlan** y **PipelineExecutionTrees** .  
  
11. Haga clic en **Avanzadas** para revisar los detalles que el proveedor de registro escribirá en el registro para cada evento. De forma predeterminada, todas las categorías de información se seleccionan automáticamente para los eventos que se especifiquen.  
  
12. Haga clic en **Básicas** para ocultar las categorías de información.  
  
13. En la pestaña **Proveedores y registros** , en la columna **Nombre** , seleccione **Lesson 3 Log File**. Una vez que haya creado un proveedor de registro para el paquete, si lo desea, puede anular su selección para desactivar temporalmente el registro, sin tener que eliminar un proveedor de registro y crearlo de nuevo.  
  
14. Haga clic en **Aceptar**.  
  
## <a name="next-steps"></a>Pasos siguientes  
[Paso 3: Probar el paquete del tutorial de la lección 3](../integration-services/lesson-3-3-testing-the-lesson-3-tutorial-package.md)  
  
