---
title: "Protocolos de propiedades de MSSQLSERVER (pestaña marcas) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: configuration-manager
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: MSSQLSERVER property protocols
ms.assetid: 4d38e6e9-f95f-4e79-ae45-89f631037528
caps.latest.revision: "32"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: db816ac16fa53afeb3c7f8f5434d3123f5a4dc00
ms.sourcegitcommit: b6116b434d737d661c09b78d0f798c652cf149f3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/17/2018
---
# <a name="protocols-for-mssqlserver-properties-flags-tab"></a>Propiedades de Protocolos de MSSQLSERVER (pestaña Marcas)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Cuando se instala un certificado en el servidor, use la **marcas** pestaña en el **protocolos para MSSQLSERVER propiedades** cuadro de diálogo para ver o especificar el cifrado de protocolo y ocultar opciones de la instancia. [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe reiniciarse para habilitar o deshabilitar la **ForceEncryption** configuración.  
  
 Para cifrar conexiones, debe proporcionar a [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] un certificado. Si no se instala ningún certificado, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generará un certificado autofirmado al iniciar la instancia. Este certificado autofirmado se puede usar en lugar de un certificado de una entidad emisora de certificados de confianza, pero no proporciona la autenticación ni el no rechazo.  
  
> [!CAUTION]  
>  Las conexiones SSL (capa de sockets seguros) cifradas con un certificado autofirmado no proporcionan una seguridad elevada. Son susceptibles de ataques de tipo "Man-in-the-middle". No debe confiar en la SSL con certificados autofirmados en un entorno de producción ni en servidores conectados a Internet.  
  
 Para obtener más información sobre el cifrado, vea el tema sobre cómo cifrar conexiones en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 El proceso de inicio de sesión siempre está cifrado. Si **ForceEncryption** se establece en **Yes**, se cifrarán todas las comunicaciones entre el cliente y el servidor, y los clientes que se conecten a [!INCLUDE[ssDE](../../includes/ssde-md.md)] necesitan estar configurados para confiar en la entidad de certificación raíz del certificado de servidor. Para más información, vea "Cómo habilitar conexiones cifradas en el motor de base de datos [!INCLUDE[ssDE](../../includes/ssde-md.md)] (Administrador de configuración de[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] )" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="cluster-servers"></a>Servidores de clúster  
 Si desea utilizar el cifrado con clúster de conmutación por error, debe instalar el certificado del servidor con el nombre DNS completo del servidor virtual en todos los nodos del clúster de conmutación por error. Por ejemplo, si tiene un clúster de dos nodos, con nodos con nombre "test1.  *\<su empresa >*.com "y" test2. *\<su empresa >*.com "y un servidor virtual denominado"virtsql", debe instalar un certificado para" virtsql. *\<su empresa >*.com "en ambos nodos. A continuación, puede activar la casilla **ForceEncryption** en el **Administrador de configuración de SQL Server** para configurar el cifrado del clúster de conmutación por error.  
  
## <a name="options"></a>Opciones  
 **ForceEncryption**  
 Fuerce el cifrado de protocolos. El cifrado es un método para mantener la confidencialidad de la información reservada y consiste en alterar los datos para darles un formato ilegible. El cifrado asegura que los datos permanecen seguros, incluso si se ven los paquetes durante el proceso de transmisión. Para utilizar el enlace del canal, active **Forzar cifrado** en **Activado** y configure **Protección ampliada** en la pestaña **Opciones avanzadas** .  
  
 **HideInstance**  
 Permite impedir que el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser exponga esta instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] a los equipos cliente que intenten buscarla con el botón **Examinar** . En el caso de instancias con nombre en el servidor, para conectar, las aplicaciones cliente deben especificar la información de extremo de protocolo. Por ejemplo, el número de puerto o el nombre de canalización con nombre, como **tcp:server,5000**. Para más información, consulte [Logging In to SQL Server](../../database-engine/configure-windows/logging-in-to-sql-server.md).  
  
 Para obtener más información, vea "Cómo habilitar conexiones cifradas en el motor de base de datos (Administrador de configuración de SQL Server)" en los Libros en pantalla.  
  
  
