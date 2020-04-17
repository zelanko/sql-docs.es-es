---
title: 'Tarea 16: Verificación con el Administrador de datos maestros ( Master Data Manager) Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 57ad9d3e-8f95-4df6-af01-c291ccf49164
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: d9828c02625ae2bc5a85859577a237b4c4fa99c5
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2020
ms.locfileid: "81484685"
---
# <a name="task-16-verifying-with-master-data-manager"></a>Tarea 16: Comprobación con Master Data Manager
  En esta tarea, comprobará el estado del trabajo por lotes enviado por el paquete de SSIS y comprobará que los datos se cargaron en el servidor de MDS con Master Data Manager.  
  
1.  Inicie Master Data`http://localhost/MDS` **Manager** ( ). Si ya está abierto, haga clic en **Microsoft SQL Server Master Data Services** en la parte superior para cambiar a la página **principal.**  
  
2.  Haga clic en **Administración de integración**.  
  
3.  Observe que hay un lote con el nombre **EIMBatch** que envió en la lista. Haga clic en **Importar datos** en la barra de menús si no ve la siguiente pantalla.  
  
     ![Lote EIM](../../2014/tutorials/media/et-verifyingwithmasterdatamanager.jpg "Lote EIM")  
  
4.  Vuelva a la página principal haciendo clic en **SQL Server 2012 Master Data Services** en la parte superior.  
  
5.  Asegúrese de que el modelo **Proveedores** está seleccionado para **Modelo** y **VERSION_1** está seleccionado para **Versión**y haga clic en **Explorador**.  
  
6.  Puede ver el paquete de datos de SSIS importado en MDS. Los datos deben limpiarse y no tener valores de **código** duplicados (Nota: la columna **SupplierID** en Excel corresponde al atributo **Code** de la entidad Supplier en MDS).  
  
## <a name="next-step"></a>siguiente paso  
 [Tarea 17: Revisión del proyecto de limpieza de DQS creado por el paquete SSIS](../../2014/tutorials/task-17-reviewing-dqs-cleansing-project-created-by-the-ssis-package.md)  
  
  
