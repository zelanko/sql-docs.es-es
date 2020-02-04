---
title: Habilitar un servidor de informes para el acceso mediante móvil a Power BI | Microsoft Docs
ms.date: 12/17/2015
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
ms.assetid: c1a71522-394b-46a7-b9ec-f964bdd81d82
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d14c8e092a030c88dbc4d0b5d4375bb56a8eb82c
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "63308181"
---
# <a name="enable-a-report-server-for-power-bi-mobile-access"></a>Habilitar un servidor de informes para el acceso mediante móvil a Power BI
Puede usar la aplicación móvil de Power BI para emplear informes móviles. Hay algunos valores que debe configurar para permitir que la aplicación móvil de Power BI se conecte a Reporting Services.  
  
-   [Los informes móviles exigen el modo nativo de Reporting Services](#nativemode)  
-   [Habilitar la autenticación básica para Reporting Services](#basicauth) (para CTP 3.2)  
-   [Se recomienda habilitar HTTPS junto con un certificado de confianza válido para el dispositivo cliente](#https)  
-   [Revisar la configuración del firewall](#firewall)  
  
<a name="nativemode"/>  
## <a name="reporting-services-native-mode-required"></a>Se exige el modo nativo de Reporting Services  
Los informes móviles son una característica del modo nativo. No están disponibles en el modo integrado de SharePoint. La aplicación móvil de Power BI solo funcionará con una instancia de modo nativo.  
  
<a name="basicauth"/>  
## <a name="enable-basic-authentication"></a>Habilitar la autenticación básica  
La aplicación móvil de Power BI para iOS necesita autenticación básica para conectarse y usar informes móviles. Reporting Services no está configurado con la autenticación básica habilitada de forma predeterminada. Para obtener información sobre cómo configurar la autenticación básica, consulte [Configurar la autenticación básica en el servidor de informes](../../reporting-services/security/configure-windows-authentication-on-the-report-server.md).  
  
También debe tener habilitada la autenticación de Windows para permitir que la aplicación de edición publique informes móviles.  
  
<a name="https"/>  
## <a name="enable-https"></a>Habilitar HTTPS  
Si habilita la autenticación básica, se recomienda habilitar HTTPS en Reporting Services. Si habilita HTTPS, asegúrese de que los certificados usados sean de confianza en los dispositivos cliente que ejecuten la aplicación móvil de Power BI para iOS. Esto significa que la cadena de certificación debe ser válida y estar disponible en el dispositivo cliente.  
  
Si necesita usar un certificado autofirmado con fines de desarrollo o evaluación, puede exportar el certificado del servidor de informes e instalarlo en el dispositivo móvil. Consulte la documentación del dispositivo para instalar el certificado en dicho dispositivo.  
  
Para obtener más información sobre la habilitación de SSL, consulte [Configurar conexiones SSL en un servidor de informes en modo nativo](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md).  
  
<a name="firewall"/>  
## <a name="review-firewall-settings"></a>Revisar la configuración del firewall  
Se recomienda revisar la configuración del firewall para asegurarse de que todos los dispositivos puedan conectarse correctamente a Reporting Services.   
  
Para obtener más información sobre cómo configurar Firewall de Windows, consulte [Configurar un firewall para el acceso al servidor de informes](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md).  
  
## <a name="see-also"></a>Consulte también  
  
[Configuración de la autenticación básica en el servidor de informes](../../reporting-services/security/configure-windows-authentication-on-the-report-server.md)  
[Configuración de conexiones SSL en un servidor de informes en modo nativo](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md)  
[Configurar un firewall para el acceso del Servidor de informes](../../reporting-services/report-server/configure-a-firewall-for-report-server-access.md)  
  
  
  
  
  
  

