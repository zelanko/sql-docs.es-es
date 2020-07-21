---
title: Controlar la distribución de informes | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [Reporting Services], report distribution
- subscriptions [Reporting Services], e-mail
- subscriptions [Reporting Services], file share delivery
- file share delivery [Reporting Services]
- e-mail [Reporting Services]
- subscriptions [Reporting Services], security
- mail [Reporting Services]
ms.assetid: 8f15e2c6-a647-4b05-a519-1743b5d8654c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: de8a27801ef89f10bf303cee17d1c2d0e1081c5a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66109697"
---
# <a name="control-report-distribution"></a>Controlar la distribución de informes
  Puede configurar un servidor de informes para reducir los riesgos de seguridad asociados a la distribución por correo electrónico y a recursos compartidos de archivos.  
  
## <a name="securing-reports"></a>Proteger informes  
 El primer paso para controlar la distribución de informes consiste en proteger el informe contra accesos no autorizados. Para poder utilizarse en una suscripción, el informe debe utilizar un conjunto almacenado de credenciales que no varíen para las entregas individuales. Cualquier usuario con acceso al informe en el servidor de informes puede ejecutarlo y posiblemente distribuirlo. Para impedir que esto ocurra, debe limitar el acceso al informe únicamente a aquellos usuarios que lo necesiten. Para obtener más información, consulte [proteger informes y recursos](security/secure-reports-and-resources.md) y [carpetas seguras](security/secure-folders.md).  
  
 Los informes extremadamente confidenciales que utilicen la seguridad de base de datos para autorizar el acceso no pueden distribuirse mediante una suscripción.  
  
> [!IMPORTANT]  
>  Los informes se transportan como archivos. Los riesgos y las medidas de seguridad que se aplican a los archivos se aplican igualmente a los informes que se guardan en disco o se envían como datos adjuntos. Cualquier usuario con acceso a un archivo puede distribuirlo o utilizarlo como desee.  
  
## <a name="controlling-e-mail-delivery"></a>Controlar la entrega por correo electrónico  
 Puede configurar un servidor de informes para limitar la distribución por correo electrónico a dominios de host específicos. Por ejemplo, puede evitar que un servidor de informes entregue un informe a todos los dominios, excepto a los que figuran en el archivo de configuración RSReportServer.  
  
 También puede establecer los parámetros de configuración para ocultar el campo **Para** en una suscripción. En este caso, los informes solo se entregan al usuario que haya definido la suscripción. No obstante, una vez que se envíe un informe a un usuario, no puede impedir explícitamente que se reenvíe.  
  
 El método más eficaz de controlar la distribución de informes consiste en configurar el servidor de informes para que solo envíe una dirección URL de servidor de informes. El servidor de informes utiliza Autenticación de Windows y un modelo de autorización basada en roles para controlar el acceso a un informe. Si un usuario recibe accidentalmente mediante el correo electrónico un informe que no está autorizado para ver, el servidor de informes no lo mostrará.  
  
## <a name="controlling-file-share-delivery"></a>Controlar la entrega a recursos compartidos de archivos  
 La entrega a recursos compartidos de archivos se utiliza para enviar un informe a un archivo de un disco duro. Una vez que el archivo se ha guardado en un disco, ya no está sujeto al modelo de seguridad basada en roles que utiliza el servidor de informes para controlar el acceso de los usuarios. Para proteger un informe que se haya entregado a un disco, puede utilizar listas de control de acceso (ACL) en el archivo en sí o en la carpeta que lo contenga. Según el sistema operativo que utilice, es posible que existan opciones de seguridad adicionales.  
  
## <a name="see-also"></a>Consulte también  
 [Configurar un servidor de informes para la entrega por correo electrónico &#40;SSRS Configuration Manager&#41;](../../2014/sql-server/install/configure-a-report-server-for-e-mail-delivery-ssrs-configuration-manager.md)   
 [Suscripciones y entrega &#40;Reporting Services&#41;](subscriptions/subscriptions-and-delivery-reporting-services.md)   
 [Creación y administración de suscripciones para servidores de informes en modo nativo](../../2014/reporting-services/create-manage-subscriptions-native-mode-report-servers.md)  
  
  
