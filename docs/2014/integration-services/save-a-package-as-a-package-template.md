---
title: Guardar un paquete como una plantilla de paquete | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- reusing packages
- templates [Integration Services]
ms.assetid: efe66cec-3933-4f6e-8d35-fe3d300de66c
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 9bf2bfd8cadad08243be765977b68115bf2ae6f6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36102888"
---
# <a name="save-a-package-as-a-package-template"></a>guardar un paquete como una plantilla de paquete
  En este tema se describe cómo designar y usar paquetes personalizados como plantillas cuando se crean nuevos paquetes de Integration Services en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. De forma predeterminada, [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] usa una plantilla de paquetes que crea un paquete vacío cuando se agrega un nuevo paquete a un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . No puede reemplazar esta plantilla predeterminada, pero puede agregar nuevas plantillas.  
  
 Puede designar varios paquetes para utilizar como plantillas. Para poder implementar paquetes personalizados como plantillas, primero debe crear los paquetes.  
  
 Cuando crea paquetes a partir de paquetes personalizados utilizados como plantillas, los nuevos paquetes tienen el mismo nombre y GUID que la plantilla. Para diferenciar los paquetes, debe actualizar el valor de la propiedad `Name` y generar un nuevo GUID para la propiedad `ID`. Para más información, vea [Crear paquetes en herramientas de datos de SQL Server](create-packages-in-sql-server-data-tools.md) y [Establecer las propiedades de paquetes](set-package-properties.md).  
  
### <a name="to-designate-a-custom-package-as-a-package-template"></a>Para designar un paquete personalizado como plantilla de paquetes  
  
1.  En el sistema de archivos, busque el paquete que desea utilizar como plantilla.  
  
2.  Copie el paquete a la carpeta DataTransformationItems. De forma predeterminada, esta carpeta se encuentra en C:\Archivos de programa\Microsoft Visual Studio 9.0\Common7\IDE\PrivateAssemblies\ProjectItems\DataTransformationProject.  
  
3.  Repita los pasos 1 y 2 para los demás paquetes que desee utilizar como plantilla.  
  
### <a name="to-use-a-custom-package-as-a-package-template"></a>Para utilizar un paquete personalizado como plantilla de paquetes  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra el proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en el que desea crear un paquete.  
  
2.  En el Explorador de soluciones, haga clic con el botón derecho en el proyecto, seleccione **Agregar** y, después, haga clic en **Nuevo elemento**.  
  
3.  En el cuadro de diálogo **Agregar nuevo elemento -\<nombre de proyecto>**, haga clic en el paquete que quiera usar como plantilla.  
  
     La lista de plantillas incluye la plantilla de paquetes predeterminada denominada Nuevo paquete de SSIS. El icono de paquete identifica plantillas que se pueden utilizar como plantillas de paquetes.  
  
4.  Haga clic en **Agregar**.  
  
## <a name="see-also"></a>Vea también  
 [Crear paquetes en SQL Server Data Tools](create-packages-in-sql-server-data-tools.md)   
 [Paquetes de Integration Services &#40;SSIS&#41;](../../2014/integration-services/integration-services-ssis-packages.md)  
  
  