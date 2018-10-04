---
title: Configurar y administrar claves de cifrado (Administrador de configuración de SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- encryption keys [Reporting Services]
- private keys [Reporting Services]
- cryptography [Reporting Services]
- symmetric keys [Reporting Services]
- encryption [Reporting Services]
- public keys [Reporting Services]
ms.assetid: 58e61636-88a2-4338-ae5f-3dd210aee887
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 16a1851a46b6602bc9d92d5c7e0111ece8701d43
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48222515"
---
# <a name="configure-and-manage-encryption-keys-ssrs-configuration-manager"></a>Configurar y administrar claves de cifrado (Administrador de configuración de SSRS)
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] utiliza claves de cifrado para proteger las credenciales y la información de conexión que se almacena en una base de datos del servidor de informes. En [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], el cifrado se puede realizar a través de una combinación de claves públicas, privadas y simétricas que se utilizan para proteger la información confidencial. La clave simétrica se crea al inicializar el servidor de informes durante su instalación o configuración, y el servidor de informes la utiliza para cifrar los datos confidenciales que almacena. El sistema operativo crea las claves públicas y privadas, y se utilizan para proteger la clave simétrica. Para cada instancia del servidor de informes que almacena datos confidenciales en una base de datos del servidor de informes se crea un par de claves pública y privada.  
  
 Para administrar las claves de cifrado, hay que crear una copia de seguridad de la clave simétrica y saber cuándo y cómo se deben restaurar, eliminar o cambiar las claves. Si migra una instalación del servidor de informes o configura una implementación de ampliación horizontal, debe disponer de una copia de seguridad de la clave simétrica para poder aplicarla a la nueva instalación.  
  
> [!IMPORTANT]  
>  Cambiar periódicamente la clave de cifrado de Reporting Services es una práctica recomendada de seguridad. El momento recomendado para cambiar la clave es el inmediatamente posterior a una actualización de versión principal de Reporting Services. Si se cambia la clave después de una actualización se minimiza la interrupción del servicio adicional que ocasiona el cambio de la clave de cifrado de Reporting Services fuera del ciclo de actualización.  
  
 Para administrar las claves simétricas, puede usar la herramienta de configuración de Reporting Services o la utilidad **rskeymgmt** . Las herramientas incluidas en [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] solo se usan para administrar la clave simétrica (el sistema operativo se encarga de administrar las claves públicas y privadas). Tanto la herramienta de configuración de Reporting Services como la utilidad **rskeymgmt** admiten las tareas siguientes:  
  
-   Crear una copia de seguridad de la clave simétrica que se pueda utilizar para recuperar una instalación de un servidor de informes o como parte de una migración planeada.  
  
-   Restaurar una clave simétrica guardada previamente en una base de datos del servidor de informes, permitiendo el acceso de una instancia nueva del servidor de informes a datos existentes que no cifró originalmente.  
  
-   Eliminar los datos cifrados en una base de datos del servidor de informes, en el caso poco probable de que ya no se tenga acceso a datos cifrados.  
  
-   Volver a crear claves simétricas y volver a cifrar datos en el caso poco probable de que la clave simétrica esté en unas circunstancias comprometidas. Como práctica recomendada de seguridad, se debería volver a crear la clave simétrica periódicamente (por ejemplo, cada cierto número de meses) para proteger la base de datos del servidor de informes de ataques de intrusos que traten de descifrar la clave.  
  
-   Agregar o quitar una instancia del servidor de informes de una implementación escalada del servidor de informes en la que varios servidores de informes comparten una sola base de datos del servidor de informes y la clave simétrica que proporciona el cifrado reversible para la base de datos.  
  
## <a name="in-this-section"></a>En esta sección  
 [Inicializar un servidor de informes &#40;Administrador de configuración de SSRS&#41;](ssrs-encryption-keys-initialize-a-report-server.md)  
 Explica cómo se crean las claves de cifrado.  
  
 [Copia de seguridad y restauración de claves de cifrado de Reporting Services](ssrs-encryption-keys-back-up-and-restore-encryption-keys.md)  
 Explica cómo realizar copias de seguridad de claves de cifrado y cómo restaurarlas para recuperar o migrar una instalación del servidor de informes.  
  
 [Store los datos del servidor de informes cifrados &#40;Administrador de configuración de SSRS&#41;](ssrs-encryption-keys-store-encrypted-report-server-data.md)  
 Describe el cifrado en un servidor de informes.  
  
 [Eliminar y volver a crear las claves de cifrado &#40;Administrador de configuración de SSRS&#41;](ssrs-encryption-keys-delete-and-re-create-encryption-keys.md)  
 Explica cómo reemplazar una clave simétrica por una nueva versión y cómo empezar de nuevo si no se pueden validar las claves simétricas.  
  
 [Agregar y quitar claves de cifrado para la implementación escalada &#40;Administrador de configuración de SSRS&#41;](add-and-remove-encryption-keys-for-scale-out-deployment.md)  
 Explica como agregar y quitar claves de cifrado para controlar qué servidores de informes forman parte de una implementación escalada.  
  
## <a name="see-also"></a>Vea también  
 [Store los datos del servidor de informes cifrados &#40;Administrador de configuración de SSRS&#41;](ssrs-encryption-keys-store-encrypted-report-server-data.md)  
  
  
