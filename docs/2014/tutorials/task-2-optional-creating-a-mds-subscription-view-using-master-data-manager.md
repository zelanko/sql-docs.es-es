---
title: 'Tarea 2 (opcional): Crear una vista de suscripciones de MDS con Master Data Manager | Documentos de Microsoft'
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
ms.assetid: f3da8219-e0cb-4848-95ca-285a76ec1ba9
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 4883d4f5c7bef05de9625c2fcb7bac235c0306e7
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36203315"
---
# <a name="task-2-optional-creating-a-mds-subscription-view-using-master-data-manager"></a>Tarea 2 (opcional): crear una vista de suscripciones de MDS con Master Data Manager
  En esta tarea, creará una vista de suscripciones para exponer el **proveedor** entidad en el **proveedores** modelo para otras aplicaciones. No use esta vista en la versión actual del tutorial.  
  
1.  Cambie a la página principal de **Master Data Manager** ([http://localhost/MDS](http://localhost/MDS)), haga clic en **SQL Server 2012 Master Data Services** en la parte superior.  
  
2.  Haga clic en **administración de integraciones**.  
  
3.  Haga clic en **crear vistas** en la barra de menús.  
  
     ![Agregue un nuevo botón de vista de suscripción](../../2014/tutorials/media/et-creatingamdssubscriptionviewusingmdm-01.jpg "agregar un nuevo botón de vista de suscripción")  
  
4.  Haga clic en **+ (signo más)** icono en la barra de herramientas para crear una vista de suscripciones.  
  
5.  En el **Crear vista de suscripciones** panel, escriba **proveedores** para **nombre de la vista de suscripción**.  
  
6.  Seleccione **Proveedores** en **Modelo**.  
  
7.  Seleccione **VERSION_1** en **Versión**.  
  
8.  Seleccione **proveedor** para **entidad**.  
  
9. Seleccione **miembros hoja** para **formato**.  
  
     ![Botón de vista de suscripción guardar](../../2014/tutorials/media/et-creatingamdssubscriptionviewusingmdm-02.jpg "guardar botón de vista de suscripción")  
  
10. Haga clic en **guardar** en la barra de herramientas para guardar la vista de suscripción. Esta acción crea una vista en SQL Server denominada **proveedores**. Puede comprobarlo con SQL Server Management Studio (SSMS).  
  
## <a name="next-step"></a>Paso siguiente  
 [Tarea 3 &#40;opcional&#41;: revisar las vistas de suscripción](task-3-optional-reviewing-the-subscription-views.md)  
  
  