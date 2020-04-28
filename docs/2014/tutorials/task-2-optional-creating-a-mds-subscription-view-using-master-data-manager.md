---
title: 'Tarea 2 (opcional): creación de una vista de suscripciones de MDS con Master Data Manager | Microsoft Docs'
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81484715"
---
# <a name="task-2-optional-creating-a-mds-subscription-view-using-master-data-manager"></a>Tarea 2 (opcional): Creación de una vista de suscripciones de MDS con Master Data Manager
  En esta tarea, creará una vista de suscripciones para exponer la entidad **proveedor** del modelo **proveedores** a otras aplicaciones. No use esta vista en la versión actual del tutorial.  
  
1.  Cambie a la Página principal de **Master Data Manager** (`http://localhost/MDS`) haciendo clic en **SQL Server 2012 Master Data Services** en la parte superior.  
  
2.  Haga clic en **Administración de integraciones**.  
  
3.  Haga clic en **crear vistas** en la barra de menús.  
  
     ![Botón Agregar una nueva vista de suscripción](../../2014/tutorials/media/et-creatingamdssubscriptionviewusingmdm-01.jpg "Botón Agregar una nueva vista de suscripción")  
  
4.  Haga clic en el icono **+ (más)** de la barra de herramientas para crear una vista de suscripciones.  
  
5.  En el panel **crear vista de suscripciones** , escriba **proveedores** de **nombre de vista de suscripciones**.  
  
6.  Seleccione **Proveedores** en **Modelo**.  
  
7.  Seleccione **VERSION_1** en **Versión**.  
  
8.  Seleccione **proveedor** para **entidad**.  
  
9. Seleccione **los miembros hoja** para el **formato**.  
  
     ![Botón Guardar vista de suscripción](../../2014/tutorials/media/et-creatingamdssubscriptionviewusingmdm-02.jpg "Botón Guardar vista de suscripción")  
  
10. Haga clic en **Guardar** en la barra de herramientas para guardar la vista de suscripciones. Esta acción crea una vista en SQL Server **proveedores**con nombre. Puede comprobarlo con SQL Server Management Studio (SSMS).  
  
## <a name="next-step"></a>siguiente paso  
 [Tarea 3 &#40;&#41; opcional: revisar las vistas de suscripciones](task-3-optional-reviewing-the-subscription-views.md)  
  
  
