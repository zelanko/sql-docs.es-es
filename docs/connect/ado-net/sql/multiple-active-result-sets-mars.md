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
ms.openlocfilehash: 4475e4b8a71b4abcf4e1c2324a49e03a8bb64fbb
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "78896671"
---
# <a name="multiple-active-result-sets-mars"></a>Conjuntos de resultados activos múltiples (MARS)

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

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
