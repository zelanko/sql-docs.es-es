---
title: Copia de seguridad clave de cifrado (modo nativo de SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.backupencryptionkey.F1
ms.assetid: eb8c82be-323b-4d86-ab10-c1bf69a4abe3
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: db573e1a070b110ff0f5224a6d079f3fe7c377ca
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48061695"
---
# <a name="backup-encryption-key-ssrs-native-mode"></a>Copia de seguridad de clave de cifrado (Modo nativo de SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] utiliza una clave de cifrado para proteger datos confidenciales que se almacenan en la base de datos del servidor de informes. Tener una copia de seguridad de esta clave es esencial para garantizar el acceso continuado a las cadenas de conexión cifradas y a las credenciales. Debe disponer de una copia de seguridad de esta clave si mueve la base de datos del servidor de informes a otro equipo o si cambia el nombre de usuario o la contraseña de la cuenta del servicio Servidor de informes. Ambas operaciones requieren que restaure la clave a partir de una copia de seguridad que creara previamente.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Para abrir el cuadro de diálogo de la clave de cifrado de copia de seguridad, haga clic en **las claves de cifrado** en el panel de navegación de la [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager y, a continuación, haga clic en **copia de seguridad**. Este cuadro de diálogo también aparece al actualizar la cuenta de servicio con la página cuenta de servicio en la [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager. Para obtener más información sobre la [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager, vea [Reporting Services Configuration Manager &#40;modo nativo&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
## <a name="options"></a>Opciones  
 **Ubicación del archivo**  
 Especifique un nombre de archivo y una ubicación para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a la clave simétrica. La clave simétrica nunca se almacena en texto simple. Debe escribir una contraseña para proteger el archivo.  
  
 **Contraseña**  
 Escriba una contraseña que proteja el archivo contra el acceso no autorizado. Solo los usuarios que conozcan la contraseña podrán restaurar la clave que se bloquea dentro del archivo. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] exige una directiva de contraseña segura. La contraseña debe contener ocho caracteres, como mínimo, e incluir una combinación de caracteres alfanuméricos en mayúsculas y minúscula, y al menos un carácter de símbolo.  
  
 **Confirmar contraseña**  
 Vuelva a escribir la contraseña que escribió.  
  
## <a name="see-also"></a>Vea también  
 [Temas de Ayuda de F1 de administrador de configuración de Reporting Services &#40;modo nativo de SSRS&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [Hacer copia de seguridad y restaurar claves de cifrado de Reporting Services](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)   
 [Eliminar y volver a crear claves de cifrado &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-delete-and-re-create-encryption-keys.md)   
 [Inicializar un servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)   
 [Almacenar datos cifrados del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [Las claves de cifrado &#40;modo nativo de SSRS&#41;](../../../2014/sql-server/install/encryption-keys-ssrs-native-mode.md)  
  
  
