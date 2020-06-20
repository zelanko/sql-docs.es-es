---
title: Guardar un paquete como una plantilla de paquete | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- reusing packages
- templates [Integration Services]
ms.assetid: efe66cec-3933-4f6e-8d35-fe3d300de66c
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 84eb956d8a973cf1186eb8f7454c5a8dd8f0709d
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84964263"
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
  
3.  En el cuadro de diálogo **agregar \<project name> nuevo elemento-** , haga clic en el paquete que desea utilizar como plantilla.  
  
     La lista de plantillas incluye la plantilla de paquetes predeterminada denominada Nuevo paquete de SSIS. El icono de paquete identifica plantillas que se pueden utilizar como plantillas de paquetes.  
  
4.  Haga clic en **Agregar**.  
  
## <a name="see-also"></a>Consulte también  
 [Crear paquetes en SQL Server Data Tools](create-packages-in-sql-server-data-tools.md)   
 [Paquetes de Integration Services &#40;SSIS&#41;](../../2014/integration-services/integration-services-ssis-packages.md)  
  
  
