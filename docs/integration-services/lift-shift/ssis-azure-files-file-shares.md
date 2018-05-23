---
title: Conectarse a archivos y recursos compartidos de archivos de forma local y en Azure | Microsoft Docs
description: En este artículo se describe cómo usar el sistema de archivos y los recursos compartidos de archivos, de forma local y en Azure, con SSIS.
ms.date: 11/27/2017
ms.topic: conceptual
ms.prod: sql
ms.technology:
- integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 6472263658ed831aade7d0951b10a712dfee312d
ms.sourcegitcommit: 0cc2cb281e467a13a76174e0d9afbdcf4ccddc29
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/15/2018
---
# <a name="connect-to-files-and-file-shares-on-premises-and-in-azure-with-ssis"></a>Conectarse a archivos y recursos compartidos de archivos de forma local y en Azure con SSIS
En este artículo se describe cómo actualizar los paquetes de SQL Server Integration Services (SSIS) cuando se elevan y desplazan paquetes que usan sistemas de archivos locales a SSIS de Azure.

> [!IMPORTANT]
> Actualmente, la base de datos del catálogo de SSIS (SSISDB) solo admite un único conjunto de credenciales de acceso. Por lo tanto, Integration Runtime (IR) de SSIS de Azure no puede usar credenciales diferentes para conectarse a diferentes recursos compartidos de archivos de forma local y a recursos compartidos de Azure Files.

## <a name="store-temporary-files"></a>Almacenar archivos temporales
Si necesita almacenar y procesar archivos temporales durante la ejecución de un paquete único, los paquetes pueden usar la carpeta de trabajo actual (`.`) o la carpeta temporal (`%TEMP%`) de los nodos de Integration Runtime de SSIS de Azure.

## <a name="store-files-across-multiple-package-executions"></a>Almacenar archivos en varias ejecuciones de paquetes
Si necesita almacenar y procesar archivos permanentes y hacer que persistan durante varias ejecuciones de paquetes, puede usar los recursos compartidos de archivos locales o Azure Files.

### <a name="use-on-premises-file-shares"></a>Usar recursos compartidos de archivos locales
Para seguir usando **recursos compartidos de archivos locales** al elevar y desplazar paquetes que usan sistemas de archivos locales a SSIS de Azure, haga lo siguiente:
1.  Transfiera los archivos de los sistemas de archivos locales a recursos compartidos de archivos locales.
2.  Una los recursos compartidos de archivos locales a Azure Virtual Network (VNet).
3.  Una la instancia de IR de SSIS de Azure a la misma red virtual. Para obtener más información, consulte [Unión de una instancia de Integration Runtime de SSIS de Azure a una red virtual](https://docs.microsoft.com/azure/data-factory/join-azure-ssis-integration-runtime-virtual-network).
4.  Conecte la instancia de IR de SSIS de Azure al recurso compartido de archivos locales de la misma red virtual mediante la configuración de las credenciales de acceso que usan la autenticación de Windows. Para obtener más información, consulte [Connect to on-premises data sources and Azure file shares with Windows Authentication](ssis-azure-connect-with-windows-auth.md) (Conectarse a orígenes de datos locales y a recursos compartidos de archivos de Azure con la autenticación de Windows).
5.  Actualice las rutas de acceso de archivos locales en los paquetes a rutas de acceso UNC que apuntan a los recursos compartidos de archivos locales. Por ejemplo, actualice `C:\abc.txt` a `\\<on-prem-server-name>\<share-name>\abc.txt`.

### <a name="use-azure-file-shares"></a>Usar recursos compartidos de archivos de Azure
Para usar **Azure Files** al elevar y desplazar paquetes que usan sistemas de archivos locales a SSIS de Azure, haga lo siguiente:
1.  Transfiera archivos de los sistemas de archivos locales a Azure Files. Para obtener más información, consulte [Azure Files](https://azure.microsoft.com/services/storage/files/).
2.  Conecte la instancia de IR de SSIS de Azure a Azure Files mediante la configuración de las credenciales de acceso que usan la autenticación de Windows. Para obtener más información, consulte [Connect to on-premises data sources and Azure file shares with Windows Authentication](ssis-azure-connect-with-windows-auth.md) (Conectarse a orígenes de datos locales y a recursos compartidos de archivos de Azure con la autenticación de Windows).
3.  Actualice las rutas de acceso de archivos locales en los paquetes a rutas de acceso UNC que apuntan a Azure Files. Por ejemplo, actualice `C:\abc.txt` a `\\<storage-account-name>.file.core.windows.net\<share-name>\abc.txt`.
