---
title: Conjuntos de resultados activos múltiples (MARS)
description: Describe cómo tener más de un objeto SqlDataReader abierto en una conexión cuando cada instancia de SqlDataReader se inicia desde un comando independiente.
ms.date: 08/15/2019
ms.assetid: c90ef863-bac7-44cf-adc1-f05c36fcf57d
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: e93493a28adfecd7dd39c79a86170b06ed18b992
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80924287"
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
