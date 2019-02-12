---
title: 'Tarea 16: Comprobar con Master Data Manager | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 57ad9d3e-8f95-4df6-af01-c291ccf49164
author: leolimsft
ms.author: lle
manager: craigg
ms.openlocfilehash: 3b9e24e062695c3b8b4c1aacd37b464fafd99558
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56023606"
---
# <a name="task-16-verifying-with-master-data-manager"></a>Tarea 16: comprobar con Master Data Manager
  En esta tarea, comprobará el estado del trabajo por lotes enviado por el paquete de SSIS y comprobará que los datos se cargaron en el servidor de MDS con Master Data Manager.  
  
1.  Iniciar **Master Data Manager** ([http://localhost/MDS](http://localhost/MDS)). Si ya está abierto, haga clic en **Microsoft SQL Server Master Data Services** en la parte superior para cambiar a la **página principal**.  
  
2.  Haga clic en **administración de integraciones**.  
  
3.  Observe que hay un lote con denominado **EIMBatch** que ha enviado en la lista. Haga clic en **importar datos** en la barra de menús si no ve la pantalla siguiente.  
  
     ![Lote EIM](../../2014/tutorials/media/et-verifyingwithmasterdatamanager.jpg "lote EIM")  
  
4.  Cambie a la página principal haciendo clic con el **SQL Server 2012 Master Data Services** en la parte superior.  
  
5.  Asegúrese de que **proveedores** modelo está seleccionado para **modelo** y **VERSION_1** está seleccionada para **versión**y haga clic en  **Explorador**.  
  
6.  Puede ver el paquete de datos de SSIS importado en MDS. Los datos deben estar limpios y tener ningún **código** valores (tenga en cuenta: **SupplierID** columna en Excel corresponde a **código** atributo de entidad del proveedor en MDS).  
  
## <a name="next-step"></a>Paso siguiente  
 [Tarea 17: Revisar el proyecto de limpieza de DQS creado por el paquete SSIS](../../2014/tutorials/task-17-reviewing-dqs-cleansing-project-created-by-the-ssis-package.md)  
  
  
