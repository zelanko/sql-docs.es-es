---
title: 'Tarea 2: Carga de datos de proveedores a MDS mediante el complemento MDS para Excel Microsoft Docs'
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
ms.openlocfilehash: 4e3cd4cecd88bcad83c6e9f2a59ecd5f225fb02a
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487699"
---
# <a name="task-2-uploading-supplier-data-to-mds-using-mds-add-in-for-excel"></a>Tarea 2: Carga de datos de proveedor en MDS con el complemento MDS para Excel
  En esta tarea, publicará los datos limpiados y del proveedor en **MDS** mediante el **complemento MDS para Excel**. Cree una entidad denominada **Proveedor** en el modelo **Proveedores** que creó en la lección anterior. La entidad tendrá un atributo para cada columna del archivo de Excel. Los atributos Code y Name de la entidad Supplier corresponden a las columnas **SupplierID** y **Supplier Name** en Excel.  
  
1.  Abra **Proveedores limpios y coincidentes.xls** en **Excel**.  
  
2.  Presione **CTRL+A** para seleccionar datos completos. Es **importante** que seleccione todos los datos de la hoja de cálculo.  
  
3.  Haga clic en **Datos maestros** en la barra de menús.  
  
4.  Haga clic en el botón **Crear entidad** en la cinta de opciones.  
  
     ![Excel - Pestaña de datos maestros - Botón Crear entidad](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-01.jpg "Excel - Pestaña de datos maestros - Botón Crear entidad")  
  
5.  En el cuadro de diálogo **Administrar conexiones** , si no ve la conexión al **servidor MDS local** bajo **Conexiones existentes**, haga lo siguiente:  
  
    1.  Seleccione **Crear una nueva conexión**y haga clic en el botón **Nuevo** .  
  
    2.  En el cuadro de diálogo **Agregar nueva conexión,** escriba **Servidor MDS local** para **Descripción** y **http:\//localhost/MDS** para la dirección del **servidor MDS**y haga clic en **Aceptar** para cerrar el cuadro de diálogo.  
  
6.  En el cuadro de diálogo **Administrar conexiones,** seleccione **Servidor MDS local** (`http://localhost/MDS`), haga clic en **Probar** para probar la conexión. Haga clic en **Aceptar** en el cuadro de mensaje.  
  
7.  Haga clic en **Conectar** para conectarse al servidor MDS.  
  
8.  En el cuadro de diálogo **Crear entidad** , seleccione **Proveedores** para el **modelo**.  
  
9. Asegúrese de que **VERSION_1** está seleccionado para **Versión**.  
  
10. Escriba **Proveedor** para **Nuevo nombre**de entidad .  
  
11. Seleccione **SupplierID** para **la columna que contiene un** campo de identificador único (también puede generar un código automáticamente). Básicamente, está asignando la columna **SupplierID** en **Excel** al atributo **Code** de la entidad **Supplier.**  
  
12. Seleccione **Nombre del proveedor** para el campo Nombre de la **columna.** Básicamente, está asignando la columna Nombre de **proveedor** en **Excel** al atributo **Nombre** de la entidad **Proveedor.** Los atributos **Code** y **Name** son atributos obligatorios para una entidad en MDS.  
  
     ![Cuadro de diálogo Crear entidad](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-02.jpg "Cuadro de diálogo Crear entidad")  
  
13. Haga clic en **Aceptar** para crear la entidad en MDS, publicar los datos maestros en la entidad y cerrar el cuadro de diálogo **Crear entidad.**  
  
14. Ahora, debería ver una nueva hoja titulada **Proveedor**, que es el nombre de la entidad, agregada a su hoja de cálculo de Excel y en la parte superior de la hoja de trabajo debería ver que la hoja de trabajo está conectada al servidor MDS. Observe que la hoja de cálculo original (titulada **Sheet1**) todavía existe.  
  
     ![Excel - Pestañas Proveedor y Hoja1](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-03.jpg "Excel - Pestañas Proveedor y Hoja1")  
  
     ![Excel - Mostrar detalles de conexión MDS](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-04.jpg "Excel - Mostrar detalles de conexión MDS")  
  
15. Mantenga **Excel** abierto.  
  
## <a name="next-task"></a>Tarea siguiente  
 [Tarea 3: Comprobación de los datos en Master Data Manager](../../2014/tutorials/task-3-verifying-the-data-in-master-data-manager.md)  
  
  
