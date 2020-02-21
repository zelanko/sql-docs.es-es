---
title: Conjuntos de resultados activos múltiples (MARS)
description: Describe cómo tener más de un objeto SqlDataReader abierto en una conexión cuando cada instancia de SqlDataReader se inicia desde un comando independiente.
ms.date: 08/15/2019
ms.assetid: c90ef863-bac7-44cf-adc1-f05c36fcf57d
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 60c27bd94162b4d6bf4d7370218e1fa7781e6491
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "75247699"
---
# <a name="multiple-active-result-sets-mars"></a>Conjuntos de resultados activos múltiples (MARS)

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Descargar ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

Los conjuntos de resultados activos múltiples (MARS) son una característica que permite la ejecución de varios lotes en una sola conexión. En versiones anteriores, solo se podía ejecutar un lote a la vez en una sola conexión. La ejecución de varios lotes con MARS no implica la ejecución simultánea de las operaciones.  
  
## <a name="in-this-section"></a>En esta sección  
[Habilitación de conjuntos de resultados activos múltiples](enable-multiple-active-result-sets.md)  
Describe cómo usar MARS con SQL Server.  
  
[Manipulación de datos](manipulate-data.md)  
Proporciona ejemplos de codificación de aplicaciones de MARS.  
  
## <a name="related-sections"></a>Secciones relacionadas  
[Operaciones asincrónicas](asynchronous-operations.md)  
Proporciona detalles sobre el uso de las nuevas características asincrónicas de .NET.  
  
## <a name="next-steps"></a>Pasos siguientes
- [SQL Server y ADO.NET](index.md)
