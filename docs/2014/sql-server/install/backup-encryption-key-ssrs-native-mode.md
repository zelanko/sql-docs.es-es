---
title: Clave de cifrado de copia de seguridad (modo nativo de SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.backupencryptionkey.F1
ms.assetid: eb8c82be-323b-4d86-ab10-c1bf69a4abe3
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: a0b2c2e597ef7069bcc51fb885a2e810871bfbb5
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952648"
---
# <a name="backup-encryption-key-ssrs-native-mode"></a>Copia de seguridad de clave de cifrado (Modo nativo de SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] utiliza una clave de cifrado para proteger datos confidenciales que están almacenados en la base de datos del servidor de informes. Tener una copia de seguridad de esta clave es esencial para garantizar el acceso continuado a las cadenas de conexión cifradas y a las credenciales. Debe disponer de una copia de seguridad de esta clave si mueve la base de datos del servidor de informes a otro equipo o si cambia el nombre de usuario o la contraseña de la cuenta del servicio Servidor de informes. Ambas operaciones requieren que restaure la clave a partir de una copia de seguridad que creara previamente.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Para abrir el cuadro de diálogo Copia de seguridad de clave de cifrado, haga clic en **Claves de cifrado** en el panel de navegación del Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y, a continuación, haga clic en **Copia de seguridad**. Este cuadro de diálogo también aparece al actualizar la cuenta de servicio desde la página Cuenta de servicio del Administrador de configuración de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Para obtener más información sobre el Configuration Manager [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], [vea &#40;administrador de configuración de Reporting Services modo&#41;nativo](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
## <a name="options"></a>Opciones  
 **Ubicación del archivo**  
 Especifique un nombre de archivo y una ubicación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] para la clave simétrica. La clave simétrica nunca se almacena en texto simple. Debe escribir una contraseña para proteger el archivo.  
  
 **Contraseña**  
 Escriba una contraseña que proteja el archivo contra el acceso no autorizado. Solo los usuarios que conozcan la contraseña podrán restaurar la clave que se bloquea dentro del archivo. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] exige una directiva de contraseñas segura. La contraseña debe contener ocho caracteres, como mínimo, e incluir una combinación de caracteres alfanuméricos en mayúsculas y minúscula, y al menos un carácter de símbolo.  
  
 **Confirmar contraseña**  
 Vuelva a escribir la contraseña que escribió.  
  
## <a name="see-also"></a>Vea también  
 [Administrador de configuración de Reporting Services temas &#40;de ayuda de F1 en&#41;el modo nativo de SSRS](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [Hacer copia de seguridad y restaurar claves de cifrado de Reporting Services](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)   
 [Eliminar y volver a crear claves de cifrado &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-delete-and-re-create-encryption-keys.md)   
 [Inicializar un servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)   
 [Almacenar datos cifrados del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [Claves &#40;de cifrado modo nativo de SSRS&#41;](../../../2014/sql-server/install/encryption-keys-ssrs-native-mode.md)  
  
  
