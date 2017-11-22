---
title: "Introducción a SQL Server 2017 en la nube | Documentos de Microsoft"
description: "Este tutorial de inicio rápido muestra cómo ejecutar el servidor de SQL 2017 en Linux en la nube de su elección."
author: annashres
ms.author: annashres
manager: jhubbard
ms.date: 10/25/2017
ms.topic: article
ms.prod: sql-linux
ms.technology: database-engine
ms.assetid: 
ms.openlocfilehash: 0bc304b50930f8c8de5d244ea0b606add5f24d2f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="run-the-sql-server-2017-in-the-cloud"></a>Ejecutar el servidor de SQL 2017 en la nube

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

En este tutorial de inicio rápido, se instalará SQL Server 2017 en Red Hat Enterprise Linux (RHEL), SUSE Linux Enterprise Server (SLES) o Ubuntu en la nube de su elección. Vaya a [aprovisionar una máquina virtual de Linux SQL Server en el portal de Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json) para ejecutar SQL Server en Linux en Azure.

    > [!NOTE]
    > If you choose to run a paid edition of SQL Server then you need to bring your own license (BYOL)

## <a name="amazon-web-services"></a>Servicios Web de Amazon
1.  Crear un AMI Linux con un mínimo de 3,25 GB de memoria de marketplace 
    * [RHEL 7.3 +](https://aws.amazon.com/marketplace/pp/B00KWBZVK6)
    * [SLES v12 SP2](https://aws.amazon.com/marketplace/pp/B00PMM99PI)
    * [Ubuntu 16.04](https://aws.amazon.com/marketplace/pp/B01JBL2M0O)
1.  Conectar con el AMI con ssh
1.  Siga el tutorial rápido para la distrbution Linux que eligió: 
    * [RHEL](quickstart-install-connect-red-hat.md)
    * [SLES GRANDE](quickstart-install-connect-suse.md)
    * [Ubuntu](quickstart-install-connect-ubuntu.md)
1.  Configurar para las conexiones remotas: 
    * Abra el [consola EC2 de Amazon]( https://console.aws.amazon.com/ec2/)
    * En el panel de navegación, elija **grupos de seguridad**. 
    * Elija **entrantes, editar, Agregar regla**
    * Agregar una regla de entrada para permitir el tráfico en el puerto en el que SQL Server escucha (puerto TCP 1433)

    
## <a name="digital-ocean"></a>Océano digital
1. Inicie sesión en el [el panel de control](https://cloud.digitalocean.com/login) y haga clic en crear un droplet
1. Elija un droplet Ubuntu 16.04 con al menos 3,25 GB de memoria
1. Conectarse a la gota con ssh
1. Siga el [inicio rápido de Ubuntu](quickstart-install-connect-ubuntu.md)
1. Configurar para las conexiones remotas:
    * En la parte superior del Panel de Control, siga el **red** vincular y, a continuación, seleccione **Firewalls**
    * Agregar una regla de entrada para permitir el tráfico en el puerto en el que SQL Server escucha (puerto TCP 1433)
    
## <a name="google-cloud-platform"></a>Plataforma de nube de Google
1.  Crear una imagen de Linux con un mínimo de 3,25 GB de memoria desde el iniciador de la nube 
    * [RHEL 7.3 +](https://console.cloud.google.com/launcher/details/rhel-cloud/rhel-7)
    * [SLES v12 SP2](https://console.cloud.google.com/launcher/details/suse-cloud/sles-12)
    * [Ubuntu 16.04](https://console.cloud.google.com/launcher/details/ubuntu-os-cloud/ubuntu-xenial)
1.  Conectarse a la imagen con ssh
1.  Siga el tutorial rápido para la distrbution Linux que eligió: 
    * [RHEL](quickstart-install-connect-red-hat.md)
    * [SLES GRANDE](quickstart-install-connect-suse.md)
    * [Ubuntu](quickstart-install-connect-ubuntu.md)
1.  Configurar para las conexiones remotas: 
    * Vaya a la [las reglas de Firewall](https://console.cloud.google.com/networking/firewalls)
    * Agregar una regla de entrada para permitir el tráfico en el puerto en el que SQL Server escucha (apartado TCP del valor predeterminado: 1433)
