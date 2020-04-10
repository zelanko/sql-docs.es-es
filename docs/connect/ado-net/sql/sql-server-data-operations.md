---
title: Operaciones de datos de SQL Server en ADO.NET
description: Describe cómo trabajar con datos en SQL Server. Contiene secciones sobre las operaciones de copia masiva, MARS, las operaciones asincrónicas y los parámetros con valores de tabla.
ms.date: 08/15/2019
ms.assetid: b864ebc9-ed8e-4059-85fd-36d9198f5521
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daenge
ms.reviewer: v-kaywon
ms.openlocfilehash: f6e842b38291fb704828b9b5a70d0652cfda51e0
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80920990"
---
# <a name="sql-server-data-operations-in-adonet"></a>Operaciones de datos de SQL Server en ADO.NET

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

En esta sección se describen las funcionalidades y características de SQL Server específicas del proveedor de datos SqlClient de Microsoft para SQL Server (<xref:Microsoft.Data.SqlClient>).  
  
## <a name="in-this-section"></a>En esta sección  
[Operaciones de copia masiva en SQL Server](bulk-copy-operations-sql-server.md)  
Describe la funcionalidad de copia masiva del proveedor de datos de .NET para SQL Server.  
  
[Conjuntos de resultados activos múltiples (MARS)](multiple-active-result-sets-mars.md)  
Describe cómo tener más de un objeto <xref:Microsoft.Data.SqlClient.SqlDataReader> abierto en una conexión cuando cada instancia de <xref:Microsoft.Data.SqlClient.SqlDataReader> se inicia desde un comando independiente.  
  
[Operaciones asincrónicas](asynchronous-operations.md)  
Describe cómo realizar operaciones asincrónicas de base de datos mediante una API modelada según el modelo asincrónico usado por .NET Framework.  
  
[Parámetros con valores de tabla](table-valued-parameters.md)  
Describe cómo trabajar con parámetros con valores de tabla, que se introdujeron en SQL Server 2008.  
  
## <a name="next-steps"></a>Pasos siguientes
- [SQL Server y ADO.NET](index.md)
