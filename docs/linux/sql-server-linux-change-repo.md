---
title: Registrar el el repositorio de disponibilidad General de SQL Server en Linux | Documentos de Microsoft
description: "Cambiar repositorios desde el repositorio de vista previa 2017 de SQL Server en el repositorio de disponibilidad General (GA) en Linux (GA se también conoce a veces como RTM)."
author: annashres
ms.author: anshrest
manager: jhubbard
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.workload: Inactive
ms.openlocfilehash: 53c2c674c90b327cfe4baf2d109fab09d045f890
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/01/2017
---
# <a name="change-repositories-from-the-preview-repository-to-the-ga-repository"></a>Repositorios de cambio desde el repositorio de vista previa en el repositorio de GA

Cuando se actualiza SQL Server 2017 desde CTP 2.1, RC1 o RC2 a la versión de disponibilidad General (GA) tendrá que cambiar repositorios. Las siguientes secciones explican la elección de repositorios y cómo realizar el cambio antes de actualizar.

## <a name="repository-choices"></a>Opciones de repositorio

Es importante tener en cuenta que hay dos tipos principales de repositorios para cada distribución:

  > [!IMPORTANT]
  > Cualquier versión anterior de CTP 2.1 debe actualizarse al menos 2.1 antes de actualizar a la versión de GA.

- **Las actualizaciones acumulativas (CU)**: repositorio de actualización acumulativa The (CU) contiene los paquetes para la versión de SQL Server base y cualquier correcciones o mejoras desde esa versión. Las actualizaciones acumulativas son específicas de una versión de lanzamiento, por ejemplo, SQL Server 2017. Se publican a un ritmo regular.

- **GDR**: repositorio el GDR contiene paquetes para la versión de SQL Server base y solo correcciones críticas y actualizaciones de seguridad desde esa versión. Estas actualizaciones también se agregan a la próxima versión CU.

Cada versión CU y GDR contiene el paquete completo de SQL Server y todas las actualizaciones anteriores para ese repositorio. Se admite la actualización desde una versión GDR a una versión CU cambiando su repositorio configurado para SQL Server. También puede [degradar](sql-server-linux-setup.md#rollback) a cualquier versión dentro de la versión principal (por ejemplo: 2017).

> [!NOTE]
> Puede actualizar desde una versión GDR a CU cambiando los repositorios de la versión en cualquier momento. Actualizar desde una CU no se admite la versión a una versión GDR. 

## <a name="change-to-a-ga-repository"></a>Cambiar a un repositorio de GA

Para cambiar desde el repositorio de vista previa en un repositorio de origen (CU o GDR), siga estos pasos:

1. Eliminar el repositorio de vista previa configurada previamente.

   | Plataforma | Comando de eliminación de repositorio |
   |-----|-----|
   | RHEL | `sudo rm -rf /etc/yum.repos.d/mssql-server.repo` |
   | SLES GRANDE | `sudo zypper removerepo 'packages-microsoft-com-mssql-server'` |
   | Ubuntu | `sudo add-apt-repository -r 'deb [arch=amd64] https://packages.microsoft.com/ubuntu/16.04/mssql-server xenial main'` |

1. Para **Ubuntu solo**, importe las claves GPG repositorio público.

   ```bash
   sudo curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
   ```

1. Configure el nuevo repositorio.

   | Plataforma | Repositorio | Command |
   |-----|-----|-----|
   | RHEL | CU | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017.repo` |
   | RHEL | GDR | `sudo curl -o /etc/yum.repos.d/mssql-server.repo https://packages.microsoft.com/config/rhel/7/mssql-server-2017-gdr.repo` |
   | SLES GRANDE | CU  | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017.repo` |
   | SLES GRANDE | GDR | `sudo zypper addrepo -fc https://packages.microsoft.com/config/sles/12/mssql-server-2017-gdr.repo` |
   | Ubuntu | CU | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017.list)" && sudo apt-get update` |
   | Ubuntu | GDR | `sudo add-apt-repository "$(curl https://packages.microsoft.com/config/ubuntu/16.04/mssql-server-2017-gdr.list)" && sudo apt-get update` |

1. [Instalar](sql-server-linux-setup.md#platforms) o [actualizar](sql-server-linux-setup.md#upgrade) SQL Server con el repositorio de GA.

   > [!IMPORTANT]
   > En este punto, si decide realizar una instalación completa con la [tutoriales](#platforms), recuerde que acaba de configurar el repositorio de destino. No repita este paso en los tutoriales. Esto es especialmente cierto si configura el repositorio GDR, ya que los tutoriales usan el repositorio de CU.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre cómo instalar SQL Server 2017 en Linux, consulte [Guía de instalación para SQL Server en Linux](sql-server-linux-setup.md).
