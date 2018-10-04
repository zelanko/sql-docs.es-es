---
title: Guardar copia del paquete | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.savecopyas.f1
helpviewer_keywords:
- Save Copy of Package dialog box
ms.assetid: 7b44c0d7-d8fa-4491-8836-0899f621d3a8
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0cd386cad85726707f1ce3ea9f7931bda4e66c25
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48140505"
---
# <a name="save-copy-of-package"></a>Guardar copia del paquete
  Utilice el cuadro de diálogo **Guardar copia del paquete** , disponible en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], para guardar una copia de un paquete de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] desde [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] en una ubicación diferente y, opcionalmente, modificar el nivel de protección del paquete.  
  
## <a name="options"></a>Opciones  
 **Ubicación del paquete**  
 Seleccione el tipo de ubicación de almacenamiento en que desea guardar la copia del paquete. Las siguientes opciones están disponibles:  
  
 **SQL Server**  
  
 **Sistema de archivos**  
  
 **Almacén de paquetes SSIS**  
  
 **Server**  
 Escriba un nombre de servidor o seleccione un servidor de la lista. Esta opción está disponible solo si la ubicación de almacenamiento es **SQL Server** o **Almacén de paquetes SSIS**.  
  
 **Autenticación**  
 Seleccione Autenticación de Windows o Autenticación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Esta opción solo está disponible si la ubicación de almacenamiento es [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Siempre que sea posible, use la autenticación de Windows.  
  
 **Tipo de autenticación**  
 Seleccione un tipo de autenticación.  
  
 **Nombre de usuario.**  
 Si usa la autenticación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , proporcione un nombre de usuario.  
  
 **Contraseña**  
 Si está usando la autenticación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , proporcione una contraseña.  
  
 **Ruta de acceso del paquete**  
 Escriba la ruta de acceso del paquete o haga clic en el botón Examinar **(…)** y busque la carpeta en la que quiere almacenar el paquete.  
  
 **Nivel de protección**  
 Haga clic en el botón Examinar **(…)** y actualice el nivel de protección del cuadro de diálogo **Nivel de protección de paquetes** . Para obtener más información, vea [Nivel de protección de paquetes y del proyecto, cuadro de diálogo](../../2014/integration-services/package-and-project-protection-level-dialog-box.md).  
  
## <a name="see-also"></a>Vea también  
 [Referencia de interfaz de usuario de cuadro de diálogo de importar paquete](../../2014/integration-services/import-package-dialog-box-ui-reference.md)   
 [Referencia de interfaz de usuario del cuadro de diálogo de paquete de exportación](../../2014/integration-services/export-package-dialog-box-ui-reference.md)   
 [Guardar paquetes](save-packages.md)   
 [Importar y exportar paquetes &#40;servicio SSIS&#41;](../../2014/integration-services/import-and-export-packages-ssis-service.md)  
  
  
