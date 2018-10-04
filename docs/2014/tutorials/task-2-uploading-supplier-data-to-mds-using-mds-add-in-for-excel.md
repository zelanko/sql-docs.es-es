---
title: 'Tarea 2: Cargar datos de proveedor en MDS con el complemento MDS para Excel | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.topic: conceptual
ms.assetid: 598deb57-e0cc-4e0a-aeb1-94432c094c67
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 36e50a34f708bc13da489591d73ca0521cdb5a6b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48101215"
---
# <a name="task-2-uploading-supplier-data-to-mds-using-mds-add-in-for-excel"></a>Tarea 2: cargar datos de proveedor en MDS con el complemento MDS para Excel
  En esta tarea, publica los datos limpios y de proveedor a **MDS** utilizando el **complemento MDS para Excel**. Crear una entidad denominada **proveedor** en el **proveedores** modelo que creó en la lección anterior. La entidad tendrá un atributo para cada columna del archivo de Excel. Los atributos de código y el nombre de la entidad proveedor corresponden a la **SupplierID** y **Supplier Name** las columnas de Excel.  
  
1.  Abra **limpios y Matched Suppliers.xls** en **Excel**.  
  
2.  Presione **CTRL+A** para seleccionar todos los datos. Es **importante** que seleccione todos los datos en la hoja de cálculo.  
  
3.  Haga clic en **Datos maestros** en la barra de menús.  
  
4.  Haga clic en **crear entidad** botón en la cinta de opciones.  
  
     ![Excel - pestaña de datos maestros - botón Crear entidad](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-01.jpg "Excel - pestaña de datos maestros - botón Crear entidad")  
  
5.  En el cuadro de diálogo **Administrar conexiones** , si no ve la conexión al **servidor MDS local** bajo **Conexiones existentes**, haga lo siguiente:  
  
    1.  Seleccione **Crear una nueva conexión**y haga clic en el botón **Nuevo** .  
  
    2.  En el **agregar nueva conexión** cuadro de diálogo, escriba **servidor MDS Local** para **descripción** y **http://localhost/MDS** para  **Dirección del servidor MDS**y haga clic en **Aceptar** para cerrar el cuadro de diálogo.  
  
6.  En **administrar conexiones** cuadro de diálogo, seleccione **servidor MDS Local** (http://localhost/MDS), haga clic en **probar** para probar la conexión. Haga clic en **Aceptar** en el cuadro de mensaje.  
  
7.  Haga clic en **Connect** para conectarse al servidor de MDS.  
  
8.  En el **crear entidad** cuadro de diálogo, seleccione **proveedores** para el **modelo**.  
  
9. Asegúrese de que **VERSION_1** está seleccionada para **versión**.  
  
10. Escriba **proveedor** para **nuevo nombre de entidad**.  
  
11. Seleccione **SupplierID** para **la columna que contiene un identificador único** campo (también puede generar un código automáticamente). Básicamente, esto se asigna el **SupplierID** columna en **Excel** a la **código** atributo de **proveedor** entidad.  
  
12. Seleccione **Supplier Name** para **la columna que contiene los nombres** campo. Básicamente, esto se asigna el **Supplier Name** columna en **Excel** a la **nombre** atributo de la **proveedor** entidad. El **código** y **nombre** atributos son obligatorios para una entidad en MDS.  
  
     ![Crear el cuadro de diálogo entidad](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-02.jpg "crear el cuadro de diálogo entidad")  
  
13. Haga clic en **Aceptar** para crear la entidad en MDS, publicar los datos maestros en la entidad y cerrar **crear entidad** cuadro de diálogo.  
  
14. Ahora, debería ver una nueva hoja denominada **proveedor**, que es el nombre de la entidad, se agrega a la hoja de cálculo de Excel y en la parte superior de la hoja de cálculo verá que la hoja de cálculo está conectado al servidor de MDS. Tenga en cuenta que la hoja de cálculo original (titulada **Sheet1**) sigue existiendo.  
  
     ![Excel - pestañas proveedor y Hoja1](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-03.jpg "Excel - pestañas proveedor y Hoja1")  
  
     ![Excel - mostrar detalles de conexión de MDS](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-04.jpg "Excel - mostrar detalles de conexión de MDS")  
  
15. Mantener **Excel** abrir.  
  
## <a name="next-task"></a>Tarea siguiente  
 [Tarea 3: Comprobar los datos en Master Data Manager](../../2014/tutorials/task-3-verifying-the-data-in-master-data-manager.md)  
  
  
