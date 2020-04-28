---
title: 'Tarea 1 (requisito previo): eliminación de los datos de proveedor en MDS | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 6f0a4287-7fd4-4f18-b7e4-a5191a9d4a3c
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 0290f033be47bec61e9ccce8465892d8cc98608c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81484635"
---
# <a name="task-1-prerequisite-removing-supplier-data-in-mds"></a>Tarea 1 (requisito previo): Eliminación de datos de proveedor en MDS
  En esta tarea, quitará los datos de proveedor almacenados en MDS. En la lección anterior cargó los datos manualmente mediante el **complemento MDS para Excel** . El paquete de SSIS que cree en esta lección cargará los datos en MDS automáticamente. Por tanto, antes de probar el paquete de SSIS, necesita quitar los datos de proveedor de MDS, quitar la jerarquía derivada, quitar las entidades Proveedor y Estado, y crear la entidad Proveedor sin datos.  
  
1.  Inicie **Master Data Manager** navegando hasta `http://localhost/MDS` o el sitio web y la aplicación que especificó al configurar MDS. Si dejó **Master Data Manager** abierto, haga clic en **SQL Server 2012 Master Data Services** en la parte superior para cambiar a la **página principal**.  
  
2.  Haga clic en **Administración del sistema** en la sección **Tareas administrativas** .  
  
3.  Mantenga el mouse sobre **Administrar** en el menú y haga clic en **Jerarquías derivadas**. Necesita eliminar la jerarquía derivada **SuppliersInState** antes de eliminar las entidades del modelo **Proveedores** .  
  
4.  Seleccione **SuppliersInState** en la lista **Jerarquía derivada** y haga clic en el botón **X (Eliminar)** de la barra de herramientas.  
  
5.  Haga clic en **Aceptar** para confirmar la eliminación.  
  
6.  Mantenga el mouse sobre **Administrar** en el menú y haga clic en **Entidades**.  
  
7.  Haga clic en **Proveedor** y, a continuación, haga clic en el botón **Eliminar (X)** de la barra de herramientas para eliminar la entidad. Haga clic en **Aceptar** en los cuadros de mensajes.  
  
8.  Repita el paso anterior para eliminar la entidad **Estado** .  
  
9. No cierre **Master Data Manager**.  
  
10. Cambie a la ventana de Excel que tiene abierto el archivo **Cleansed and Matched Suppliers.xls** . Cambie a la pestaña **Hoja1** en la parte inferior.  
  
11. Seleccione solo la **primera fila con encabezados**. No seleccione ninguna otra fila. Desea crear las entidades basadas en las columnas de Excel pero no desea cargar ningún dato. Por tanto, solo selecciona la primera fila con los encabezados.  
  
12. Haga clic en **Datos maestros** en la barra de menús.  
  
13. Haga clic en **Crear entidad** en la cinta de opciones.  
  
14. En el cuadro de diálogo **Administrar conexiones** , si no ve la conexión al **servidor MDS local** bajo **Conexiones existentes**, haga lo siguiente:  
  
    1.  Seleccione **Crear una nueva conexión**y haga clic en el botón **Nuevo** .  
  
    2.  En el cuadro de diálogo Agregar nueva conexión, escriba **servidor MDS local** para **Descripción** y **http\/:/localhost/MDS** para la **dirección del servidor MDS**y haga clic en **Aceptar** para cerrar el cuadro de diálogo.  
  
15. En el cuadro de diálogo **Administrar conexiones** , seleccione **servidor MDS local** (`http://localhost/MDS`), haga clic en **probar** para probar la conexión. Haga clic en **Aceptar** en el cuadro de mensaje.  
  
16. Haga clic en **Conectar** para establecer una conexión con el servidor MDS.  
  
17. En el cuadro de diálogo **Crear entidad** , haga lo siguiente:  
  
    1.  Confirme que **Rango** está establecido en **$1:$1**.  
  
    2.  Seleccione **Proveedores** en **Modelo**.  
  
    3.  Seleccione **VERSION_1** en **Versión**.  
  
    4.  Escriba **Proveedor** en **Nuevo nombre de entidad**.  
  
    5.  Seleccione **SupplierID** en **Código**.  
  
    6.  Seleccione **Supplier Name** en **Nombre**.  
  
    7.  Haga clic en **Aceptar** para crear la entidad y cerrar el cuadro de diálogo.  
  
18. Cierre **Excel** y **no guarde** el archivo.  
  
19. En **Master Data Manager**, actualice el navegador de Internet y confirme que aparece la entidad **Supplier** en la lista.  
  
20. Vaya a la **página principal** haciendo clic en **SQL Server 2012 Master Data Services** en la parte superior.  
  
21. Confirme que el modelo **Proveedores** está seleccionado en **Modelo** y **VERSION_1** está seleccionado para **Versión**.  
  
22. Haga clic en **Explorador**. Observe que se crea la entidad **Proveedor** con todos los atributos **sin ningún valor**.  
  
## <a name="next-step"></a>siguiente paso  
 [Tarea 2 &#40;&#41; opcional: crear una vista de suscripciones de MDS con Master Data Manager](../../2014/tutorials/task-2-optional-creating-a-mds-subscription-view-using-master-data-manager.md)  
  
  
