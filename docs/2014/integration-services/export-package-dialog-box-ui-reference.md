---
title: Exportar la referencia de interfaz de usuario del cuadro de diálogo de paquete | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.dtsserver.exportpackage.f1
helpviewer_keywords:
- Export Package dialog box
ms.assetid: 3742fe8a-ef57-444d-b2fb-cb25d16bae97
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: ecbe181c790e1d839a0ccd6d7c96849a2e8512c5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36199489"
---
# <a name="export-package-dialog-box-ui-reference"></a>Referencia de la interfaz de usuario del cuadro de diálogo Exportar paquete
  Utilice el cuadro de diálogo **Exportar paquete** , disponible en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], para exportar un paquete de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] a una ubicación diferente y, opcionalmente, modificar el nivel de protección del paquete.  
  
## <a name="options"></a>Opciones  
 **Ubicación del paquete**  
 Seleccione el tipo de almacenamiento al que desea exportar el paquete. Las siguientes opciones están disponibles:  
  
 **SQL Server**  
  
 **Sistema de archivos**  
  
 **Almacén de paquetes SSIS**  
  
 **Server**  
 Escriba un nombre de servidor o seleccione un servidor de la lista.  
  
 **Autenticación**  
 Seleccione Autenticación de Windows o Autenticación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Esta opción solo está disponible si la ubicación de almacenamiento es [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Siempre que sea posible, utilice la autenticación de Windows.  
  
 **Tipo de autenticación**  
 Seleccione un tipo de autenticación.  
  
 **Nombre de usuario.**  
 Si usa la autenticación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , proporcione un nombre de usuario.  
  
 **Contraseña**  
 Si está usando la autenticación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , proporcione una contraseña.  
  
 **Ruta de acceso del paquete**  
 Escriba la ruta de acceso del paquete o haga clic en el botón Examinar **(…)** y busque la carpeta en la que quiera almacenar el paquete.  
  
 **Nivel de protección**  
 Haga clic en el botón Examinar **(…)** y actualice el nivel de protección del cuadro de diálogo **Nivel de protección de paquetes** . Para obtener más información, vea [Nivel de protección de paquetes y del proyecto, cuadro de diálogo](../../2014/integration-services/package-and-project-protection-level-dialog-box.md).  
  
## <a name="see-also"></a>Vea también  
 [Guardar copia del paquete](../../2014/integration-services/save-copy-of-package.md)   
 [Referencia de interfaz de usuario del cuadro de diálogo de importar paquete](../../2014/integration-services/import-package-dialog-box-ui-reference.md)   
 [Guardar paquetes](save-packages.md)   
 [Importar y exportar paquetes &#40;servicio SSIS&#41;](../../2014/integration-services/import-and-export-packages-ssis-service.md)  
  
  