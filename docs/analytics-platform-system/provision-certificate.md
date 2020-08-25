---
title: Aprovisionamiento del certificado
description: Aprovisionamiento de certificados en Analytics Platform System.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 669e65a7d27b208d861a33618d889707134dfefa
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/25/2020
ms.locfileid: "74400511"
---
# <a name="certificate-provisioning-in-analytics-platform-system"></a>Aprovisionamiento de certificados en Analytics Platform System
La página de **aprovisionamiento de certificados PDW** del sistema Analytics Platform System**Configuration Manager** importa o quita el certificado que usa PDW. 

Con, un certificado para cifrar las conexiones puede ayudar a proteger la comunicación con el nodo de control a través de clientes de SQL Server, herramientas que usan los controladores de PDW de SQL Server, la [consola de administración](monitor-the-appliance-by-using-the-admin-console.md)y las cargas de Integration Services. 
  
## <a name="prerequisites"></a>Prerrequisitos  
Antes de instalar el certificado, haga lo siguiente:  
  
1.  Obtener un certificado seguro. Si necesita más información acerca de cómo obtener un certificado seguro, póngase en contacto con Soporte técnico de Microsoft.  
  
2.  Guarde el certificado en el nodo de control en un archivo PFX protegido por contraseña.  
  
## <a name="for-security-reasons-obtain-a-trusted-certificate"></a>Por motivos de seguridad, obtener un certificado de confianza  
PDW de SQL Server admite el uso de un certificado para cifrar las conexiones al nodo de control; incluye conexiones a la **consola de administración**de.  
  
De forma predeterminada, la **consola de administración** incluye un certificado autofirmado que proporciona privacidad, pero no la autenticación de servidor. Esto puede dejar comunicaciones vulnerables a un ataque de tipo "Man in the Middle". Cuando un usuario se conecta a la consola de administración mediante el certificado autofirmado, Internet Explorer devuelve el error: "hay un problema con el certificado de seguridad de este sitio web".  
  
Aunque la conexión a través del certificado autofirmado cifra los datos en vuelo entre el cliente y el servidor, la conexión sigue en riesgo de los atacantes.  
  
> [!WARNING]  
> Los administradores del dispositivo deben adquirir inmediatamente un certificado que se encadene a una entidad de certificación de confianza que reconozcan los clientes, con el fin de tener una conexión segura y quitar el error que informa de Internet Explorer.  
  
La ruta de certificación debe contener el nombre de dominio completo que se asigna a la dirección IP del clúster del nodo de control (recomendado) o el nombre que los usuarios escriben en sus barras de direcciones del explorador para tener acceso a la **consola de administración**.  
  
Use el**Configuration Manager** del sistema de plataforma de análisis para agregar o quitar el certificado de confianza. No se admite la utilización directa de la herramienta de configuración de certificados (**winHttpCertCfg.exe**) de Microsoft Windows http Services para administrar el certificado.  
  
## <a name="import-or-remove-the-certificate"></a>Importar o quitar el certificado  
Las instrucciones siguientes muestran cómo importar o quitar el certificado de la aplicación.  
  
### <a name="to-import-the-certificate"></a>Para importar el certificado  
  
1.  Inicie el **Configuration Manager**.  
Para obtener más información, consulte [Inicio del&#41;de &#40;de Configuration Manager de la plataforma de análisis ](launch-the-configuration-manager.md).  

2.  En el panel izquierdo del **Configuration Manager**, expanda **topología de almacenamiento de datos paralelo**y, a continuación, haga clic en **certificados**.  
  
3.  Seleccione **importar un certificado y configure el dispositivo para usarlo**y, a continuación, haga clic en **examinar** para buscar y seleccionar el archivo de certificado.  
  
4.  Escriba la contraseña del certificado en el campo **contraseña** .  
  
5.  Haga clic en **aplicar** para configurar el certificado para el dispositivo.  
  
PDW de SQL Server no cifrará la conexión actual mediante el certificado importado, pero usará el certificado para las nuevas conexiones.  
  
### <a name="to-remove-the-previously-imported-certificate"></a>Para quitar el certificado importado anteriormente  
  
1.  Inicie el **Configuration Manager**. 

<!-- MISSING LINKS
For more information, see [Launch the Configuration Manager &#40;Analytics Platform System&#41;](launch-the-configuration-manager-analytics-platform-system.md).  
-->
  
2.  En el panel izquierdo del **Configuration Manager**, expanda **topología de almacenamiento de datos paralelo**y, a continuación, haga clic en **certificados**.  
  
3.  Seleccione **quitar cualquier certificado aprovisionado en el dispositivo**.  
  
4.  Haga clic en **aplicar** para quitar el certificado importado previamente del dispositivo.  
  
PDW de SQL Server continuará cifrando las conexiones actuales, pero no usará el certificado quitado para las nuevas conexiones.  
  
![Certificado PDW del dispositivo DWConfig](media/dwconfig-appl-pdw-cert.png "Certificado PDW del dispositivo DWConfig")  
  
## <a name="see-also"></a>Consulte también  
[Inicie el sistema de Configuration Manager &#40;Analytics Platform&#41;](launch-the-configuration-manager.md)  
