---
title: Restaurar clave de cifrado (modo nativo de SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.restoreencryptionkey.F1
ms.assetid: 11ce51e5-f5d4-40b6-88d8-9360fb50e66c
caps.latest.revision: 6
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: d9a048a70beb3fa22ab250316b6e630b845e7ca7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37303635"
---
# <a name="restore-encryption-key-ssrs-native-mode"></a>Restaurar clave de cifrado (Modo nativo de SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] utiliza una clave de cifrado para proteger datos confidenciales que se almacenan en la base de datos del servidor de informes. Para asegurarse de que dispone de acceso continuado a los datos cifrados, es importante que cree una copia de seguridad de la clave de cifrado por si necesita restaurarla posteriormente debido a cambios de la cuenta de servicio o como parte de una migración planeada. En este tema es una visión general de cómo usar el [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager para restaurar las claves.  
  
 [!INCLUDE[applies](../../includes/applies-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
 Para restaurar la clave, debe haber guardado previamente una copia de seguridad de la misma en un archivo protegido mediante contraseña. Durante la restauración de la clave, el servidor de informes reemplazará una clave existente con la clave que se encuentra en el archivo protegido mediante contraseña. La clave que está dentro del archivo debe ser idéntica a la que se utiliza para cifrar y descifrar los datos.  
  
 Para comprobar si restauró una clave válida, utilice el Administrador de informes para ver suscripciones o cualquier informe que tenga un origen de datos que utilice las credenciales almacenadas. Si recibe el error "El servidor de informes no puede tener acceso a los datos cifrados" al intentar abrir una página de definición de suscripción, o si el sistema solicita que escriba las credenciales al abrir un informe que previamente utilizaba las credenciales almacenadas para el origen de datos del informe, entonces restauró una clave no válida.  
  
 Si restaura una clave no válida que sea diferente de la que se usó para cifrar datos, no se podrán descifrar los datos que estén almacenados actualmente en la base de datos del servidor de informes. Si restaura una clave no válida, debería restaurar una copia de seguridad de la clave correcta inmediatamente, si está disponible. Si no dispone de una copia de seguridad de la  clave que se usó para cifrar los datos, debe eliminar todos los datos cifrados. Haga clic en el **eliminar** situado en la [las claves de cifrado](../../../2014/sql-server/install/encryption-keys-ssrs-native-mode.md) página para realizar este paso. Después de eliminar el contenido cifrado, debe actualizar manualmente todas las suscripciones y volver a especificar todas las credenciales almacenadas que se hayan definido para los informes y las suscripciones controladas por datos del servidor de informes.  
  
## <a name="restore-encryption-key-dialog"></a>Cuadro de diálogo Restaurar clave de cifrado  
 Para obtener información sobre dónde encontrar el [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager, vea [Reporting Services Configuration Manager &#40;modo nativo&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
 Para abrir el cuadro de diálogo Restaurar clave de cifrado, haga clic en **las claves de cifrado** en el panel de navegación de la [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager y, a continuación, haga clic en **restaurar**. Este cuadro de diálogo también aparece al actualizar la cuenta de servicio con la página cuenta de servicio en la [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager. Para obtener más información sobre  
  
## <a name="options"></a>Opciones  
 **Ubicación del archivo**  
 Seleccione el archivo protegido mediante contraseña que contenga una copia de la clave simétrica. La extensión de archivo predeterminada es .snk.  
  
 **Contraseña**  
 Escriba la contraseña que desbloquea el archivo. Solo los usuarios que conocen la contraseña pueden restaurar la clave. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] exige una directiva de contraseña segura. La contraseña debe contener ocho caracteres, como mínimo, e incluir una combinación de caracteres alfanuméricos en mayúsculas y minúscula, y al menos un carácter de símbolo.  
  
## <a name="see-also"></a>Vea también  
 [Temas de Ayuda de F1 de administrador de configuración de Reporting Services &#40;modo nativo de SSRS&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [Hacer copia de seguridad y restaurar claves de cifrado de Reporting Services](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)   
 [Eliminar y volver a crear claves de cifrado &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-delete-and-re-create-encryption-keys.md)   
 [Inicializar un servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-initialize-a-report-server.md)   
 [Almacenar datos cifrados del servidor de informes &#40;Administrador de configuración de SSRS&#41;](../../reporting-services/install-windows/ssrs-encryption-keys-store-encrypted-report-server-data.md)   
 [Las claves de cifrado &#40;modo nativo de SSRS&#41;](../../../2014/sql-server/install/encryption-keys-ssrs-native-mode.md)  
  
  
