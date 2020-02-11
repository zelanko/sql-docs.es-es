---
title: 'Tarea 2: carga de datos de proveedor en MDS mediante Complemento MDS para Excel | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 598deb57-e0cc-4e0a-aeb1-94432c094c67
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 57a5044ccee040ef1eba95925c689f48739c259f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "65484659"
---
# <a name="task-2-uploading-supplier-data-to-mds-using-mds-add-in-for-excel"></a>Tarea 2: cargar datos de proveedor en MDS con el complemento MDS para Excel
  En esta tarea, publicará los datos limpios y de proveedor en **MDS** mediante el **complemento MDS para Excel**. Cree una entidad denominada **Supplier** en el modelo **proveedores** que creó en la lección anterior. La entidad tendrá un atributo para cada columna del archivo de Excel. Los atributos Code y Name de la entidad Supplier corresponden a las columnas **SupplierID** y **Supplier Name** de Excel.  
  
1.  Abra **limpiar y coincidentes proveedores. xls** en **Excel**.  
  
2.  Presione **Ctrl +** a para seleccionar todos los datos. Es **importante** que seleccione todos los datos en la hoja de cálculo.  
  
3.  Haga clic en **Datos maestros** en la barra de menús.  
  
4.  Haga clic en el botón **crear entidad** de la cinta de opciones.  
  
     ![Excel - Pestaña de datos maestros - Botón Crear entidad](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-01.jpg "Excel - Pestaña de datos maestros - Botón Crear entidad")  
  
5.  En el cuadro de diálogo **Administrar conexiones** , si no ve la conexión al **servidor MDS local** bajo **Conexiones existentes**, haga lo siguiente:  
  
    1.  Seleccione **Crear una nueva conexión**y haga clic en el botón **Nuevo** .  
  
    2.  En el cuadro de diálogo **Agregar nueva conexión** , escriba **servidor MDS local** para **Descripción** y **http://localhost/MDS** para **dirección del servidor MDS**, y haga clic en **Aceptar** para cerrar el cuadro de diálogo.  
  
6.  En el cuadro de diálogo **Administrar conexiones** , seleccione **servidor MDS local** (http://localhost/MDS), haga clic en **probar** para probar la conexión. Haga clic en **Aceptar** en el cuadro de mensaje.  
  
7.  Haga clic en **conectar** para conectarse al servidor de MDS.  
  
8.  En el cuadro de diálogo **crear entidad** , seleccione **proveedores** para el **modelo**.  
  
9. Asegúrese de que **VERSION_1** está seleccionado para **versión**.  
  
10. Escriba **proveedor** para **el nuevo nombre de entidad**.  
  
11. Seleccione **IdProveedor** en **la columna que contiene un identificador único** (también puede generar un código automáticamente). Básicamente está asignando la columna **SupplierID** en **Excel** al atributo **code** de la entidad **Supplier** .  
  
12. Seleccione **nombre de proveedor** para **la columna que contiene el campo nombres** . Básicamente está asignando la columna **Supplier Name** de **Excel** al atributo **Name** de la entidad **Supplier** . Los atributos **code** y **Name** son atributos obligatorios para una entidad en MDS.  
  
     ![Cuadro de diálogo Crear entidad](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-02.jpg "Cuadro de diálogo Crear entidad")  
  
13. Haga clic en **Aceptar** para crear la entidad en MDS, publicar los datos maestros en la entidad y cerrar el cuadro de diálogo **crear entidad** .  
  
14. Ahora debería ver una nueva hoja titulada **proveedor**, que es el nombre de la entidad, agregada a la hoja de cálculo de Excel y en la parte superior de la hoja de cálculo debería ver que la hoja de cálculo está conectada al servidor MDS. Observe que la hoja de cálculo original (titulada **Hoja1**) sigue existiendo.  
  
     ![Excel - Pestañas Proveedor y Hoja1](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-03.jpg "Excel - Pestañas Proveedor y Hoja1")  
  
     ![Excel - Mostrar detalles de conexión MDS](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-04.jpg "Excel - Mostrar detalles de conexión MDS")  
  
15. Mantenga abierto **Excel** .  
  
## <a name="next-task"></a>Tarea siguiente  
 [Tarea 3: comprobar los datos en Master Data Manager](../../2014/tutorials/task-3-verifying-the-data-in-master-data-manager.md)  
  
  
