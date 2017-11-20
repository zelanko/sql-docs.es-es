---
title: 'Paso 5: Probar los paquetes actualizados | Documentos de Microsoft'
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: integration-services
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: 683e52e5-1c7e-49ab-9ffe-6a450a1c5776
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 55dae3d13775100b6d443dfc8d97948c3f621c01
ms.contentlocale: es-es
ms.lasthandoff: 09/26/2017

---
# <a name="lesson-1-5---testing-the-updated-packages"></a>Lección 1-5-probar los paquetes actualizados
Antes de ir a la siguiente lección, en la que creará el paquete de implementación que se utilizará para instalar los paquetes del tutorial en el equipo de destino, debe probar los paquetes. En esta tarea, ejecutará los paquetes, DataTransfer.dtsx y LoadXMLData, que ha agregado al proyecto Deployment Tutorial y ha ampliado con configuraciones.  
  
Al ejecutar los paquetes, cada ejecutable del paquete se convierte en color verde en cuanto finaliza correctamente. Cuando todos los ejecutables están en verde, el paquete se ha completado correctamente. También puede ver el progreso en la ejecución del paquete en la pestaña **Progreso** .  
  
Si los paquetes no se ejecutan correctamente, debe solucionarlos antes de ir a la siguiente lección.  
  
### <a name="to-run-the-datatransfer-package"></a>Para ejecutar el paquete DataTransfer  
  
1.  En el Explorador de soluciones, haga clic en DataTransfer.dtsx.  
  
2.  En el menú **Depurar** , haga clic en **Iniciar depuración**.  
  
3.  Una vez que se haya completado la ejecución del paquete, en el menú **Depurar** , haga clic en **Detener depuración**.  
  
### <a name="to-run-the-loadxmldata-package"></a>Para ejecutar el paquete LoadXMLData  
  
1.  En el Explorador de soluciones, haga clic en LoadXMLData.dtsx.  
  
2.  En el menú **Depurar** , haga clic en **Iniciar depuración**.  
  
3.  Una vez que se haya completado la ejecución del paquete, en el menú **Depurar** , haga clic en **Detener depuración**.  
  
## <a name="next-lesson"></a>Lección siguiente  
[Lección 2: Crear el paquete de implementación en SSIS](../integration-services/lesson-2-create-the-deployment-bundle-in-ssis.md)  
  
  
  

