---
title: Abrir y guardar archivos con paquetes SSIS implementados en Azure | Microsoft Docs
description: Obtenga información sobre cómo abrir y guardar archivos de forma local y en Azure al aplicar lift-and-shift a los paquetes SSIS que usan los sistemas de archivos locales en SSIS en Azure.
ms.date: 11/27/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: integration-services
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: c4f9d5e91db382d59dc156ed919c1af06cc56b77
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/12/2018
ms.locfileid: "35410477"
---
# <a name="open-and-save-files-on-premises-and-in-azure-with-ssis-packages-deployed-in-azure"></a>Abrir y guardar archivos de forma local y en Azure con paquetes SSIS implementados en Azure

En este artículo se describe cómo abrir y guardar archivos de forma local y en Azure al aplicar lift-and-shift a los paquetes SSIS que usan los sistemas de archivos locales en SSIS en Azure.

> [!IMPORTANT]
> Actualmente, el catálogo de SSIS (SSISDB) solo admite un único conjunto de credenciales de acceso. Como resultado, no se pueden usar otros conjuntos de credenciales para conectarse a varios recursos compartidos de archivos de forma local y a recursos compartidos de Azure Files.

## <a name="save-temporary-files"></a>Guardar los archivos temporales
Si necesita almacenar y procesar archivos temporales durante la ejecución de un paquete único, los paquetes pueden usar la carpeta de trabajo actual (`.`) o la carpeta temporal (`%TEMP%`) de los nodos de Integration Runtime de SSIS de Azure.

## <a name="use-on-premises-file-shares"></a>Usar recursos compartidos de archivos locales
Para seguir usando **recursos compartidos de archivos locales** al elevar y desplazar paquetes que usan sistemas de archivos locales a SSIS de Azure, haga lo siguiente:
1.  Transfiera los archivos de los sistemas de archivos locales a recursos compartidos de archivos locales.
2.  Una los recursos compartidos de archivos locales a una red virtual de Azure.
3.  Una la instancia de Azure SSIS IR a la misma red virtual. Para obtener más información, consulte [Unión de una instancia de Integration Runtime de SSIS de Azure a una red virtual](https://docs.microsoft.com/azure/data-factory/join-azure-ssis-integration-runtime-virtual-network).
4.  Conecte la instancia de Azure SSIS IR al recurso compartido de archivos locales dentro de la misma red virtual mediante la configuración de credenciales de acceso que usan la autenticación de Windows. Para obtener más información, vea [Conexión a datos y a recursos compartidos de archivos con la autenticación de Windows](ssis-azure-connect-with-windows-auth.md).
5.  Actualice las rutas de acceso de archivos locales en los paquetes a rutas de acceso UNC que apuntan a los recursos compartidos de archivos locales. Por ejemplo, actualice `C:\abc.txt` a `\\<on-prem-server-name>\<share-name>\abc.txt`.

## <a name="use-azure-file-shares"></a>Usar recursos compartidos de archivos de Azure
Para usar **Azure Files** al elevar y desplazar paquetes que usan sistemas de archivos locales a SSIS de Azure, haga lo siguiente:
1.  Transfiera archivos de los sistemas de archivos locales a Azure Files. Para obtener más información, consulte [Azure Files](https://azure.microsoft.com/services/storage/files/).
2.  Conecte la instancia de IR de SSIS de Azure a Azure Files mediante la configuración de las credenciales de acceso que usan la autenticación de Windows. Para obtener más información, vea [Conexión a datos y a recursos compartidos de archivos con la autenticación de Windows](ssis-azure-connect-with-windows-auth.md).
3.  Actualice las rutas de acceso de archivos locales en los paquetes a rutas de acceso UNC que apuntan a Azure Files. Por ejemplo, actualice `C:\abc.txt` a `\\<storage-account-name>.file.core.windows.net\<share-name>\abc.txt`.
