---
title: Características en desuso de SQL Server 2017 Reporting Services | Microsoft Docs
description: En este artículo se describen las características que dejarán de usarse en la próxima versión de SQL Server Reporting Services.
ms.date: 11/20/2019
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- Reporting Services, backward compatibility
- deprecated features [Reporting Services]
- HTML OWC rendering extension [Reporting Services]
- Report Server Web service, endpoints
ms.assetid: 3876c01e-f81d-4cce-9104-5106a8c369e6
author: maggiesMSFT
ms.author: maggies
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: d8fe51ce9d86688669e84ad866ad9f5e6da075e8
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "74320319"
---
# <a name="deprecated-features-in-sql-server-2017-reporting-services"></a>Características en desuso de SQL Server 2017 Reporting Services

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2017](../includes/ssrs-appliesto-2017.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../includes/ssrs-appliesto-not-pbirs.md)]

Cuando marcamos una característica como en desuso, significa que:

- Solo está en modo de mantenimiento. No se realizarán cambios nuevos, ni tampoco cambios relacionados con la interoperabilidad con características nuevas.
- Nos esforzamos por no quitar una característica en desuso en las versiones futuras para facilitar las actualizaciones, aunque en raras ocasiones puede que optemos por quitar permanentemente la característica de Reporting Services si limita las innovaciones futuras.
- Para un nuevo trabajo de desarrollo, no se recomienda el uso de las características en desuso.

## <a name="features-deprecated-in-the-next-version-of-sql-server"></a>Características en desuso en la próxima versión de SQL Server

Las siguientes características de SQL Server 2017 Reporting Services no se admitirán en la próxima versión de SQL Server. No use estas características en nuevos trabajos de desarrollo y modifique lo antes posible las aplicaciones que las usan actualmente.

> [!NOTE]
> Esta lista es idéntica a la lista de SQL Server 2016 Reporting Services (13.x). No hay anunciada ninguna nueva característica en desuso o descontinuada para SQL Server 2017 Reporting Services (14.x).


| **Categoría** | **Característica en desuso** | **Sustitución** |
| --- | --- | --- |
| Servidor de informes | Representador de HTML 4.0 | Representador de HTML 5 |

## <a name="see-also"></a>Consulte también

[Funcionalidad no incluida en SQL Server Reporting Services (SSRS)](discontinued-functionality-to-sql-server-reporting-services-in-sql-server.md)

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231).
