---
title: 'Certificado de aprovisionamiento: Analytics Platform System | Microsoft Docs'
description: Aprovisionamiento de certificados en Analytics Platform System.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 98fffc189aab674f46030086a8277395e84f7f4d
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/27/2018
ms.locfileid: "52399809"
---
# <a name="certificate-provisioning-in-analytics-platform-system"></a>Aprovisionamiento de certificados en Analytics Platform System
El **suministro de certificados de PDW** página del sistema de plataforma de análisis**Configuration Manager** importa o quita el certificado utilizado por PDW. 

Un certificado para cifrar las conexiones permiten una comunicación segura al nodo de Control a través de los clientes de SQL Server, las herramientas que usan los controladores de PDW de SQL Server, el [Admin Console](monitor-the-appliance-by-using-the-admin-console.md), y los servicios de integración de carga. 
  
## <a name="prerequisites"></a>Requisitos previos  
Antes de instalar el certificado, realice lo siguiente:  
  
1.  Obtener un certificado seguro. Si necesita obtener más información sobre cómo obtener un certificado seguro, póngase en contacto con Microsoft Support.  
  
2.  Guarde el certificado en el nodo de Control en un archivo PFX protegido por contraseña.  
  
## <a name="for-security-reasons-obtain-a-trusted-certificate"></a>Por motivos de seguridad, obtener un certificado de confianza  
PDW de SQL Server admite el uso de un certificado para cifrar las conexiones en el nodo de Control; incluidas las conexiones con el **Admin Console**.  
  
De forma predeterminada, el **Admin Console** incluye un certificado autofirmado que proporciona privacidad, pero no la autenticación de servidor. Esto puede dejar las comunicaciones vulnerable a ataques man-in-the-middle. Cuando un usuario se conecta a la consola de administración mediante el certificado autofirmado, Internet Explorer devuelve el error: "Hay un problema con el certificado de seguridad del sitio Web".  
  
Aunque la conexión mediante el certificado autofirmado cifra los datos sobre la marcha entre el cliente y el servidor, la conexión todavía está expuesto a los atacantes.  
  
> [!WARNING]  
> Los administradores del equipo inmediatamente deben adquirir un certificado que se encadena a una entidad de certificación de confianza reconocida por los clientes, con el fin de tener una conexión segura y quitar el error que informa de Internet Explorer.  
  
La ruta de certificación debe contener el nombre de dominio completo que se asigna para el nodo de Control de dirección IP del clúster (recomendado) o el nombre que los usuarios escriban en las barras de dirección del explorador para tener acceso a la **Admin Console**.  
  
Usar el sistema Analytics Platform System**Configuration Manager** para agregar o quitar el certificado de confianza. Directamente mediante la herramienta de configuración de certificado de Microsoft Windows HTTP Services (**winHttpCertCfg.exe**) administrar el certificado no es compatible.  
  
## <a name="import-or-remove-the-certificate"></a>Importar o quitar el certificado  
Las instrucciones siguientes muestran cómo importar o quitar el certificado del dispositivo.  
  
### <a name="to-import-the-certificate"></a>Para importar el certificado  
  
1.  Iniciar el **Configuration Manager**.  
Para obtener más información, consulte [iniciar el Administrador de configuración &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md).  

2.  En el panel izquierdo de la **Configuration Manager**, expanda **topología de almacenamiento de datos paralela**y, a continuación, haga clic en **certificados**.  
  
3.  Seleccione **importar un certificado y configurar el dispositivo para usarlo**y, a continuación, haga clic en **examinar** para buscar y seleccionar el archivo de certificado.  
  
4.  Escriba la contraseña del certificado en el **contraseña** campo.  
  
5.  Haga clic en **aplicar** para configurar el certificado para el dispositivo.  
  
PDW de SQL Server no cifrará la conexión actual con el certificado importado, pero usará el certificado para las nuevas conexiones.  
  
### <a name="to-remove-the-previously-imported-certificate"></a>Para quitar el certificado importado anteriormente  
  
1.  Iniciar el **Configuration Manager**. 

<!-- MISSING LINKS
For more information, see [Launch the Configuration Manager &#40;Analytics Platform System&#41;](launch-the-configuration-manager-analytics-platform-system.md).  
-->
  
2.  En el panel izquierdo de la **Configuration Manager**, expanda **topología de almacenamiento de datos paralela**y, a continuación, haga clic en **certificados**.  
  
3.  Seleccione **quitar cualquier certificado en el dispositivo**.  
  
4.  Haga clic en **aplicar** para quitar el certificado importado anteriormente desde el dispositivo.  
  
PDW de SQL Server seguirá cifrar las conexiones actuales, pero no usará el certificado que ha quitado para las nuevas conexiones.  
  
![Certificado PDW del dispositivo DWConfig](media/dwconfig-appl-pdw-cert.png "certificado PDW del dispositivo DWConfig")  
  
## <a name="see-also"></a>Vea también  
[Inicie el Administrador de configuración &#40;Analytics Platform System&#41;](launch-the-configuration-manager.md)  
