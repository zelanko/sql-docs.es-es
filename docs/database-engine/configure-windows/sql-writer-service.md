---
title: Servicio del objeto de escritura de SQL | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.suite: sql
ms.technology: configuration
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- VDI [SQL Server]
- restoring [SQL Server], SQL Writer Service
- backups [SQL Server], while SQL Server running
- Volume Shadow Copy Service
- volume backups while running [SQL Server]
- Virtual Backup Device Interface [SQL Server]
- SQL Writer Service
- services [SQL Server], SQL Writer
- MSDE Writer
- VSS
ms.assetid: 0f299867-f499-4c2a-ad6f-b2ef1869381d
caps.latest.revision: 29
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 80eb04dfefca7903592ea391d915e140d93f479f
ms.sourcegitcommit: 2666ca7660705271ec5b59cc5e35f6b35eca0a96
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 09/06/2018
ms.locfileid: "43888351"
---
# <a name="sql-writer-service"></a>servicio del objeto de escritura de SQL
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  El servicio del objeto de escritura de SQL proporciona otras funciones para la realización de copias de seguridad y restauración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante el marco del Servicio de instantáneas de volumen.  
  
 El servicio del objeto de escritura de SQL se instala automáticamente. Se debe ejecutar cuando la aplicación Servicio de instantáneas de volumen (VSS) solicita una copia de seguridad o una restauración. Para configurar el servicio, utilice el applet Servicios de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. El servicio SQL Writer se instala en todos los sistemas operativos.  
  
## <a name="purpose"></a>Finalidad  
 Durante la ejecución, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] bloquea los archivos de datos y tiene acceso exclusivo a estos. Cuando no se ejecuta el servicio del objeto de escritura de SQL, los programas de copia de seguridad que se estén ejecutando en Windows no tendrán acceso a los archivos de datos, y se deberán realizar las copias de seguridad mediante [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Utilice el servicio del objeto de escritura de SQL para que los programas de copia de seguridad de Windows puedan copiar archivos de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mientras se ejecuta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="volume-shadow-copy-service"></a>Servicio de instantáneas de volumen  
 VSS es un conjunto de API COM que implementa un marco para permitir la realización de copias de seguridad de volumen mientras las aplicaciones de un sistema siguen escribiendo en los volúmenes. VSS proporciona una interfaz coherente que permite la coordinación entre las aplicaciones de usuario que actualizan los datos del disco (objetos de escritura) y los que realizan copias de seguridad de las aplicaciones (solicitantes).  
  
 VSS captura y copia imágenes estables para la creación de copias de seguridad en sistemas en ejecución, especialmente servidores, sin degradar innecesariamente el rendimiento y la estabilidad de los servicios que proporcionan. Para obtener más información acerca de VSS, vea la documentación de Windows.  

> [!NOTE]
> Si utiliza VSS para realizar copias de seguridad de una máquina virtual que hospeda un grupo de disponibilidad básico, si la máquina virtual hospeda actualmente bases de datos que se encuentran en un estado secundario, comenzando por [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 CU2 y [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU9, esas bases de datos *no* se copiarán con la máquina virtual.  Esto se debe a que los grupos de disponibilidad básicos no admiten la realización de copias de seguridad de bases de datos en la réplica secundaria.  Antes de estas versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la copia de seguridad podría producir un error.
  
## <a name="virtual-backup-device-interface-vdi"></a>Interfaz del dispositivo de copia de seguridad virtual (VDI)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ofrece una API denominada interfaz del dispositivo de copia de seguridad virtual (VDI) que permite a los proveedores de software independientes integrar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en sus productos para ofrecer la compatibilidad con las operaciones relativas a las copias de seguridad y restauración. Estas API están diseñadas para ofrecer una confiabilidad y rendimiento máximos, así como para ser compatibles con todas las funciones relativas a las copias de seguridad y restauración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , incluidas todas las capacidades de copias de seguridad interactivas y de instantáneas.  
  
## <a name="permissions"></a>Permisos  
 El servicio del objeto de escritura de SQL debe ejecutarse en la cuenta **Sistema local** . El servicio del objeto de escritura de SQL usa el inicio de sesión **NT Service\SQLWriter** para conectarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El uso del inicio de sesión **NT Service\SQLWriter** permite que el proceso del objeto de escritura de SQL se ejecute en un nivel de privilegios menor en una cuenta designada como **ningún inicio de sesión**, lo que limita la vulnerabilidad. Si el servicio del objeto de escritura de SQL está deshabilitado, cualquier utilidad que emplee instantáneas de VSS, como System Center Data Protection Manager, así como otros productos de terceros, dejaría de funcionar, o lo que es peor, con el riesgo de realizar copias de seguridad de bases de datos que no fueran coherentes. Si ni [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el sistema en el que se ejecuta o el sistema host (en el caso de una máquina virtual) necesitan usar otra cosa que no sea la copia de seguridad de [!INCLUDE[tsql](../../includes/tsql-md.md)] , se puede deshabilitar el servicio del objeto de escritura de SQL y quitar el inicio de sesión de forma segura.  Tenga en cuenta que una copia de seguridad de nivel del sistema o de volumen puede invocar el servicio del objeto de escritura de SQL, tanto si la copia de seguridad se basa directamente en instantáneas como si no. Algunos productos de copia de seguridad del sistema usan VSS para evitar quedar bloqueados por archivos abiertos o bloqueados. El Servicio del objeto de escritura de SQL necesita permisos elevados en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] porque en el transcurso de sus actividades inmoviliza brevemente toda la E/S para la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="features"></a>Características  
 El objeto de escritura de SQL es compatible con las operaciones siguientes:  
  
-   Copias de seguridad y restauración completas de la base de datos, incluidos los catálogos de texto completo  
  
-   Copias de seguridad y restauración diferenciales  
  
-   Restauración con desplazamiento  
  
-   Cambio de nombre de una base de datos  
  
-   Copia de seguridad de solo copia  
  
-   Recuperación automática de instantánea de base de datos  
  
 El objeto de escritura de SQL no es compatible con las operaciones siguientes:  
  
-   Copias de seguridad de registros  
  
-   Copia de seguridad de archivos y grupos de archivos  
  
-   Restauración de página  
  
## <a name="remarks"></a>Notas
El servicio SQL Writer es un servicio independiente del motor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y se comparte entre diferentes versiones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y entre diferentes instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el mismo servidor.  El archivo de servicio de SQL Writer se envía como parte del paquete de instalación [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y se marcará con el mismo número de versión que el motor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con el que se envía.  Cuando se instala una nueva instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un servidor o se actualiza una instancia existente, si el número de versión de la instancia que se instala o actualiza es mayor que el número de versión del servicio SQL Writer que se encuentra actualmente en el servidor, ese archivo se reemplazará por el del paquete de instalación.  Tenga en cuenta que si el servicio SQL Writer se actualizó mediante un Service Pack o una actualización acumulativa y se está instalando una versión RTM de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], es posible sustituir una versión más reciente del servicio SQL Writer por otra más antigua, siempre que la instalación tenga un mayor número de versión principal.  Por ejemplo, el servicio SQL Writer se actualizó en [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP2 CU2.  Si esa instancia se actualiza a [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] RTM, el servicio SQL Writer actualizado se reemplazará por una versión anterior.  En este caso, necesitaría aplicar la última actualización acumulativa a la nueva instancia para obtener la versión más reciente del servicio SQL Writer.

