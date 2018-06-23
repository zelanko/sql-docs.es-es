---
title: 'Tarea 16: Comprobar con Master Data Manager | Documentos de Microsoft'
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
ms.assetid: 57ad9d3e-8f95-4df6-af01-c291ccf49164
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 36220f21f3e2e28d75ff546857fd87b1e71436f1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36107530"
---
# <a name="task-16-verifying-with-master-data-manager"></a>Tarea 16: comprobar con Master Data Manager
  En esta tarea, comprobará el estado del trabajo por lotes enviado por el paquete de SSIS y comprobará que los datos se cargaron en el servidor de MDS con Master Data Manager.  
  
1.  Iniciar **Master Data Manager** ([http://localhost/MDS](http://localhost/MDS)). Si ya está abierto, haga clic en **Microsoft SQL Server Master Data Services** en la parte superior para cambiar a la **página principal**.  
  
2.  Haga clic en **administración de integraciones**.  
  
3.  Observe que hay un lote con denominado **EIMBatch** que ha enviado en la lista. Haga clic en **importar datos** en la barra de menús si no ve la pantalla siguiente.  
  
     ![Lote EIM](../../2014/tutorials/media/et-verifyingwithmasterdatamanager.jpg "lote EIM")  
  
4.  Cambie a la página principal haciendo clic en **SQL Server 2012 Master Data Services** en la parte superior.  
  
5.  Asegúrese de que **proveedores** modelo está seleccionado para **modelo** y **VERSION_1** se selecciona para **versión**y haga clic en  **El Explorador de**.  
  
6.  Puede ver el paquete de datos de SSIS importado en MDS. Los datos deben estar limpios y no tener duplicados **código** valores (Nota: **SupplierID** columna en Excel corresponde a **código** atributo de entidad de proveedor en MDS).  
  
## <a name="next-step"></a>Paso siguiente  
 [Tarea 17: Revisar el proyecto de limpieza de DQS creado por el paquete SSIS](../../2014/tutorials/task-17-reviewing-dqs-cleansing-project-created-by-the-ssis-package.md)  
  
  