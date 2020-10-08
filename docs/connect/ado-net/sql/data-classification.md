---
title: Clasificación y detección de datos en SqlClient
description: Describe cómo comprobar si una base de datos de SQL Server admite la clasificación de datos y cómo obtener acceso a la información de clasificación de datos a través de un objeto SqlDataReader.
ms.date: 06/15/2020
dev_langs:
- csharp
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: johnnypham
ms.author: v-jopha
ms.reviewer: ''
ms.openlocfilehash: b53e71c4c302145af14c1f2e37f30fe0e3c8f8e2
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/05/2020
ms.locfileid: "91725726"
---
# <a name="data-discovery-and-classification-in-sqlclient"></a>Clasificación y detección de datos en SqlClient

[!INCLUDE[appliesto-netfx-netcore-netst-md](../../../includes/appliesto-netfx-netcore-netst-md.md)]

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

La [clasificación y detección de datos](../../../relational-databases/security/sql-data-discovery-and-classification.md?view=sql-server-2017) es un conjunto de servicios avanzados para detectar, clasificar, etiquetar y notificar información confidencial en las bases de datos. SqlClient proporciona una API que expone información de clasificación y detección de datos de solo lectura cuando el origen subyacente es compatible con la característica. Se obtiene acceso a esta información a través de SqlDataReader.

En esta aplicación de ejemplo se muestra cómo acceder a las propiedades de clasificación de datos de SqlDataReader.

[!code-csharp [SqlDataReader_DataDiscoveryAndClassification#1](~/../sqlclient/doc/samples/SqlDataReader_DataDiscoveryAndClassification.cs#1)]

**Consulte también**  

 [Características de SQL Server y ADO.NET](sql-server-features-adonet.md)