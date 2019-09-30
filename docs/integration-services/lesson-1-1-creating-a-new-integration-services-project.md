---
title: 'Paso 1: Creación de un proyecto de Integration Services | Microsoft Docs'
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: f14521b5-941e-443b-8f5e-385f98e37fbf
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 74e56788741b36e68884db823fa46eb24856081e
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/26/2019
ms.locfileid: "71296125"
---
# <a name="lesson-1-1-create-a-new-integration-services-project"></a>Lección 1-1: Crear un proyecto de Integration Services

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



El primer paso al crear un paquete en [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] es crear un proyecto [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . En este proyecto de ejemplo se incluyen plantillas para los orígenes de datos, las vistas de orígenes de datos y los paquetes que pueden constituir una solución de transformación de datos.  
  
Los paquetes que crea en este tutorial de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] interpretan los valores de los datos dependientes de la configuración regional. Si el equipo no está configurado para usar la opción de configuración regional **Inglés (Estados Unidos)** , debe establecer propiedades adicionales en el paquete. 

Los paquetes que se usan en las lecciones 2 a 6 se copian del paquete que crea en esta lección.  
  
> [!NOTE]  
> Si todavía no lo ha hecho, consulte los [requisitos previos de la lección 1](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md#prerequisites).

## <a name="create-a-new-integration-services-project"></a>Crear un proyecto de Integration Services  
  
1.  En el menú **Inicio** de Windows, busque y seleccione **Visual Studio (SSDT)** .  
  
2.  En Visual Studio, seleccione **Archivo** > **Nuevo** > **Proyecto** para crear un proyecto de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)].  
  
3.  En el cuadro de diálogo **Nuevo proyecto**, expanda el nodo **Business Intelligence** en **Instalado** y seleccione **Proyecto de Integration Services** en el panel **Plantillas**.  
  
4.  En el cuadro **Nombre** , cambie el nombre predeterminado por **SSIS Tutorial**. Para usar una carpeta que ya existe, desactive la casilla **Crear directorio para la solución**.  
  
5.  Acepte la ubicación predeterminada o seleccione **Examinar** para buscar la carpeta que quiere usar. En el cuadro de diálogo **Ubicación del proyecto**, seleccione la carpeta y, luego, elija **Seleccionar carpeta**.  
  
6.  Seleccione **Aceptar**.  
  
    De forma predeterminada, se crea un paquete vacío, denominado **Package.dtsx** y se agrega al proyecto en **Paquetes SSIS**.  
  
7.  En el **Explorador de soluciones**, haga clic con el botón derecho en **Package.dtsx**, seleccione **Cambiar nombre** y cambie el nombre del paquete predeterminado por **Lesson 1.dtsx**.  
  
## <a name="go-to-next-task"></a>Ir a la tarea siguiente
[Paso 2: Incorporación y configuración de un administrador de conexiones de archivos planos](../integration-services/lesson-1-2-adding-and-configuring-a-flat-file-connection-manager.md)  
  
