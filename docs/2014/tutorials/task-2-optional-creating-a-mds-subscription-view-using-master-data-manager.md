---
title: 'Tarea 2 (Opcional): Creación de una vista de suscripción de MDS mediante el Administrador de datos maestros. Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: f3da8219-e0cb-4848-95ca-285a76ec1ba9
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: cc923792adc3fefb5ebaab9e225169648394c71f
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2020
ms.locfileid: "81484715"
---
# <a name="task-2-optional-creating-a-mds-subscription-view-using-master-data-manager"></a>Tarea 2 (opcional): Creación de una vista de suscripciones de MDS con Master Data Manager
  En esta tarea, creará una vista de suscripción para exponer la entidad **Supplier** en el modelo **Suppliers** a otras aplicaciones. No use esta vista en la versión actual del tutorial.  
  
1.  Cambie a la página principal de Administrador de **datos maestrosMaster Data Manager** (`http://localhost/MDS`) haciendo clic en SQL Server **2012 Master Data Services** en la parte superior.  
  
2.  Haga clic en **Administración de integración**.  
  
3.  Haga clic en **Crear vistas** en la barra de menús.  
  
     ![Botón Agregar una nueva vista de suscripción](../../2014/tutorials/media/et-creatingamdssubscriptionviewusingmdm-01.jpg "Botón Agregar una nueva vista de suscripción")  
  
4.  Haga clic en el icono **+ (Más)** en la barra de herramientas para crear una vista de suscripción.  
  
5.  En el panel Crear vista de **suscripción** , escriba **Proveedores** para el nombre de **la vista Suscripción**.  
  
6.  Seleccione **Proveedores** en **Modelo**.  
  
7.  Seleccione **VERSION_1** en **Versión**.  
  
8.  Seleccione **Proveedor** para **Entidad**.  
  
9. Seleccione **Miembros hoja** para **Formato**.  
  
     ![Botón Guardar vista de suscripción](../../2014/tutorials/media/et-creatingamdssubscriptionviewusingmdm-02.jpg "Botón Guardar vista de suscripción")  
  
10. Haga clic en **Guardar** en la barra de herramientas para guardar la vista de suscripción. Esta acción crea una vista en SQL Server denominada **Proveedores**. Puede comprobarlo con SQL Server Management Studio (SSMS).  
  
## <a name="next-step"></a>siguiente paso  
 [Tarea 3 &#40;&#41; opcional: Revisión de las vistas de suscripción](task-3-optional-reviewing-the-subscription-views.md)  
  
  
