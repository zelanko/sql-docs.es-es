---
title: Configuración de IIS para controladores para PHP
description: Obtenga información sobre cómo configurar IIS para hospedar aplicaciones PHP que usan los controladores para PHP para SQL Server. Los recursos que figuran aquí son específicos para utilizar FastCGI con IIS.
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- configuring, Internet Information Services
ms.assetid: d2dc75d3-9bf7-481c-85f2-8b6310b21461
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7ab31be628d4c93f0e4331e3d63d47c4924a6fa7
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/05/2020
ms.locfileid: "91726889"
---
# <a name="configuring-iis-for-the-microsoft-drivers-for-php-for-sql-server"></a>Configuración de IIS para los controladores de Microsoft para PHP para SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

En este tema se proporcionan vínculos a recursos del [sitio web de Internet Information Services (IIS)](https://www.iis.net/) que son relevantes para la configuración de IIS a fin de hospedar aplicaciones PHP. Los recursos que figuran aquí son específicos para utilizar FastCGI con IIS. FastCGI es un protocolo estándar que permite a los archivos ejecutables de la interfaz de puerta de enlace común (CGI) del marco de una aplicación comunicarse con el servidor web. La diferencia entre el protocolo CGI estándar y FastCGI es que este último vuelve a usar los procesos CGI en varias solicitudes.  
  
## <a name="tutorials"></a>Tutoriales  
En los siguientes vínculos se ofrecen tutoriales sobre cómo configurar FastCGI para PHP y hospedar aplicaciones PHP en IIS 6.0 e IIS 7.0:  
  
-   [FastCGI with PHP (FastCGI con PHP)](/iis/web-hosting/web-server-for-shared-hosting/fastcgi-with-php)  
-   [Using FastCGI to Host PHP Applications on IIS 7.0 (Uso de FastCGI para hospedar aplicaciones PHP en IIS 7.0)](/iis/application-frameworks/install-and-configure-php-applications-on-iis/using-fastcgi-to-host-php-applications-on-iis)  
-   [Using FastCGI to Host PHP Applications on IIS 6.0 (Uso de FastCGI para hospedar aplicaciones PHP en IIS 6.0)](/iis/application-frameworks/install-and-configure-php-applications-on-iis/using-fastcgi-to-host-php-applications-on-iis-60)  
-   [Configuring FastCGI Extension for IIS 6.0 (Configuración de la extensión de FastCGI para IIS 6.0)](/iis/application-frameworks/install-and-configure-php-on-iis/configuring-the-fastcgi-extension-for-iis-60)  
  
## <a name="video-presentations"></a>Presentaciones en vídeo  
En los siguientes vínculos se ofrecen presentaciones en vídeo sobre cómo configurar FastCGI para PHP y utilizar las características de IIS 7.0 para hospedar aplicaciones PHP:  
  
-   [Setting up FastCGI for PHP (Configuración de FastCGI para PHP)](/iis/application-frameworks/running-php-applications-on-iis/set-up-fastcgi-for-php)  
-   [Partying with PHP on Microsoft Internet Information Services 7 (Integración de PHP con Microsoft Internet Information Services 7)](/iis/application-frameworks/running-php-applications-on-iis/mix08-partying-with-php-on-microsoft-internet-information-services-7-and-above)  
  
## <a name="support-resources"></a>Recursos de soporte  
En los siguientes foros se ofrece soporte técnico de la comunidad para FastCGI en IIS:  
  
-   [FastCGI Handler (Controlador de FastCGI)](https://forums.iis.net/1103.aspx)  
-   [IIS 7 - FastCGI Module (IIS 7: módulo de FastCGI)](https://forums.iis.net/1104.aspx)  
  
## <a name="see-also"></a>Consulte también  
[Introducción a los controladores de Microsoft para PHP para SQL Server](../../connect/php/getting-started-with-the-php-sql-driver.md)

[Guía de programación para los controladores de Microsoft para PHP para SQL Server](../../connect/php/programming-guide-for-php-sql-driver.md)

[Referencia de API del controlador SQLSRV](../../connect/php/sqlsrv-driver-api-reference.md)

[Constantes &#40;controladores de Microsoft para PHP para SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  
