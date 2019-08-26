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
ms.openlocfilehash: a0ad547d26c86c43b0009cdf20acae33ed7e8ab7
ms.sourcegitcommit: 57e20b7d02853ec9af46b648106578aed133fb45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/16/2019
ms.locfileid: "69553235"
---
# <a name="microsoft-connector-for-oracle"></a>Microsoft Connector for Oracle

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

Microsoft Connector for Oracle permite exportar datos desde un origen de datos de Oracle y cargar datos en él en un paquete SSIS.

## <a name="version-support"></a>Compatibilidad de versiones

Microsoft Connector for Oracle admite los siguientes productos de Microsoft SQL Server:

- Desde SQL Server 2019
- SQL Server Data Tools (SSDT)

Se admiten las siguientes versiones de la base de datos de Oracle del origen de datos:

- Oracle 10.x
- Oracle 11.x
- Oracle 12c
- Oracle 18c (sin compatibilidad con la autenticación de Windows)

La base de datos de Oracle es compatible con todos los sistemas operativos y plataformas.
> [!NOTE]
>
> Microsoft Connector for Oracle Database no necesita el cliente Oracle en SQL Server 2019.

## <a name="installation"></a>Installation

Si tiene que ejecutar el paquete en SQL Server, puede obtener el programa de instalación de Microsoft Connector for Oracle Database [aquí](https://www.microsoft.com/en-us/download/details.aspx?id=58228). A continuación, siga las instrucciones del asistente para la instalación.

Después de instalar el conector, debe reiniciar el Servicio de integración de SQL Server para asegurarse de que el origen y el destino de Oracle funcionen correctamente.

Si tiene que diseñar el paquete con el conector, no es necesario que lo descargue. SQL Server Data Tools (SSDT) lo incluye desde la versión 15.9.0.

## <a name="uninstallation"></a>Desinstalación

Puede ejecutar el Asistente para desinstalación para quitar Microsoft Connector for Oracle Database de SQL Server.

## <a name="design-ssis-package-with-previous-version"></a>Diseño de un paquete SSIS con una versión anterior

Desde la versión 15.9.0, SSDT ya incluye Microsoft Connector for Oracle Database, por lo que no necesita realizar ninguna instalación cuando diseñe paquetes SSIS que tengan como destino SQL Server 2019.

Para diseñar un paquete SSIS que tenga como destino SQL Server 2017 y versiones anteriores, sí debe instalar Connector for Oracle de Attunity con la versión correspondiente.

**Vínculos de descarga:**

- [SQL Server 2017: Microsoft Connector Version 5.0 for Oracle de Attunity](https://www.microsoft.com/en-us/download/details.aspx?id=55179)
- [SQL Server 2016: Microsoft Connector Version 4.0 for Oracle de Attunity](https://www.microsoft.com/en-us/download/details.aspx?id=52950)
- [SQL Server 2014: Microsoft Connector Version 3.0 for Oracle de Attunity](https://www.microsoft.com/en-us/download/details.aspx?id=44582)
- [SQL Server 2012: Microsoft Connector Version 2.0 for Oracle de Attunity](https://www.microsoft.com/en-us/download/details.aspx?id=29283)

## <a name="next-steps"></a>Pasos siguientes

- Configure el [Administrador de conexiones de Oracle](oracle-connection-manager.md).
- Configure el [origen de Oracle](oracle-source.md).
- Configure el [destino de Oracle](oracle-destination.md).
- Si tiene alguna pregunta, visite [TechCommunity](https://aka.ms/AA5u35j).
