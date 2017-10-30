---
title: "Página general de la integración de servicios de diseñadores opciones | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- VS.ToolsOptionsPages.Business_Intelligence_Designers.Data_Transformation_Designers.General
ms.assetid: d695690a-923b-4036-945e-7621e8651deb
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 4a8ade977c971766c8f716ae5f33cac606c8e22d
ms.openlocfilehash: 599665d49b8512ec772ac5ca522cb4e0b7a521ec
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="general-page-of-integration-services-designers-options"></a>Opciones de diseñadores de página general de la integración de servicios
  Utilice la página **General** de la página **Diseñadores de Integration Services** en el cuadro de diálogo **Opciones** con el fin de especificar las opciones para cargar, mostrar y actualizar los paquetes.  
  
 Para abrir la página **General** , en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], en el menú **Herramientas** , haga clic en **Opciones**, expanda **Diseñadores de Business Intelligence**y seleccione **Diseñadores de Integration Services**.  
  
## <a name="options"></a>Opciones  
 **Comprobar la firma digital al cargar un paquete**  
 Seleccione para que [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] compruebe la firma digital al cargar un paquete. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]solo comprobará si la firma digital está presente, es válida y procede de un origen de confianza. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]no comprobará si el paquete se ha cambiado desde que se firmó el paquete.  
  
 Si establece el valor del Registro **BlockedSignatureStates** , este valor del Registro invalida la opción **Comprobar la firma digital al cargar un paquete** . Para más información, vea [Implementar una directiva de firma estableciendo un valor del Registro](../integration-services/packages/implement-a-signing-policy-by-setting-a-registry-value.md).  
  
 Para más información sobre los paquetes y los certificados digitales, vea [Identificar el origen de paquetes con firmas digitales](../integration-services/security/identify-the-source-of-packages-with-digital-signatures.md).  
  
 **Mostrar una advertencia si un paquete está sin firmar**  
 Seleccione esta opción para mostrar una advertencia cuando se carga un paquete que está sin firmar.  
  
 **Mostrar etiquetas de restricción de precedencia**  
 Seleccione qué etiqueta (Correcto, Error o Conclusión) mostrar en restricciones de precedencia al mostrar los paquetes en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
 **Lenguaje de scripting**  
 Seleccione el lenguaje de scripting predeterminado para las nuevas tareas Script y los componentes Script.  
  
 **Actualizar las cadenas de conexión para reflejar los nuevos nombres de proveedor**  
 Al abrir o actualizar [!INCLUDE[ssISversion2005](../includes/ssisversion2005-md.md)] paquetes, actualice las cadenas de conexión para utilizar los nombres de los proveedores siguientes para la versión actual de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)]:  
  
-   Proveedor OLE DB de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client  
  
 El Asistente para actualizar paquetes de [!INCLUDE[ssIS](../includes/ssis-md.md)] solo actualiza las cadenas de conexión que se almacenan en administradores de conexiones. No actualiza las cadenas de conexión que se construyen dinámicamente utilizando el lenguaje de expresiones de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] o código en una tarea Script.  
  
 **Crear el identificador del nuevo paquete**  
 Al actualizar paquetes de [!INCLUDE[ssISversion2005](../includes/ssisversion2005-md.md)] , cree los identificadores de los paquetes nuevos para las versiones actualizadas de los paquetes.  
  
## <a name="see-also"></a>Vea también  
 [Información general de seguridad &#40; Integration Services &#41;](../integration-services/security/security-overview-integration-services.md)   
 [Ampliar paquetes con Scripting](../integration-services/extending-packages-scripting/extending-packages-with-scripting.md)  
  
  

