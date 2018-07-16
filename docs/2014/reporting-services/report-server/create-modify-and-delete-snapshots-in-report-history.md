---
title: Crear, modificar y eliminar instantáneas del historial de informes | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- snapshots [Reporting Services]
- report snapshots [Reporting Services]
ms.assetid: 5aebbbfa-a8db-462d-8ab9-746fad9525f0
caps.latest.revision: 39
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 8954e5f1959460c8546543e79b2db9cd49c8342b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37270251"
---
# <a name="create-modify-and-delete-snapshots-in-report-history"></a>Crear, modificar y eliminar instantáneas del historial de informes
  El historial de informe es un conjunto de instantáneas de informe. Puede mantener el historial del informe agregando y eliminando instantáneas, o bien modificando las propiedades correspondientes al almacenamiento del historial. Es posible crear el historial del informe de manera manual o programada.  
  
 Para crear el historial del informe, es imprescindible que su asignación de roles incluya la tarea "Administrar historial de informe". Para ver el historial del informe, su asignación de roles debe incluir la tarea "Ver informes". El historial del informe está disponible para todos los usuarios que tienen acceso al informe en cuestión. No es posible habilitar o deshabilitar selectivamente el historial del informe para un subconjunto de usuarios.  
  
 Las instantáneas del historial del informe se identifican por la fecha y la hora de creación. Estos valores de fecha y hora hacen referencia al momento en que se ejecutó la consulta.  
  
## <a name="creating-snapshots-in-report-history"></a>Crear instantáneas en el historial del informe  
 Pueden crearse instantáneas de forma manual o a intervalos programados para cualquier informe compatible con la ejecución desatendida. Para realizar la ejecución de manera desatendida, el informe debe utilizar las credenciales almacenadas o ninguna credencial. Por otra parte, si el informe incluye parámetros, deberá especificar los valores predeterminados que desea utilizar cuando se ejecute el informe. Utilice la página de propiedades del informe para especificar las credenciales almacenadas y los valores de los parámetros. Para más información, vea [Parámetros &#40;página de propiedades del Administrador de informes&#41;](../parameters-properties-page-report-manager.md).  
  
 Cada vez que cree una instantánea de informe, se almacenarán los siguientes elementos junto con la instantánea en la base de datos del servidor de informes:  
  
-   El conjunto de resultados, es decir, los datos del informe recuperados a través de las credenciales indicadas en la página de propiedades Orígenes de datos del informe.  
  
-   La definición de informe subyacente, tal como existe en el momento en que se crea la instantánea. Si la definición de informe se modifica con posterioridad a la toma de la instantánea, ésta no reflejará los cambios efectuados.  
  
-   Los valores de los parámetros que se utilizan para obtener o filtrar el conjunto de resultados.  
  
-   Los recursos incrustados, como las imágenes. Los recursos externos vinculados a un informe no se almacenan con sus instantáneas.  
  
 Los modos posibles de crear un historial del informe y el número de instantáneas de informes que pueden almacenarse vienen determinados por la configuración.  
  
 Si el informe genera algún error, no se creará la instantánea. En cambio, los informes que generan advertencias, pero que logran ejecutarse, sí sirven para generar instantáneas.  
  
## <a name="modifying-properties-and-deleting-report-history"></a>Modificar las propiedades y eliminar el historial del informe  
 Una vez creada la instantánea de un informe, ya no es posible modificarla. Sin embargo, puede modificar las propiedades de manera que se elimine el historial del informe.  
  
 Existen varias maneras de eliminar el historial del informe:  
  
-   Eliminar manualmente cada una de las instantáneas o grupos de instantáneas.  
  
     Puede eliminar las instantáneas de la página Historial en el Administrador de informes. Navegue hasta el informe, haga clic en Historial, active las casillas situadas al lado de las instantáneas que desea eliminar y, a continuación, haga clic en **Eliminar**.  
  
-   Disminuir el límite del historial del informe para reducir el número de instantáneas para almacenar. Es posible establecer el límite del historial del informe para el servidor de informes o para informes concretos. Cuando disminuye el límite, las instantáneas más antiguas se eliminan del historial.  
  
 No se puede eliminar todo el historial del informe almacenado en un servidor de informes mediante una operación masiva.  
  
 El historial del informe también se elimina cuando se elimina un informe. Por ejemplo, si elimina un informe de ventas mensual porque lo va a sustituir por una versión más reciente, también se eliminará todo el historial del informe asociado al informe. Asimismo, si mueve un informe, se moverá también todo su historial con él.  
  
## <a name="see-also"></a>Vea también  
 [Crear historial de informes &#40;modo integrado de Reporting Services en SharePoint&#41;](create-report-history-reporting-services-in-sharepoint-integrated-mode.md)   
 [El Administrador de informes &#40;modo nativo de SSRS&#41;](../report-manager-ssrs-native-mode.md)   
 [Administración de contenido del servidor de informes &#40;modo nativo de SSRS&#41;](report-server-content-management-ssrs-native-mode.md)   
 [Agregar una instantánea al historial del informe &#40;el Administrador de informes&#41;](add-a-snapshot-to-report-history-report-manager.md)   
 [Limitar el historial de informe &#40;Administrador de informes&#41;](../reports/limit-report-history-report-manager.md)  
  
  
