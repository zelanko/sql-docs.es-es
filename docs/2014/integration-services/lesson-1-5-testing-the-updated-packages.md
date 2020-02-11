---
title: 'Paso 5: Probar los paquetes actualizados | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 683e52e5-1c7e-49ab-9ffe-6a450a1c5776
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 979c2b792d7c56dcdb9fadde112c7e6bff789c15
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62767630"
---
# <a name="step-5-testing-the-updated-packages"></a>Paso 5: Probar los paquetes actualizados
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
 [Lección 2: Crear el paquete de implementación](../integration-services/lesson-2-create-the-deployment-bundle-in-ssis.md)  
  
![Integration Services icono (pequeño)](media/dts-16.gif "Icono de Integration Services (pequeño)")  **Manténgase al día con Integration Services**<br /> Para obtener las descargas, artículos, ejemplos y vídeos más recientes de Microsoft, así como soluciones seleccionadas de la comunidad, visite la página de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en MSDN:<br /><br /> [Visite la página de Integration Services en MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Para recibir notificaciones automáticas de estas actualizaciones, suscríbase a las fuentes RSS disponibles en la página.  
  
  
