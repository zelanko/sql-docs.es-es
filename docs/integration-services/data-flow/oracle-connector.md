---
title: Microsoft Connector for Oracle | Microsoft Docs
ms.custom: ''
ms.date: 08/14/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 92aaf7c04d7a5e176fce4448b9d4f6172b541647
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "75755841"
---
# <a name="microsoft-connector-for-oracle"></a>Microsoft Connector for Oracle

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

Microsoft Connector for Oracle permite exportar datos desde un origen de datos de Oracle y cargar datos en él en un paquete SSIS.

## <a name="version-support"></a>Compatibilidad con versiones

Microsoft Connector for Oracle admite los siguientes productos de Microsoft SQL Server:

- Desde SQL Server 2019
- SQL Server Data Tools (SSDT) a partir de la versión 15.9.3

Se admiten las siguientes versiones de la base de datos de Oracle del origen de datos:

- Oracle 10.x
- Oracle 11.x
- Oracle 12c
- Oracle 18c (sin compatibilidad con la autenticación de Windows)

La base de datos de Oracle es compatible con todos los sistemas operativos y plataformas.
> [!NOTE]
>
> Microsoft Connector for Oracle Database no necesita el cliente de Oracle en SQL Server 2019.

## <a name="installation"></a>Instalación

Para instalar el conector para la base de datos de Oracle, descargue y ejecute el instalador a partir de la [última versión del conector de Microsoft para Oracle](https://www.microsoft.com/download/details.aspx?id=58228). A continuación, siga las instrucciones del asistente para la instalación.

Después de instalar el conector, debe reiniciar el Servicio de integración de SQL Server para asegurarse de que el origen y el destino de Oracle puedan funcionar correctamente.

Para ejecutar un paquete SSIS que tenga como destino SQL Server 2017 y versiones anteriores, además de **Microsoft Connector for Oracle**, tendrá que instalar el **cliente de Oracle** y **Microsoft Connector for Oracle de Attunity** con la versión correspondiente, disponibles en los vínculos siguientes:

- [SQL Server 2017: Microsoft Connector Version 5.0 for Oracle de Attunity](https://www.microsoft.com/download/details.aspx?id=55179)
- [SQL Server 2016: Microsoft Connector Version 4.0 for Oracle de Attunity](https://www.microsoft.com/download/details.aspx?id=52950)
- [SQL Server 2014: Microsoft Connector Version 3.0 for Oracle de Attunity](https://www.microsoft.com/download/details.aspx?id=44582)
- [SQL Server 2012: Microsoft Connector Version 2.0 for Oracle de Attunity](https://www.microsoft.com/download/details.aspx?id=29283)

## <a name="uninstallation"></a>Desinstalación

Puede ejecutar el Asistente para desinstalación para quitar Microsoft Connector for Oracle Database de SQL Server.

## <a name="next-steps"></a>Pasos siguientes

- Configure el [Administrador de conexiones de Oracle](oracle-connection-manager.md).
- Configure el [origen de Oracle](oracle-source.md).
- Configure el [destino de Oracle](oracle-destination.md).
- Si tiene alguna pregunta, visite [TechCommunity](https://aka.ms/AA5u35j).
