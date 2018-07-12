---
title: 'Lección 3: Agregar registro | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 64cd24cc-ba8e-4bd7-b10b-6b80d8b04af6
caps.latest.revision: 24
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c4ad03f67a8a386b3c42697d1060910c277580c3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37164886"
---
# <a name="lesson-3-adding-logging"></a>Lección 3: Agregar registro
  [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] incluye características de registro que permiten supervisar y solucionar los problemas de ejecución de paquetes mediante el seguimiento de eventos de tarea y de contenedor. La características de registro son flexibles, pueden habilitarse en el nivel de paquete o en tareas y contendores individuales del paquete. Puede seleccionar qué eventos deben registrarse y crear varios registros para un único paquete.  
  
 El registro lo proporciona un proveedor de registro. Cada proveedor de registro puede escribir información de registro en distintos formatos y tipos de destino. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] proporciona los siguientes proveedores de registro:  
  
-   Archivo de texto  
  
-   [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]  
  
-   Registro de eventos de Windows  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
-   Archivo XML  
  
 En esta lección, creará una copia del paquete que creó en [lección 2: Agregar bucles](lesson-2-adding-looping-with-ssis.md). Utilizando este nuevo paquete, luego agregará y configurará el registro para supervisar eventos específicos durante la ejecución del paquete. Si no ha finalizado cualquiera de las lecciones anteriores, también puede copiar el paquete de la lección 2 finalizada incluido en el tutorial.  
  
> [!IMPORTANT]  
>  Para este tutorial, se necesita la base de datos de ejemplo **AdventureWorksDW2012** . Para obtener más información acerca de cómo instalar e implementar **AdventureWorksDW2012**, [Reporting Services Product Samples de CodePlex](http://go.microsoft.com/fwlink/p/?LinkID=52691).  
  
## <a name="lesson-tasks"></a>Tareas de la lección  
 Esta lección contiene las siguientes tareas:  
  
-   [Paso 1: Copiar el paquete de la lección 2](lesson-3-1-copying-the-lesson-2-package.md)  
  
-   [Paso 2: Agregar y configurar el registro](lesson-3-2-adding-and-configuring-logging.md)  
  
-   [Paso 3: Probar el paquete del tutorial de la lección 3](../integration-services/lesson-3-3-testing-the-lesson-3-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>Iniciar la lección  
 [Paso 1: Copiar el paquete de la lección 2](lesson-3-1-copying-the-lesson-2-package.md)  
  
  
