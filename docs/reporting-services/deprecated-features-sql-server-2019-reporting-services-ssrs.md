---
title: Características en desuso de SQL Server 2019 Reporting Services | Microsoft Docs
description: En este artículo se describen las características que dejarán de usarse en la próxima versión de SQL Server Reporting Services.
ms.date: 11/21/2019
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
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: eaa7edebe99a7c444fe1bfa23971317517399ea2
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "74320279"
---
# <a name="deprecated-features-in-sql-server-2019-reporting-services"></a>Características en desuso de SQL Server 2019 Reporting Services

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2019-and-later](../includes/ssrs-appliesto-2019-and-later.md)] [!INCLUDE [ssrs-appliesto-pbirs](../includes/ssrs-appliesto-pbirs.md)]

Cuando marcamos una característica como en desuso, significa que:

- Solo está en modo de mantenimiento. No se realizarán cambios nuevos, ni tampoco cambios relacionados con la interoperabilidad con características nuevas.
- Nos esforzamos por no quitar una característica en desuso en las versiones futuras para facilitar las actualizaciones, aunque en raras ocasiones puede que optemos por quitar permanentemente la característica de Reporting Services si limita las innovaciones futuras.
- Para un nuevo trabajo de desarrollo, no se recomienda el uso de las características en desuso.

**Características en desuso en una versión futura de SQL Server**

SQL Server Reporting Services admite las siguientes características en la próxima versión de SQL Server, pero las dejará en desuso en una versión posterior. No se ha determinado la versión específica de SQL Server.

| **Categoría** | **Característica en desuso** | **Sustitución** |
| --- | --- | --- |
| Servidor de informes | Galería de elementos de informe | None |
| Servidor de informes | Informes móviles y Publicador de informes móviles | Los informes de Power BI en Power BI Report Server ofrecen funcionalidades móviles. |
| Servidor de informes | Formatos de representación XLS y DOC | Los formatos XLSX y DOCX están disponibles y son compatibles. |
| Servidor de informes | Fuente de distribución de datos Atom | La compatibilidad con fuentes de oData está disponible para los conjuntos de valores compartidos en SSRS y Power BI Report Server. |

## <a name="see-also"></a>Consulte también

[Funcionalidad no incluida en SQL Server 2019 Reporting Services (SSRS)](discontinued-functionality-sql-server-reporting-services-2019.md)

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231).
