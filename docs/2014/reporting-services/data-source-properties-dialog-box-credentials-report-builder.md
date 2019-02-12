---
title: Las credenciales (generador de informes) cuadro de diálogo Propiedades del origen de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10017"
ms.assetid: 4531f09f-d653-4c05-a120-d7788838bc99
author: maggiesmsft
ms.author: maghan
manager: kfile
ms.openlocfilehash: c57ce5992349aa9fe195620b8ac1c1d2b2ba4744
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56034206"
---
# <a name="data-source-properties-dialog-box-credentials-report-builder"></a>Propiedades del origen de datos (cuadro de diálogo), Credenciales (Generador de informes)
  Seleccione **Credenciales** en el cuadro de diálogo **Propiedades del origen de datos** para mostrar y modificar las credenciales para conectarse a un origen de datos incrustado en el informe. Las credenciales que proporcione se usarán para tener acceso al origen de datos con el fin de obtener una vista previa de los informes. Para obtener más información, vea [Especificar credenciales en el Generador de informes](../../2014/reporting-services/specify-credentials-in-report-builder.md).  
  
## <a name="options"></a>Opciones  
 **Usar la autenticación de Windows (seguridad integrada)**  
 Seleccione esta opción para utilizar la autenticación de Windows.  
  
 **Use este nombre de usuario y contraseña**  
 Seleccione esta opción para proporcionar un nombre de usuario y una contraseña específicos. Para los orígenes de datos incrustados: al publicar el proyecto del servidor de informes en el servidor de destino, el nombre de usuario y la contraseña se guardan como las credenciales almacenadas para la base de datos. Si desea usar el nombre de usuario y la contraseña como credenciales de Windows, puede cambiar las propiedades del origen de datos compartido publicado en el servidor de destino. Para obtener más información, vea [Crear, eliminar o modificar un origen de datos compartido &#40;Administrador de informes&#41;](../../2014/reporting-services/create-delete-or-modify-a-shared-data-source-report-manager.md) en la documentación de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] en los [Libros en pantalla](https://go.microsoft.com/fwlink/?linkid=121312) de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 **Nombre de usuario.**  
 Escriba un nombre de usuario con el que iniciar sesión en el origen de datos.  
  
 **Contraseña**  
 Escriba una contraseña con la que iniciar sesión en el origen de datos.  
  
 **Pedir credenciales**  
 Seleccione esta opción para solicitar las credenciales al ejecutar el informe.  
  
 **Escriba la cadena de mensaje**  
 Escriba una frase para pedir al usuario que proporcione las credenciales de inicio de sesión para el origen de datos.  
  
 **Sin credenciales**  
 Seleccione esta opción si no desea proporcionar credenciales para el origen de datos. Esta opción solo funciona si el origen de datos no acepta credenciales o si se pasan credenciales de otra manera.  
  
 En algunas extensiones de datos, se debe configurar una cuenta de ejecución desatendida en el servidor de informes.  
  
 Para obtener más información, vea el tema del tipo de origen de datos correspondiente en [Agregar datos de orígenes de datos externos &#40;SSRS&#41;](report-data/add-data-from-external-data-sources-ssrs.md) y [Configurar la cuenta de ejecución desatendida &#40;Administrador de configuración de SSRS&#41;](install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md) en la documentación de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] de los [Libros en pantalla](https://go.microsoft.com/fwlink/?linkid=121312) de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vea también  
 [Ayuda del Generador de informes para cuadros de diálogo, paneles y asistentes](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [Propiedades del origen de datos (cuadro de diálogo), General &#40;Generador de informes&#41;](../../2014/reporting-services/data-source-properties-dialog-box-general-report-builder.md)   
 [Agregar y comprobar una conexión de datos o un origen de datos &#40;generador de informes y SSRS&#41;](report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)   
 [Agregar datos a un informe &#40;generador de informes y SSRS&#41;](report-data/report-datasets-ssrs.md)  
  
  
