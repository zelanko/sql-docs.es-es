---
title: Solucionar problemas con la publicación o la visualización de un informe en un servidor de informes en modo nativo | Microsoft Docs
ms.date: 02/28/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: troubleshooting
ms.topic: conceptual
ms.assetid: df7720a1-d178-45bb-8d6f-63e208cae7fe
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 6e3a96e3eef90778b0e7877b88ba79cb4e0dd43e
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "65573859"
---
# <a name="troubleshoot-publishing-or-viewing-a-report-on-a-native-mode-report-server"></a>Solucionar problemas con la publicación o la visualización de un informe en un servidor de informes en modo nativo
  
  
  
Al publicar o cargar un informe en un servidor de informes configurado en modo nativo, podría observar problemas que son específicos de la visualización en el servidor de informes. Utilice este tema como ayuda para solucionar estos problemas.   
  
## <a name="why-am-i-being-prompted-for-credentials-when-i-publish-a-report"></a>¿Por qué me piden las credenciales cuando publico un informe?  
Para implementar un informe en un servidor de informes, debe especificar la dirección del servidor. Podría ver un cuadro de diálogo Inicio de sesión de Reporting Services, que le solicita las credenciales.   
  
No se especifica correctamente el nombre del servidor de informes  
  
  
Al implementar el informe en un servidor de informes en modo nativo, un error común es especificar el nombre de la carpeta de informes en lugar del correspondiente al servidor de informes.   
  
Compruebe que la dirección URL del servidor de informes es adecuada (por ejemplo, `https://localhost/reportserver`) y no la dirección del directorio virtual del Administrador de informes (por ejemplo, `https://localhost/reports`). Si especificó un número de puerto para el servidor de informes que sea diferente del número de puerto predeterminado 80, debe especificarlo en la dirección del servidor de informes (por ejemplo, `https://localhost:81/reportserver`).   
  
 ## <a name="nothing-happens-when-i-toggle-items-in-my-published-report"></a>No ocurre nada cuando activo o desactivo elementos en el informe publicado.  
  Al ver un informe en la vista previa local, puede alternar los elementos en el informe y mostrarlos u ocultarlos. Al ver el mismo informe una vez publicado en el servidor de informes, ya no se puede alternar entre los elementos.   
  
\<nombre del servidor de informes> Incluye un carácter de subrayado (_)  
  
Si un informe se ejecuta sin errores, pero los elementos de alternancia no funcionan, por ejemplo, hace clic en el icono de expandir (+) pero no sucede nada, compruebe el nombre del equipo que hospeda el servidor de informes. Si incluye un subrayado, los elementos de alternancia no funcionarán. Este es un problema conocido. No existe solución.   
  
Para ejecutar informes con elementos de alternancia, debe usar un equipo cuyo nombre no incluya caracteres de subrayado.  
  
## <a name="images-and-charts-do-not-load-when-i-use-run-as-and-a-browser-to-run-my-report"></a>Las imágenes y gráficos no se cargan cuando utilizo Ejecutar como y un explorador para ejecutar un informe.  
Al ejecutar el Administrador de informes en un contexto de seguridad diferente, podría no ver todos los elementos en un informe.   
  
### <a name="insufficient-permissions-on-internet-temporary-file-folders"></a>Permisos insuficientes en las carpetas de archivos temporales de Internet  
  
En algunas circunstancias, al utilizar el Administrador de informes para ver informes publicados que incluyen gráficos o imágenes, podría no verlos. Por ejemplo, cuando se usa el comando **Ejecutar como** de Microsoft Windows para ver un informe con un contexto de seguridad diferente, podría no tener permisos para la carpeta donde el servidor de informes almacena en caché los gráficos e imágenes como archivos temporales de Internet.   
  
Compruebe que dispone de permiso para tener acceso a las carpetas que contienen los archivos almacenados en memoria caché.   
    
## <a name="see-also"></a>Consulte también  
[Compatibilidad del explorador de Reporting Services y Power View](../../reporting-services/browser-support-for-reporting-services-and-power-view.md)  
[Errores y eventos (Reporting Services)](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  
[Solución de problemas de recuperación de datos de informes de Reporting Services](../../reporting-services/troubleshooting/troubleshoot-data-retrieval-issues-with-reporting-services-reports.md)  
[Solución de problemas de suscripciones y entrega de Reporting Services](../../reporting-services/troubleshooting/troubleshoot-reporting-services-subscriptions-and-delivery.md)  
  
  

[!INCLUDE[feedback_stackoverflow_msdn_connect](../../includes/feedback-stackoverflow-msdn-connect-md.md)]

