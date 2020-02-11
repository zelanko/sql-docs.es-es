---
title: Referencia de la interfaz de usuario del cuadro de diálogo Exportar paquete | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.dtsserver.exportpackage.f1
helpviewer_keywords:
- Export Package dialog box
ms.assetid: 3742fe8a-ef57-444d-b2fb-cb25d16bae97
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c1cca0a2761f87d6f4f3837df1e9a0bdcc5b91a4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66058909"
---
# <a name="export-package-dialog-box-ui-reference"></a>Referencia de la interfaz de usuario del cuadro de diálogo Exportar paquete
  Utilice el cuadro de diálogo **Exportar paquete** , disponible en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], para exportar un paquete de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] a una ubicación diferente y, opcionalmente, modificar el nivel de protección del paquete.  
  
## <a name="options"></a>Opciones  
 **Ubicación del paquete**  
 Seleccione el tipo de almacenamiento al que desea exportar el paquete. Están disponibles las siguientes opciones:  
  
 **SQL Server**  
  
 **Sistema de archivos**  
  
 **Almacenamiento de paquetes SSIS**  
  
 **Server**  
 Escriba un nombre de servidor o seleccione un servidor de la lista.  
  
 **Autenticación**  
 Seleccione Autenticación de Windows o Autenticación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Esta opción solo está disponible si la ubicación de almacenamiento es [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Siempre que sea posible, utilice la autenticación de Windows.  
  
 **Tipo de autenticación**  
 Seleccione un tipo de autenticación.  
  
 **Nombre de usuario**  
 Si usa la autenticación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , proporcione un nombre de usuario.  
  
 **Contraseña**  
 Si está usando la autenticación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , proporcione una contraseña.  
  
 **Ruta de acceso del paquete**  
 Escriba la ruta de acceso del paquete, o bien haga clic en el botón Examinar **(…)** y busque la carpeta donde quiera guardar el paquete.  
  
 **Nivel de protección**  
 Haga clic en el botón Examinar **(…)** y actualice el nivel de protección en el cuadro de diálogo **Nivel de protección de paquetes**. Para obtener más información, vea [Nivel de protección de paquetes y del proyecto, cuadro de diálogo](../../2014/integration-services/package-and-project-protection-level-dialog-box.md).  
  
## <a name="see-also"></a>Consulte también  
 [Guardar copia del paquete](../../2014/integration-services/save-copy-of-package.md)   
 [Referencia de la interfaz de usuario del cuadro de diálogo Importar paquete](../../2014/integration-services/import-package-dialog-box-ui-reference.md)   
 [Guardar paquetes](save-packages.md)   
 [Importar y exportar paquetes &#40;servicio SSIS&#41;](../../2014/integration-services/import-and-export-packages-ssis-service.md)  
  
  
