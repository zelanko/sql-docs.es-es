---
title: 'Tarea 2: Cargar datos de proveedor en MDS con el complemento MDS para Excel | Documentos de Microsoft'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 598deb57-e0cc-4e0a-aeb1-94432c094c67
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 1831fc9ea79027e24d752d05e3b50d3a58d6e06f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36105287"
---
# <a name="task-2-uploading-supplier-data-to-mds-using-mds-add-in-for-excel"></a>Tarea 2: cargar datos de proveedor en MDS con el complemento MDS para Excel
  En esta tarea, publicará los datos limpios y de proveedor a **MDS** mediante la **el complemento MDS para Excel**. Crear una entidad denominada **proveedor** en el **proveedores** modelo que creó en la lección anterior. La entidad tendrá un atributo para cada columna del archivo de Excel. Los atributos de código y el nombre de la entidad proveedor corresponden a la **SupplierID** y **Supplier Name** columnas en Excel.  
  
1.  Abra **limpios y coincidentes Suppliers.xls** en **Excel**.  
  
2.  Presione **CTRL+A** para seleccionar todos los datos. Es **importante** que seleccione todos los datos en la hoja de cálculo.  
  
3.  Haga clic en **Datos maestros** en la barra de menús.  
  
4.  Haga clic en **crear entidad** botón en la cinta de opciones.  
  
     ![Excel - pestaña de datos maestros - botón Crear entidad](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-01.jpg "Excel - pestaña de datos maestros - botón Crear entidad")  
  
5.  En el cuadro de diálogo **Administrar conexiones** , si no ve la conexión al **servidor MDS local** bajo **Conexiones existentes**, haga lo siguiente:  
  
    1.  Seleccione **Crear una nueva conexión**y haga clic en el botón **Nuevo** .  
  
    2.  En el **agregar nueva conexión** cuadro de diálogo, escriba **servidor MDS Local** para **descripción** y **http://localhost/MDS** para  **Dirección del servidor MDS**y haga clic en **Aceptar** para cerrar el cuadro de diálogo.  
  
6.  En **administrar conexiones** cuadro de diálogo, seleccione **servidor MDS Local** (http://localhost/MDS), haga clic en **probar** para probar la conexión. Haga clic en **Aceptar** en el cuadro de mensaje.  
  
7.  Haga clic en **conectar** para conectarse al servidor de MDS.  
  
8.  En el **crear entidad** cuadro de diálogo, seleccione **proveedores** para el **modelo**.  
  
9. Asegúrese de que **VERSION_1** se selecciona para **versión**.  
  
10. Escriba **proveedor** para **nuevo nombre de entidad**.  
  
11. Seleccione **SupplierID** para **la columna que contiene un identificador único** campo (también puede generar un código automáticamente). Básicamente, esto asigna la **SupplierID** columna en **Excel** a la **código** atributo de **proveedor** entidad.  
  
12. Seleccione **Supplier Name** para **la columna que contiene nombres** campo. Esto asigna la **Supplier Name** columna en **Excel** a la **nombre** atributo de la **proveedor** entidad. El **código** y **nombre** atributos son obligatorios para una entidad en MDS.  
  
     ![Crear cuadro de diálogo entidad](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-02.jpg "Crear cuadro de diálogo de entidad")  
  
13. Haga clic en **Aceptar** para crear la entidad en MDS, publicar los datos maestros en la entidad y cerrar **crear entidad** cuadro de diálogo.  
  
14. Ahora, debería ver una nueva hoja denominada **proveedor**, que es el nombre de la entidad, que se agrega a la hoja de cálculo de Excel y en la parte superior de la hoja de cálculo debe ver que la hoja de cálculo está conectado al servidor de MDS. Tenga en cuenta que la hoja de cálculo original (titulada **Sheet1**) sigue existiendo.  
  
     ![Excel - pestañas proveedor y Hoja1](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-03.jpg "Excel - pestañas proveedor y Hoja1")  
  
     ![Excel - muestra los detalles de conexión de MDS](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-04.jpg "Excel - muestra los detalles de conexión de MDS")  
  
15. Mantener **Excel** abrir.  
  
## <a name="next-task"></a>Tarea siguiente  
 [Tarea 3: Comprobar los datos en Master Data Manager](../../2014/tutorials/task-3-verifying-the-data-in-master-data-manager.md)  
  
  