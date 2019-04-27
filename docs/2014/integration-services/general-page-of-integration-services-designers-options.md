---
title: Página general | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.Business_Intelligence_Designers.Data_Transformation_Designers.General
ms.assetid: d695690a-923b-4036-945e-7621e8651deb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: f27ec0c9fe8078bb11a48114a3d456793271853d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62768291"
---
# <a name="general-page"></a>Página General
  Utilice la página **General** de la página **Diseñadores de Integration Services** en el cuadro de diálogo **Opciones** con el fin de especificar las opciones para cargar, mostrar y actualizar los paquetes.  
  
 Para abrir la página **General** , en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], en el menú **Herramientas** , haga clic en **Opciones**, expanda **Diseñadores de Business Intelligence**y seleccione **Diseñadores de Integration Services**.  
  
## <a name="options"></a>Opciones  
 **Comprobar la firma digital al cargar un paquete**  
 Seleccione para que [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] compruebe la firma digital al cargar un paquete. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] solo realizará la comprobación si la firma digital está presente, es válida y procede de un origen de confianza. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] no comprobará si el paquete ha cambiado desde que se firmó.  
  
 Si establece el valor del Registro **BlockedSignatureStates** , este valor del Registro invalida la opción **Comprobar la firma digital al cargar un paquete** . Para más información, vea [Implementar una directiva de firma estableciendo un valor del Registro](implement-a-signing-policy-by-setting-a-registry-value.md).  
  
 Para más información sobre los paquetes y los certificados digitales, vea [Identificar el origen de paquetes con firmas digitales](security/identify-the-source-of-packages-with-digital-signatures.md).  
  
 **Mostrar una advertencia si un paquete está sin firmar**  
 Seleccione esta opción para mostrar una advertencia cuando se carga un paquete que está sin firmar.  
  
 **Mostrar etiquetas de restricción de precedencia**  
 Seleccione la etiqueta que quiere que se muestre (Correcto, Error o Conclusión) en restricciones de precedencia al visualizar paquetes en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
 **Lenguaje de scripting**  
 Seleccione el lenguaje de scripting predeterminado para las nuevas tareas Script y los componentes Script.  
  
 **Actualizar las cadenas de conexión para reflejar los nuevos nombres de proveedor**  
 Al abrir o actualizar paquetes de [!INCLUDE[ssISversion2005](../includes/ssisversion2005-md.md)] , actualice las cadenas de conexión para que usen los nombres de los proveedores siguientes para la versión actual de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]:  
  
-   [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] Proveedor OLE DB  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client  
  
 El Asistente para actualizar paquetes de [!INCLUDE[ssIS](../includes/ssis-md.md)] solo actualiza las cadenas de conexión que se almacenan en administradores de conexiones. No actualiza las cadenas de conexión que se construyen dinámicamente utilizando el lenguaje de expresiones de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] o código en una tarea Script.  
  
 **Crear el identificador del nuevo paquete**  
 Al actualizar paquetes de [!INCLUDE[ssISversion2005](../includes/ssisversion2005-md.md)] , cree los identificadores de los paquetes nuevos para las versiones actualizadas de los paquetes.  
  
## <a name="see-also"></a>Vea también  
 [Información general sobre seguridad &#40;Integration Services&#41;](security/security-overview-integration-services.md)   
 [Ampliar paquetes con scripting](extending-packages-scripting/extending-packages-with-scripting.md)  
  
  
