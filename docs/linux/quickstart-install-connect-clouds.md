---
title: "Introducción a SQL Server 2017 en la nube | Documentos de Microsoft"
description: "Este tutorial rápido muestra cómo ejecutar el servidor de SQL 2017 en Linux en la nube de su elección."
author: annashres
ms.author: annashres
manager: craigg
ms.date: 10/25/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.component: 
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: 
ms.openlocfilehash: 3966bb71f4112c12d340ab9780586013d8732206
ms.sourcegitcommit: f0c5e37c138be5fb2cbb93e9f2ded307665b54ea
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/24/2018
---
# <a name="quickstart-run-the-sql-server-2017-in-the-cloud"></a>Inicio rápido: Ejecutar el servidor de SQL 2017 en la nube

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

En este tutorial rápido, se instalará SQL Server 2017 en Red Hat Enterprise Linux (RHEL), SUSE Linux Enterprise Server (SLES) o Ubuntu en la nube de su elección. Vaya a [aprovisionar una máquina virtual de Linux SQL Server en el portal de Azure](https://docs.microsoft.com/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json) para ejecutar SQL Server en Linux en Azure.

    > [!NOTE]
    > If you choose to run a paid edition of SQL Server then you need to bring your own license (BYOL)

## <a name="amazon-web-services"></a>Servicios Web de Amazon
1.  Crear un AMI Linux con al menos 2 GB de memoria de marketplace 
    * [RHEL 7.3+](https://aws.amazon.com/marketplace/pp/B00KWBZVK6)
    * [SLES v12 SP2](https://aws.amazon.com/marketplace/pp/B00PMM99PI)
    * [Ubuntu 16.04](https://aws.amazon.com/marketplace/pp/B01JBL2M0O)
1.  Conectar con el AMI con ssh
1.  Siga el tutorial rápido para la distribución de Linux que eligió: 
    * [RHEL](quickstart-install-connect-red-hat.md)
    * [SLES](quickstart-install-connect-suse.md)
    * [Ubuntu](quickstart-install-connect-ubuntu.md)
1.  Configurar para las conexiones remotas: 
    * Abra el [consola EC2 de Amazon]( https://console.aws.amazon.com/ec2/)
    * En el panel de navegación, elija **grupos de seguridad**. 
    * Elija **entrantes, editar, Agregar regla**
    * Agregar una regla de entrada para permitir el tráfico en el puerto en el que SQL Server escucha (puerto TCP 1433)

    
## <a name="digital-ocean"></a>Océano digital
1. Inicie sesión en el [el panel de control](https://cloud.digitalocean.com/login) y haga clic en crear un droplet
1. Elija un droplet Ubuntu 16.04 con al menos 2 GB de memoria
1. Conectarse a la gota con ssh
1. Siga el [inicio rápido de Ubuntu](quickstart-install-connect-ubuntu.md)
1. Configurar para las conexiones remotas:
    * En la parte superior del Panel de Control, siga el **red** vincular y, a continuación, seleccione **Firewalls**
    * Agregar una regla de entrada para permitir el tráfico en el puerto en el que SQL Server escucha (puerto TCP 1433)
    
## <a name="google-cloud-platform"></a>Plataforma de nube de Google
1.  Crear una imagen de Linux con al menos 2 GB de memoria desde el iniciador de la nube 
    * [RHEL 7.3+](https://console.cloud.google.com/launcher/details/rhel-cloud/rhel-7)
    * [SLES v12 SP2](https://console.cloud.google.com/launcher/details/suse-cloud/sles-12)
    * [Ubuntu 16.04](https://console.cloud.google.com/launcher/details/ubuntu-os-cloud/ubuntu-xenial)
1.  Conectarse a la imagen con ssh
1.  Siga el tutorial rápido para la distribución de Linux que eligió: 
    * [RHEL](quickstart-install-connect-red-hat.md)
    * [SLES](quickstart-install-connect-suse.md)
    * [Ubuntu](quickstart-install-connect-ubuntu.md)
1.  Configurar para las conexiones remotas: 
    * Vaya a la [las reglas de Firewall](https://console.cloud.google.com/networking/firewalls)
    * Agregar una regla de entrada para permitir el tráfico en el puerto en el que escucha SQL Server (valor predeterminado tcp: 1433)
